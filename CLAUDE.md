# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

GitHub Pages static site at gutoceolin.github.io — acervo de resumos jurídicos para o Curso de Direito da UFN (Guto Ceolin). Abrange múltiplos semestres e disciplinas. Pure HTML/CSS/vanilla JS, sem build tooling, package manager ou dependências.

## Development

**Sem build step.** Editar HTML diretamente e abrir no browser. GitHub Pages publica automaticamente a partir do branch `main`.

Preview local:
```
python -m http.server
```

Git config local definido: `user.email = gutoceolin@terra.com.br`, `user.name = Guto Ceolin`.

## File Structure

```
index.html                  ← hub principal (filtros, grid, semestres)
BRUNAO/
├── civil/
│   ├── prova-1.html        ← Pessoa Natural, Nascituro e Capacidade
│   ├── prova-2.html        ← Morte, Ausência, PJ e Domicílio (completo + quiz)
│   └── prova-3.html        ← Negócios Jurídicos e Vícios (stub)
├── const/
│   ├── prova-1.html        ← Poder Constituinte e Supremacia (completo + quiz)
│   ├── prova-2.html        ← Eficácia das Normas (stub)
│   └── prova-3.html        ← Controle de Constitucionalidade (stub)
├── proc/prova-{1,2,3}.html ← stubs
├── penal/prova-{1,2,3}.html← stubs
└── eca/prova-{1,2,3}.html  ← stubs
```

**Back-links** em todos os arquivos BRUNAO apontam para `../../index.html` (dois níveis acima).

## Architecture

### index.html
- **Hero**: card com faixa de 5 cores de disciplina, título serif, stats (15/5), nomes das disciplinas
- **Semestres**: tabs 1–6 (apenas 3º tem conteúdo); clicar em outro semestre oculta `.sem-3-only` via classe `sem-other-active` no `<html>`
- **Filtros sticky**: pills por disciplina + busca; `data-disc` em cada card e botão
- **Grid**: 3 colunas, gap 1rem; cards ordenados por matéria (Civil → Const → Proc → Penal → ECA), 3 por disciplina = Prova 1/2/3
- **Quiz score badge**: `loadQuizScores()` lê localStorage ao carregar, injeta `.qsb` com barra de progresso animada antes do `.rcard-meta`

### Páginas completas (prova-2 civil, prova-1 civil, prova-1 const)
- **Header**: back link (pill button), eyebrow, título, banca pill, barra de progresso do quiz, busca
- **Nav de módulos** (`.nb`): pills arredondadas, `onclick="swM(id, this)"`
- **Módulo** = `.mhd` (header colorido) + `.mbody` (subtabs + painéis `.sp`)
- **Quiz**: 28 questões (civil-2) com dots de progresso, feedback imediato, barra de progresso, `showR()` salva score no `localStorage`
- **Footer**: texto da disciplina + "← Voltar ao Hub" → `../../index.html`

### Stub pages
- Mostram WIP card com ícone CSS (não emoji), lista de tópicos a cobrir
- Mesma estrutura visual do hub (back link pill, footer)

## Design System

**Estética**: Clean Dashboard — sombras suaves, `border-radius:14px` nos cards, pills arredondadas (`border-radius:100px`) para botões e filtros, Cormorant Garamond para display, Outfit para UI.

**Dark/Light mode**:
- Toggle fixo `bottom:1.75rem right:1.75rem` em todas as páginas
- Anti-flash script inline no `<head>` antes do `<meta name="viewport">`
- Persistência via `localStorage('theme')`, fallback `prefers-color-scheme`
- Variáveis sobrescritas via `[data-theme=light]` no `<html>`

**Variáveis de cor** — definidas em `:root` de cada arquivo:

| Variável | Dark | Light (index) | Uso |
|---|---|---|---|
| `--bg` | `#111118` | `#f0eef7` | Fundo da página |
| `--surface` | `#1c1c26` | `#ffffff` | Cards |
| `--civil` | `#e06e8c` | `#c05070` | Direito Civil |
| `--const` | `#7b8fe8` | `#5868d0` | Teoria da Const. |
| `--proc` | `#5cb8e0` | `#2898c0` | Processual |
| `--penal` | `#e07a5c` | `#c06040` | Penal |
| `--eca` | `#5cc98a` | `#30a860` | ECA |
| `--gold` | `#d4a843` | `#987020` | Acento/quiz |

**Atenção**: páginas BRUNAO usam variáveis de módulo próprias (`--morte`, `--aus`, `--pj`, `--dom`) — **não** `--civil/--const/--eca` etc. Usar valores hex absolutos quando precisar de cores de estado (ex: dots do quiz).

**Sombras** (definidas como variáveis):
- `--sh-sm`: sombra padrão dos cards
- `--sh`: hover
- `--sh-hover`: hover elevado

**Fontes** (Google Fonts, carregadas em cada arquivo):
- `Cormorant Garamond` — títulos, display, eyebrow italic
- `Outfit` — body, UI labels, botões
- `JetBrains Mono` — dados numéricos, artigos de lei, badges de código

## Adding New Content

Para adicionar uma nova prova a uma matéria:

1. Criar `BRUNAO/{materia}/prova-N.html` copiando de um stub existente (ex: `BRUNAO/civil/prova-3.html`)
2. Para um resumo completo com quiz, copiar de `BRUNAO/civil/prova-2.html`
3. Adicionar card no grid do `index.html` com `href="BRUNAO/{materia}/prova-N.html"`
4. Back-links dentro do arquivo: `../../index.html`

## Quiz System

Nas páginas completas, o quiz:
- **Salva** score em `localStorage` na chave `quiz_{materia}_{prova-N}` (derivada de `location.pathname.split('/').slice(-2)`)
- No `index.html`, `loadQuizScores()` lê com chave derivada de `href.replace('BRUNAO/','').replace('/','_').replace('.html','')`

Para o **visual dos dots** (`.qdot.ok/.err`), usar hex absolutos — as variáveis `--eca`/`--civil` não existem nas páginas BRUNAO:
```css
.qdot.ok  { background: #5cc98a }  /* verde */
.qdot.err { background: #e06e8c }  /* rosa */
[data-theme=light] .qdot.ok  { background: #289050 }
[data-theme=light] .ecdot.err { background: #c04070 }
```

## Known Pitfalls

- **PowerShell regex replacement** com `"${1}..."` (aspas duplas) expande `${1}` como variável PS vazia em vez de backreference — usar `'$1'` ou construção com `+` para concatenar o replacement.
- **CSS no BRUNAO** usa `rgba(255,255,255,.07)` para `--border` no dark — quase invisível. Evitar para elementos que precisam de contraste real (dots, separadores visíveis).
- Nunca usar `--eca`, `--civil` etc. dentro de `BRUNAO/*.html` — essas variáveis só existem no `index.html`.

## Language

Todo conteúdo em Português Brasileiro (`lang="pt-BR"`). UI, comentários e commits em PT-BR.
