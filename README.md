# Git + GitHub — Guia passo a passo

Material prático para aprender **Git e GitHub do zero**, usando um repositório local até o envio para um repositório remoto.

## Objetivos

Ao final, o estudante deverá conseguir:

- diferenciar Git de GitHub;
- configurar nome e e-mail no Git;
- criar e inicializar um repositório local;
- entender Working Directory, Staging Area e Commit;
- usar `status`, `add`, `commit`, `log` e `diff`;
- conectar o projeto local ao GitHub usando `origin`;
- fazer `push`, `pull` e `clone`;
- criar uma branch para desenvolver uma alteração;
- usar `.gitignore` e evitar o envio de informações sensíveis.

## Antes de começar: como Git, branches e trabalho distribuído funcionam

### Git como uma linha do tempo

O Git registra a evolução do projeto por meio de **commits**. Pense em cada commit como um ponto seguro da história do software:

```text
C1 projeto inicial → C2 cria login → C3 corrige validação → C4 novo layout
```

O fluxo básico é:

```text
Arquivos → git add → Staging Area → git commit → Histórico → git push → GitHub
```

### O que é uma branch?

Uma **branch** é uma linha paralela de desenvolvimento. Ela permite implementar uma tarefa sem modificar diretamente a `main`.

```text
main             ●────●──────────────●
                       \              ↑ merge
feature/login          ●────●────●────┘
```

Exemplo para criar uma branch:

```bash
git branch
git switch -c feature/login
git branch
```

O `*` mostrado por `git branch` indica a branch atual.

Uma convenção simples para estudar é:

```text
feature/login
feature/cadastro
fix/validacao-email
```

### Por que o Git é chamado de distribuído?

Cada desenvolvedor possui uma **cópia local completa** do repositório e de seu histórico. O GitHub funciona como um ponto remoto de colaboração e sincronização.

```text
                 push                 pull
Ana / repositório local ───→ GitHub ←─── João / repositório local
       feature/login                    feature/cadastro
```

Ana pode trabalhar em `feature/login` enquanto João trabalha em `feature/cadastro`. Cada um cria commits localmente e envia sua branch ao GitHub.

### Fluxo de uma equipe

```text
1. git pull                    → atualizar o projeto
2. git switch -c feature/...  → criar uma branch para a tarefa
3. git add + git commit       → registrar o trabalho local
4. git push                   → publicar a branch no GitHub
5. Pull Request               → revisar e integrar a alteração
```

Exemplo:

```bash
git pull
git switch -c feature/minha-tarefa
# altere os arquivos
git add .
git commit -m "feat: implementa minha tarefa"
git push -u origin feature/minha-tarefa
```

Depois do `push`, a equipe pode abrir um **Pull Request** no GitHub para revisar a alteração antes de integrá-la à `main`.

---

## 1. Verificar o Git

```bash
git --version
```

O comando confirma se o Git está instalado e mostra a versão disponível.

## 2. Configurar sua identidade

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seuemail@exemplo.com"
```

Confira:

```bash
git config --global --list
```

`--global` aplica a configuração aos repositórios usados por esse usuário no computador. O nome e o e-mail ficam associados aos commits.

## 3. Criar o projeto local

```bash
mkdir projeto-git
cd projeto-git
```

Crie um arquivo `README.md` dentro da pasta.

## 4. Inicializar o repositório

```bash
git init -b main
```

Agora a pasta é um repositório Git. O Git cria internamente o diretório `.git`, responsável pelos metadados e histórico.

## 5. Verificar o estado do projeto

```bash
git status
```

Use `git status` com frequência. Ele informa a branch atual e quais arquivos estão novos, modificados ou preparados para commit.

## 6. Preparar as alterações

Um arquivo específico:

```bash
git add README.md
```

Todos os arquivos alterados da pasta:

```bash
git add .
```

Fluxo mental:

```text
Working Directory --git add--> Staging Area --git commit--> Histórico
```

## 7. Criar o primeiro commit

```bash
git commit -m "docs: adiciona README inicial"
```

O commit cria um ponto no histórico com as alterações que estavam no stage.

Exemplos de mensagens:

```text
feat: adiciona cadastro de usuário
fix: corrige validação de e-mail
docs: atualiza instruções do projeto
```

## 8. Consultar o histórico

```bash
git log --oneline
```

Cada commit possui um identificador e uma mensagem.

## 9. Criar um repositório no GitHub

No GitHub, crie um repositório vazio chamado, por exemplo, `projeto-git`.

Para este exercício, como o projeto já possui um commit local, prefira criar o repositório remoto **sem inicializar README, `.gitignore` ou licença**.

## 10. Configurar o remote `origin`

Copie a URL HTTPS do repositório criado e execute:

```bash
git remote add origin https://github.com/SEU-USUARIO/projeto-git.git
```

Verifique:

```bash
git remote -v
```

`origin` é o nome convencional usado para representar o repositório remoto principal.

Se `origin` já existir e você precisar trocar a URL:

```bash
git remote set-url origin https://github.com/SEU-USUARIO/OUTRO-REPOSITORIO.git
```

## 11. Enviar o projeto para o GitHub

```bash
git push -u origin main
```

- `push`: envia commits locais;
- `origin`: remoto de destino;
- `main`: branch enviada;
- `-u`: registra o upstream da branch.

Nos próximos envios, normalmente basta:

```bash
git push
```

## 12. Fluxo diário

Depois de alterar arquivos:

```bash
git status
git diff
git add .
git commit -m "feat: descreva a alteração"
git push
```

## 13. Atualizar o projeto local

```bash
git pull
```

Em projetos compartilhados, use o pull para trazer e integrar alterações do remoto antes de continuar o trabalho.

## 14. Clonar um projeto existente

Quando o repositório já está no GitHub:

```bash
git clone https://github.com/USUARIO/REPOSITORIO.git
cd REPOSITORIO
```

O clone cria uma cópia local e normalmente já configura `origin`.

## 15. Trabalhar com branch

Crie e entre em uma nova branch:

```bash
git switch -c feature/login
```

Faça alterações e depois:

```bash
git add .
git commit -m "feat: cria tela de login"
git push -u origin feature/login
```

Depois, no GitHub, a equipe pode revisar a branch por meio de um Pull Request.

## 16. Criar `.gitignore`

Exemplo:

```gitignore
node_modules/
target/
build/
.env
*.log
.idea/
```

Nunca envie senhas, tokens, chaves de API ou outros segredos para o repositório.

## 17. Comandos essenciais

| Comando | Para que serve |
|---|---|
| `git status` | Ver o estado do repositório |
| `git add .` | Preparar alterações |
| `git commit -m "..."` | Registrar um ponto no histórico |
| `git log --oneline` | Consultar commits |
| `git diff` | Ver alterações ainda não preparadas |
| `git remote -v` | Conferir repositórios remotos |
| `git push` | Enviar commits |
| `git pull` | Trazer e integrar alterações remotas |
| `git clone URL` | Copiar um repositório existente |
| `git switch -c branch` | Criar e entrar em uma nova branch |
| `git branch` | Listar branches locais |

## 18. Exercício final

Faça sozinho, sem copiar os comandos da seção anterior:

1. configure nome e e-mail;
2. crie uma pasta chamada `atividade-git`;
3. crie um `README.md`;
4. inicialize o Git com branch `main`;
5. consulte o status;
6. prepare o README;
7. crie o primeiro commit;
8. crie um repositório vazio no GitHub;
9. configure `origin`;
10. confira o remote;
11. envie a `main`;
12. crie a branch `feature/apresentacao`;
13. altere o README;
14. faça novo commit;
15. envie a nova branch ao GitHub.

## Próximos assuntos

Depois de dominar este guia, estude:

**merge → Pull Request → conflitos → tags → rebase → fork → colaboração em equipe**.

## Referências

- Documentação oficial do Git: https://git-scm.com/doc
- GitHub Docs — Git: https://docs.github.com/pt/get-started/using-git
- GitHub Docs — repositórios remotos: https://docs.github.com/pt/get-started/git-basics/managing-remote-repositories
