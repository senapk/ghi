# ghi — GitHub Issues no terminal com editor

`ghi` é uma ferramenta de terminal para gerenciar GitHub Issues usando:

* `gh` (GitHub CLI)
* `fzf` (interface interativa)
* seu editor (`helix`, `vim`, `nano`, etc.)

A edição e criação de issues é feita via **arquivo Markdown temporário**, permitindo editar título, descrição e labels de forma muito mais confortável.

---

# Funcionalidades

| Função                 | Descrição                                |
| ---------------------- | ---------------------------------------- |
| Listar issues          | Lista interativa com fzf                 |
| Visualizar             | Preview da issue                         |
| Editar                 | Edita título, body e labels via Markdown |
| Criar                  | Cria issue via Markdown                  |
| Labels                 | Comentar/descomentar                     |
| Abrir no browser       | Atalho                                   |
| Fechar issue           | Atalho                                   |
| Reabrir issue          | Atalho                                   |
| Cancelar edição        | Sair sem salvar                          |
| Funcionar fora do repo | Suporte a `-R owner/repo`                |

---

# Instalação

## Dependências

Você precisa ter instalado:

```bash
gh
jq
fzf
sha1sum
```

Editor (um deles):

```bash
helix
vim
nano
```

## Instalar o script

```bash
chmod +x ghi
mv ghi ~/.local/bin/ghi
```

---

# Uso

## Usando no repositório atual

```bash
ghi
```

## Usando um repositório específico

```bash
ghi -R owner/repo
```

Exemplo:

```bash
ghi -R senapk/tko
ghi -R cli/cli
```

---

# Comandos

| Comando       | Ação            |
| ------------- | --------------- |
| `ghi`         | Menu interativo |
| `ghi list`    | Lista issues    |
| `ghi view 10` | Mostra issue    |
| `ghi edit 10` | Edita issue     |
| `ghi new`     | Nova issue      |

---

# Atalhos no menu (fzf)

| Tecla  | Ação               |
| ------ | ------------------ |
| Enter  | Visualizar         |
| Ctrl+E | Editar             |
| Ctrl+N | Nova issue         |
| Ctrl+O | Abrir no navegador |
| Ctrl+C | Fechar issue       |
| Ctrl+R | Reabrir issue      |

---

# Como funciona a edição

Quando você edita ou cria uma issue, abre um arquivo Markdown assim:

```md
# [TITLE] Título da issue

## Body
Descrição da issue

## Labels (ativas primeiro, comente/descomente para alterar)
bug
enhancement
# help wanted
# documentation
```

## Labels

* Labels **sem `#`** → serão aplicadas
* Labels **com `#`** → serão removidas
* Labels novas podem ser adicionadas escrevendo o nome

---

# Cancelar edição

Para cancelar:

* Saia do editor **sem salvar**

O script detecta que o arquivo não foi modificado e cancela automaticamente.

---

# Ideia do projeto

O `ghi` segue o conceito de:

> **Editor como interface** (editor-as-interface)

Você não edita issues em formulários — você edita um arquivo Markdown.

Ferramentas que usam essa ideia:

* `git commit`
* `crontab -e`
* `kubectl edit`
* `git rebase -i`

---

# Possíveis melhorias futuras

* Filtrar por label
* Filtrar open/closed
* Suporte a Pull Requests
* Assign usuário
* Milestones
* Projetos
* Cache local
* Dashboard
* TUI completa (Textual / curses)

---

# Licença

Livre para uso e modificação.
