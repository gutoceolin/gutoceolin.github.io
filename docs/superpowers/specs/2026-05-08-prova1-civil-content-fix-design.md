# Design: Correção de Conteúdo — Civil Prova 1

**Data:** 2026-05-08  
**Arquivo alvo:** `BRUNAO/civil/prova-1.html`

## Problema

A página atual cobre conteúdo incorreto para a Prova 1. Inclui morte presumida e comoriência (arts. 6–8 CC) que pertencem à Prova 2, e não inclui Historicidade do Direito Civil.

## Conteúdo correto da Prova 1

Arts. 1–5 CC · Nascituro · Emancipação · Direitos da Personalidade · Historicidade do Direito Civil

## Estrutura de módulos (resultado final)

| # | Módulo | Cor CSS | Status |
|---|---|---|---|
| 1 | Historicidade | `--hist` (roxo novo) | Novo |
| 2 | Pessoa Natural (Arts. 1–5) | `--nat` (rosa, ex-`--morte`) | Remove subtab Extinção |
| 3 | Nascituro | `--nas` (azul, ex-`--aus`) | Sem mudança |
| 4 | Emancipação | `--eman` (dourado, ex-`--pj`) | Sem mudança |
| 5 | Direitos da Personalidade | `--dir` (verde, ex-`--dom`) | Promovido de subtab |
| 6 | Quiz | branco | Remove morte/comoriência, adiciona historicidade |

## Módulo 1 — Historicidade (novo)

Três subtabs:
- **Origens:** Direito Romano, Corpus Juris Civilis, Justiniano, recepção europeia
- **Brasil Colonial/Imperial:** Ordenações Filipinas, influência portuguesa, CC 1916 (Clóvis Beviláqua)
- **CC 2002:** Princípios da eticidade, socialidade e operabilidade; mudanças em relação ao CC 1916

## Módulo 2 — Pessoa Natural (alterado)

Remove subtab "Extinção" (morte real, morte presumida, comoriência — arts. 6–8).  
Remove subtab "Direitos da Personalidade" (vira módulo próprio).  
Mantém: "Conceito" e "Início da Personalidade".

## Módulo 5 — Direitos da Personalidade (promovido)

Três subtabs:
- **Conceito e características:** absolutos, intransmissíveis, irrenunciáveis, imprescritíveis (art. 11)
- **Tipos:** nome (arts. 16–19), imagem (art. 20), vida privada (art. 21), integridade física (art. 13)
- **Proteção:** art. 12 — cessação de ameaça + indenização; tutela inibitória

## Quiz

Remove ~3 questões sobre morte presumida e comoriência.  
Adiciona ~3 questões sobre Historicidade (princípios CC 2002, CC 1916 vs CC 2002, Ordenações).  
Total: 20 questões.

## CSS

Renomear variáveis de cor para refletir o conteúdo de Prova 1:
- `--morte` → `--nat` (Pessoa Natural)
- `--aus` → `--nas` (Nascituro)
- `--pj` → `--eman` (Emancipação)
- `--dom` → `--dir` (Direitos da Personalidade)
- Adicionar `--hist` (roxo `#9b7fe8`) para Historicidade
