# GHI — GitHub Issues TUI

Interface em modo texto (TUI) para gerenciar GitHub Issues direto do terminal.
O objetivo é permitir listar, visualizar, criar, editar e fechar issues sem sair do terminal.

O sistema usa e precisa encontrar os seguintes comandos:
- gh (GitHub CLI)
- fzf
- jq
- bat
- um editor de texto (hx, vim, nano, etc.)

## Ubuntu / Debian

```bash
sudo apt install gh fzf jq bat
```

---

# Login no GitHub

Depois de instalar o gh:

```bash
gh auth login
```

---

# Instalação do script

Salve o script como:

```bash
~/bin/ghi
chmod +x ~/bin/ghi
```

Ou dentro do repositório:

```bash
chmod +x ghi
```

---

# Uso

## Abrir o menu TUI

```bash
ghi
```

## Usar com outro repositório

```bash
ghi -R owner/repo
```

Exemplo:

```bash
ghi -R cli/cli
```

---

# Atalhos

| Tecla      | Nome   | Ação                              |
| ---------- | ------ | --------------------------------- |
| Enter      | _      | Mostrar/ocultar preview           |
| Ctrl+Alt+V | View   | Abrir no editor para visualização |
| Ctrl+Alt+E | Edit   | Abrir no editor para edição       |
| Ctrl+Alt+N | New    | Abrir no editor para criação      |
| Ctrl+Alt+C | Close  | Fechar uma issue aberta           |
| Ctrl+Alt+O | Open   | Abrir uma issue fechada           |
| Ctrl+Alt+W | Web    | Abrir no navegador                |
| Ctrl+Alt+U | Update | Atualizar lista                   |

---

# Edição de Issues

Ao editar uma issue, abrirá um arquivo temporário com a estrutura:

```
# [TITLE] Título da issue

## Body
Texto da issue

## Labels
[x] bug
[ ] enhancement
[x] documentation

## End
```

- Marque `[x]` para adicionar label
- Desmarque para remover
- Se nada for alterado, a issue não é modificada
- Se o editor fechar com erro, o arquivo fica salvo em `/tmp`

---

# Cache

O script mantém cache local em:

```
/tmp/ghi/
```

O cache dura 5 minutos para evitar muitas chamadas à API do GitHub.

---

# Editor

O script usa precisa de um editor que use o terminal para editar as issues. Ele tenta usar o editor definido nas variáveis de ambiente `VISUAL` ou `EDITOR`, ou o editor padrão `hx`.

Opções: `hx`, `vim`, `nano`, `emacs -nw`, etc.

## Configuração do editor
O editor é determinado pela variável de ambiente `EDITOR` ou `VISUAL`. Se nenhuma delas estiver definida, o script usa `hx` como padrão.
Para usar um editor diferente, defina a variável de ambiente antes de rodar o script. Adicione a seguinte linha ao seu arquivo de configuração do shell (`~/.bashrc`, `~/.zshrc`, etc.):

```bash
export EDITOR=vim
```
---

# Preview

O preview usa `bat` para renderizar Markdown com cor dentro do fzf.

Parâmetros usados:

```
batcat --language=markdown --color=always --paging=never
```

---

# Filosofia

Fluxo de uso:

```
ghi → filtra → preview → edita → continua trabalhando
```

Sem browser, sem mouse, direto no terminal.
