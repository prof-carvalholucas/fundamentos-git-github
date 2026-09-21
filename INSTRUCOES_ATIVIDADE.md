# Atividade Prática — Git e GitHub

## Objetivo

Nesta atividade você vai praticar o fluxo básico do Git e GitHub, desde a configuração inicial até o uso de **branch** e **merge**.

Ao final, você deverá ter um repositório publicado no GitHub com vários commits e pelo menos uma branch criada e integrada à `main`.

---

## Antes de começar

Você precisa ter:

- Git instalado no computador;
- uma conta no GitHub;
- terminal, Git Bash ou terminal do VS Code;
- um editor de código, como VS Code.

> **Importante:** execute uma etapa por vez. Use `git status` sempre que tiver dúvida sobre o estado do repositório.

---

## 1. Configurar nome e e-mail

> **Faça esta etapa somente se você ainda não configurou seu nome e e-mail no Git.**  
> Se já estiver configurado corretamente, apenas confira os dados e siga para a próxima etapa.

Primeiro, verifique sua configuração atual:

```bash
$ git config --global user.name
Seu Nome

$ git config --global user.email
seuemail@exemplo.com
```

Se os dados **não aparecerem** ou estiverem incorretos, configure:

```bash
$ git config --global user.name "Seu Nome"
$ git config --global user.email "seuemail@exemplo.com"
```

Confira novamente:

```bash
$ git config --global user.name
Seu Nome

$ git config --global user.email
seuemail@exemplo.com
```

**Checkpoint:** seu nome e e-mail devem aparecer corretamente no terminal.

---

## 2. Criar o projeto local

```bash
$ mkdir atividade-git-seu-nome
$ cd atividade-git-seu-nome
$ git init -b main
```

Crie um arquivo chamado `README.md` e coloque:

```markdown
# Minha Atividade Git

Aluno: Seu Nome

Projeto utilizado para estudar Git e GitHub.
```

Confira:

```bash
$ git status
```

**Checkpoint:** o `README.md` deve aparecer como arquivo ainda não rastreado.

---

## 3. Fazer o primeiro commit

Adicione o arquivo à área de preparação:

```bash
$ git add README.md
```

Confira:

```bash
$ git status
```

Agora registre a alteração:

```bash
$ git commit -m "Cria README inicial"
```

Confira o histórico:

```bash
$ git log --oneline
```

**Checkpoint:** deve existir pelo menos 1 commit.

---

## 4. Fazer uma nova alteração

Crie um arquivo chamado `aluno.txt` com seu nome e curso.

Depois execute:

```bash
$ git status
$ git add aluno.txt
$ git commit -m "Adiciona dados do aluno"
```

Confira:

```bash
$ git log --oneline
```

**Checkpoint:** seu projeto deve possuir pelo menos 2 commits.

---

## 5. Criar o repositório no GitHub

No GitHub, crie um repositório chamado:

```text
atividade-git-seu-nome
```

Para este exercício, crie o repositório remoto **sem adicionar README**, pois o projeto local já possui um.

Copie a URL do repositório e conecte o projeto local:

```bash
$ git remote add origin URL_DO_SEU_REPOSITORIO
```

Confira:

```bash
$ git remote -v
```

> `origin` é o nome convencional usado para identificar o repositório remoto principal.

**Checkpoint:** a URL do seu repositório deve aparecer associada ao `origin`.

---

## 6. Enviar o projeto para o GitHub

```bash
$ git push -u origin main
```

Depois, abra o GitHub e atualize a página do repositório.

**Checkpoint:** os arquivos `README.md` e `aluno.txt` devem estar no GitHub.

---

## 7. Criar uma branch

Crie uma branch para desenvolver uma nova funcionalidade sem alterar diretamente a `main`:

```bash
$ git switch -c feature/apresentacao
```

Confira:

```bash
$ git branch
```

A branch atual aparecerá marcada com `*`.

Na branch `feature/apresentacao`, crie o arquivo `apresentacao.txt` e escreva uma pequena apresentação sobre você.

Depois:

```bash
$ git add apresentacao.txt
$ git commit -m "Adiciona apresentação do aluno"
$ git push -u origin feature/apresentacao
```

**Checkpoint:** a branch `feature/apresentacao` deve existir localmente e no GitHub.

---

## 8. Fazer o merge

Volte para a branch principal:

```bash
$ git switch main
```

Atualize a `main`:

```bash
$ git pull origin main
```

Integre a branch criada:

```bash
$ git merge feature/apresentacao
```

Envie o resultado:

```bash
$ git push origin main
```

**Checkpoint:** o arquivo `apresentacao.txt` deve aparecer na `main` do GitHub.

---

## 9. Visualizar o histórico completo

Execute:

```bash
$ git log --oneline --graph --decorate --all
```

Observe os commits, branches e a integração realizada.

---

## 10. Testar o clone

Saia da pasta atual e faça uma nova cópia do projeto:

```bash
$ cd ..
$ git clone URL_DO_SEU_REPOSITORIO atividade-git-clone
$ cd atividade-git-clone
```

Confira:

```bash
$ git status
$ git log --oneline
$ git remote -v
```

**Checkpoint:** a nova pasta deve possuir os arquivos e o histórico do projeto.

---

# Fluxo que você precisa memorizar

```text
ALTERAR
   ↓
git status
   ↓
git add
   ↓
git commit
   ↓
git push
```

Para trabalhar com uma nova funcionalidade:

```text
main
  ↓
criar branch
  ↓
trabalhar
  ↓
commit
  ↓
push
  ↓
merge
  ↓
main
```

---

# Comandos essenciais

| Comando | Para que serve |
|---|---|
| `git status` | Ver o estado dos arquivos |
| `git add .` | Preparar alterações para commit |
| `git commit -m "mensagem"` | Registrar uma versão |
| `git log --oneline` | Ver o histórico |
| `git diff` | Ver alterações ainda não preparadas |
| `git branch` | Listar branches |
| `git switch nome` | Trocar de branch |
| `git switch -c nome` | Criar e entrar em uma branch |
| `git merge nome` | Integrar outra branch à atual |
| `git remote -v` | Ver repositórios remotos |
| `git push` | Enviar commits ao remoto |
| `git pull` | Buscar e integrar mudanças do remoto |
| `git clone URL` | Baixar uma cópia completa do repositório |

---
