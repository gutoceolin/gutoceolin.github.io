# Civil Prova 1 — Correção de Conteúdo

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Corrigir o conteúdo de `BRUNAO/civil/prova-1.html` para refletir o conteúdo real da Prova 1: Arts. 1–5 CC, Nascituro, Emancipação, Direitos da Personalidade e Historicidade.

**Architecture:** Edições diretas em único arquivo HTML estático. Sem build step. Renomear variáveis CSS semânticas, remover conteúdo de morte/comoriência, adicionar módulo Historicidade, promover Direitos da Personalidade a módulo próprio, atualizar quiz.

**Tech Stack:** HTML/CSS/JS vanilla. Sem dependências. Preview via `python -m http.server`.

---

### Task 1: Corrigir variável CSS proibida e renomear variáveis de módulo

**Files:**
- Modify: `BRUNAO/civil/prova-1.html`

Contexto: a página usa variáveis `--morte/--aus/--pj/--dom` que são nomes semânticos de Prova 2. Também usa `var(--eca)` na linha 141, variável que só existe em `index.html` — bug visual no botão "Próxima". Renomear para `--nat/--nas/--eman/--dir` + adicionar `--hist`.

- [ ] **Step 1: Corrigir var(--eca) → hex absoluto**

No arquivo `BRUNAO/civil/prova-1.html`, linha 141, substituir:
```
.qbn-next{background:var(--eca);color:#fff;
```
por:
```
.qbn-next{background:#5cc98a;color:#fff;
```

- [ ] **Step 2: Renomear --morte → --nat em todo o arquivo**

Substituir todas as ocorrências (replace_all):
- `--morte:` → `--nat:`
- `--morte-dim:` → `--nat-dim:`
- `--morte-mid:` → `--nat-mid:`
- `var(--morte)` → `var(--nat)`
- `var(--morte-dim)` → `var(--nat-dim)`
- `var(--morte-mid)` → `var(--nat-mid)`
- `data-m=morte` → `data-m=nat`
- `data-c=morte` → `data-c=nat`
- `data-m="morte"` → `data-m="nat"`
- `data-c="morte"` → `data-c="nat"`
- `switchMod('morte'` → `switchMod('nat'`
- `mod-morte` → `mod-nat`
- `[data-m=morte]` → `[data-m=nat]`
- `[data-c=morte]` → `[data-c=nat]`

- [ ] **Step 3: Renomear --aus → --nas**

Substituir todas as ocorrências (replace_all):
- `--aus:` → `--nas:`
- `--aus-dim:` → `--nas-dim:`
- `--aus-mid:` → `--nas-mid:`
- `var(--aus)` → `var(--nas)`
- `var(--aus-dim)` → `var(--nas-dim)`
- `var(--aus-mid)` → `var(--nas-mid)`
- `data-m=aus` → `data-m=nas`
- `data-c=aus` → `data-c=nas`
- `data-m="aus"` → `data-m="nas"`
- `data-c="aus"` → `data-c="nas"`
- `switchMod('aus'` → `switchMod('nas'`
- `mod-aus` → `mod-nas`
- `[data-m=aus]` → `[data-m=nas]`
- `[data-c=aus]` → `[data-c=nas]`

- [ ] **Step 4: Renomear --pj → --dir (repurposing: Capacidade Civil dissolve; sua cor/slot vira Direitos da Personalidade)**

Substituir todas as ocorrências (replace_all):
- `--pj:` → `--dir:`
- `--pj-dim:` → `--dir-dim:`
- `--pj-mid:` → `--dir-mid:`
- `var(--pj)` → `var(--dir)`
- `var(--pj-dim)` → `var(--dir-dim)`
- `var(--pj-mid)` → `var(--dir-mid)`
- `data-m=pj` → `data-m=dir`
- `data-c=pj` → `data-c=dir`
- `data-m="pj"` → `data-m="dir"`
- `data-c="pj"` → `data-c="dir"`
- `switchMod('pj'` → `switchMod('dir'`
- `mod-pj` → `mod-dir`
- `[data-m=pj]` → `[data-m=dir]`
- `[data-c=pj]` → `[data-c=dir]`

- [ ] **Step 5: Renomear --dom → --eman (Emancipação)**

Substituir todas as ocorrências (replace_all):
- `--dom:` → `--eman:`
- `--dom-dim:` → `--eman-dim:`
- `--dom-mid:` → `--eman-mid:`
- `var(--dom)` → `var(--eman)`
- `var(--dom-dim)` → `var(--eman-dim)`
- `var(--dom-mid)` → `var(--eman-mid)`
- `data-m=dom` → `data-m=eman`
- `data-c=dom` → `data-c=eman`
- `data-m="dom"` → `data-m="eman"`
- `data-c="dom"` → `data-c="eman"`
- `switchMod('dom'` → `switchMod('eman'`
- `mod-dom` → `mod-eman`
- `[data-m=dom]` → `[data-m=eman]`
- `[data-c=dom]` → `[data-c=eman]`

- [ ] **Step 6: Adicionar variável --hist no bloco :root**

No bloco `:root{`, após a linha `--dir:#5cc98a; --dir-dim:...; --dir-mid:...;`, adicionar:
```css
--hist:#9b7fe8; --hist-dim:rgba(155,127,232,.10); --hist-mid:rgba(155,127,232,.22);
```

No bloco `[data-theme=light]{` (ambas as ocorrências), adicionar após a linha de --eca ou ao final das variáveis de módulo:
```css
--hist:#7b5fc8; --hist-dim:rgba(123,95,200,.10); --hist-mid:rgba(123,95,200,.18);
```

- [ ] **Step 7: Adicionar CSS para .ch (card de Historicidade) e estilos do módulo --hist**

Logo após `.cd .ct{color:var(--dir)}.cd .ct::before{background:var(--dir)}`, adicionar:
```css
.ch .ct{color:var(--hist)}.ch .ct::before{background:var(--hist)}
```

Logo após `.nb[data-m=dir].active{border-color:var(--dir);background:var(--dir-dim)}`, adicionar:
```css
.nb[data-m=hist].active{border-color:var(--hist);background:var(--hist-dim)}
```

Logo após `.mhd[data-c=dir]{background:var(--dir-dim);border-color:rgba(92,201,138,.28)}`, adicionar:
```css
.mhd[data-c=hist]{background:var(--hist-dim);border-color:rgba(155,127,232,.28)}
```

Logo após `.mi[data-c=dir]{background:var(--dir-mid)}`, adicionar:
```css
.mi[data-c=hist]{background:var(--hist-mid)}
```

Logo após `.stab.active[data-c=dir]{border-bottom-color:var(--dir)}`, adicionar:
```css
.stab.active[data-c=hist]{border-bottom-color:var(--hist)}
```

- [ ] **Step 8: Verificar**

```bash
grep -n "var(--eca)\|var(--morte)\|var(--aus)\|var(--pj)\|var(--dom)" BRUNAO/civil/prova-1.html
```
Esperado: sem resultado (zero ocorrências).

```bash
grep -n "\-\-hist" BRUNAO/civil/prova-1.html | head -10
```
Esperado: linhas com a variável --hist definida e usada.

---

### Task 2: Atualizar nav e cabeçalho da página

**Files:**
- Modify: `BRUNAO/civil/prova-1.html`

- [ ] **Step 1: Atualizar subtítulo do header**

Substituir:
```html
<h1 class="htitle">Pessoa Natural<br><em>Nascituro · Capacidade · Emancipação</em></h1>
<div class="hsub">Arts. 1–21 CC &middot; Estatuto da Pessoa com Deficiência (Lei 13.146/2015) &middot; Banca UFN</div>
```
por:
```html
<h1 class="htitle">Direito Civil I<br><em>Historicidade · Arts. 1–5 · Direitos da Personalidade</em></h1>
<div class="hsub">Arts. 1–5 CC &middot; Arts. 11–21 CC &middot; Nascituro &middot; Emancipação &middot; Historicidade &middot; Banca UFN</div>
```

- [ ] **Step 2: Atualizar nav pills**

Substituir o bloco `<nav class="mnav">` inteiro por:
```html
<nav class="mnav">
  <button class="nb active" data-m="hist" onclick="switchMod('hist',this)"><span class="d"></span>Historicidade</button>
  <button class="nb" data-m="nat" onclick="switchMod('nat',this)"><span class="d"></span>Pessoa Natural</button>
  <button class="nb" data-m="nas" onclick="switchMod('nas',this)"><span class="d"></span>Nascituro</button>
  <button class="nb" data-m="eman" onclick="switchMod('eman',this)"><span class="d"></span>Emancipação</button>
  <button class="nb" data-m="dir" onclick="switchMod('dir',this)"><span class="d"></span>Direitos da Personalidade</button>
  <button class="nb" data-m="quiz" onclick="switchMod('quiz',this)"><span class="d"></span>Quiz (20 q.)</button>
</nav>
```

- [ ] **Step 3: Verificar**

```bash
grep -n 'data-m=' BRUNAO/civil/prova-1.html
```
Esperado: hist, nat, nas, eman, dir, quiz — nenhum morte/aus/pj/dom.

---

### Task 3: Corrigir módulo Pessoa Natural (remover subtabs Extinção e Direitos da Personalidade)

**Files:**
- Modify: `BRUNAO/civil/prova-1.html`

Contexto: o módulo Pessoa Natural (`id="mod-nat"` após renomeação) tem 4 subtabs: Conceito, Início da Personalidade, Direitos da Personalidade, Extinção. As subtabs "Direitos da Personalidade" e "Extinção" precisam ser removidas — a primeira vira módulo próprio, a segunda (morte/comoriência) não pertence à Prova 1.

- [ ] **Step 1: Remover botões de subtab desnecessários**

No bloco `.stabs` do módulo Pessoa Natural, substituir:
```html
      <button class="stab active" data-c="nat" onclick="switchTab(this,'m1t1')">Conceito</button>
      <button class="stab" data-c="nat" onclick="switchTab(this,'m1t2')">Início da Personalidade</button>
      <button class="stab" data-c="nat" onclick="switchTab(this,'m1t3')">Direitos da Personalidade</button>
      <button class="stab" data-c="nat" onclick="switchTab(this,'m1t4')">Extinção</button>
```
por:
```html
      <button class="stab active" data-c="nat" onclick="switchTab(this,'m1t1')">Conceito</button>
      <button class="stab" data-c="nat" onclick="switchTab(this,'m1t2')">Início da Personalidade</button>
```

- [ ] **Step 2: Remover painel m1t3 (Direitos da Personalidade)**

Remover o bloco inteiro `<div class="sp" id="m1t3">...</div>` que contém o conteúdo de Direitos da Personalidade (vai do `<div class="sp" id="m1t3">` até o `</div>` de fechamento do painel, antes de `<div class="sp" id="m1t4">`).

- [ ] **Step 3: Remover painel m1t4 (Extinção/Morte)**

Remover o bloco inteiro `<div class="sp" id="m1t4">...</div>` que contém morte real, morte presumida e comoriência.

- [ ] **Step 4: Verificar**

```bash
grep -n "m1t3\|m1t4\|Extinção\|comoriência\|Comoriência\|morte presumida" BRUNAO/civil/prova-1.html
```
Esperado: sem resultado.

---

### Task 4: Adicionar módulo Historicidade

**Files:**
- Modify: `BRUNAO/civil/prova-1.html`

Inserir antes do comentário `<!-- ═══ MÓDULO 1: PESSOA NATURAL ═══ -->` (que agora é mod-nat):

- [ ] **Step 1: Inserir HTML do módulo Historicidade**

```html
<!-- ═══ MÓDULO 0: HISTORICIDADE ═══ -->
<div class="mod active" id="mod-hist">
  <div class="mhd" data-c="hist">
    <div class="mi" data-c="hist">📜</div>
    <div>
      <div class="mnum">Módulo 01</div>
      <div class="mtitle">Historicidade</div>
      <div class="mdesc">Formação histórica do Direito Civil: Roma, Ordenações e os Códigos brasileiros.</div>
    </div>
  </div>
  <div class="mbody">
    <div class="stabs">
      <button class="stab active" data-c="hist" onclick="switchTab(this,'h1t1')">Origens Romanas</button>
      <button class="stab" data-c="hist" onclick="switchTab(this,'h1t2')">Brasil: CC 1916</button>
      <button class="stab" data-c="hist" onclick="switchTab(this,'h1t3')">CC 2002</button>
    </div>

    <div class="sp active" id="h1t1">
      <div class="sl">Direito Romano</div>
      <p>O Direito Civil tem suas raízes no <span class="hl">Direito Romano</span>, o mais influente sistema jurídico da Antiguidade. O termo <em>ius civile</em> designava originalmente o direito aplicável aos cidadãos romanos (<em>cives</em>), em oposição ao <em>ius gentium</em> (direito das gentes, aplicável a estrangeiros).</p>
      <div class="sl">Lei das XII Tábuas (451–450 a.C.)</div>
      <p>Primeiro código escrito de Roma, gravado em doze tábuas de bronze expostas no Fórum Romano. Marcou a transição do direito consuetudinário para o direito positivo escrito, garantindo previsibilidade e publicidade às normas.</p>
      <div class="sl">Corpus Juris Civilis (529–534 d.C.)</div>
      <p>Compilação ordenada pelo Imperador <span class="hl">Justiniano I</span>, composta por quatro partes:</p>
      <div class="g2">
        <div class="card ch"><div class="ct">Institutas</div><ul><li>Manual introdutório para estudantes</li><li>Baseado nas Institutas de Gaio</li><li>Dividido em: pessoas, coisas e ações</li></ul></div>
        <div class="card ch"><div class="ct">Digesto (Pandectas)</div><ul><li>Maior e mais importante parte</li><li>Compilação de excertos de jurisconsultos clássicos</li><li>50 livros de fragmentos doutrinários</li></ul></div>
        <div class="card ch"><div class="ct">Codex</div><ul><li>Compilação de constituições imperiais</li><li>Leis dos imperadores anteriores a Justiniano</li></ul></div>
        <div class="card ch"><div class="ct">Novelas</div><ul><li>Novas constituições do próprio Justiniano</li><li>Acrescentadas após as demais partes</li></ul></div>
      </div>
      <div class="co ci"><span class="co-ico">ℹ</span><div><strong>Influência:</strong> O Corpus Juris Civilis é a base do sistema da <em>civil law</em>, adotado pelo Brasil e pela maioria dos países da Europa continental e da América Latina. O sistema oposto é a <em>common law</em> (Inglaterra, EUA).</div></div>
    </div>

    <div class="sp" id="h1t2">
      <div class="sl">Brasil Colonial: Ordenações do Reino</div>
      <p>O Brasil foi colonizado sob a vigência das <span class="hl">Ordenações Portuguesas</span>, compilações do direito lusitano com forte influência romana e canônica. Três compilações se sucederam:</p>
      <div class="tw"><table>
        <thead><tr><th>Ordenação</th><th>Período</th><th>Observação</th></tr></thead>
        <tbody>
          <tr><td><strong>Afonsinas</strong></td><td>1446</td><td>Primeira grande compilação; vigorou antes do descobrimento do Brasil</td></tr>
          <tr><td><strong>Manuelinas</strong></td><td>1521</td><td>Substituíram as Afonsinas; vigoraram nos primeiros anos da colonização</td></tr>
          <tr><td><strong>Filipinas</strong></td><td>1603</td><td>Editadas sob Filipe II de Portugal; vigeram no Brasil até 1916</td></tr>
        </tbody>
      </table></div>
      <div class="co cw"><span class="co-ico">⚠</span><div><strong>Ordenações Filipinas:</strong> Vigoraram por mais de 300 anos no Brasil — do período colonial até a entrada em vigor do Código Civil de 1916 (1.º de janeiro de 1917).</div></div>
      <div class="sl">Projetos Precursores do CC 1916</div>
      <p><span class="hl">Teixeira de Freitas</span> elaborou a <em>Consolidação das Leis Civis</em> (1858) e o <em>Esboço</em> (1860–1865), projeto de código que influenciou os códigos civis argentino e uruguaio, mas não foi adotado no Brasil. Após outras tentativas frustradas (Nabuco de Araújo, Felício dos Santos), o projeto de <span class="hl">Clóvis Beviláqua</span> foi aprovado como <strong>Lei 3.071/1916</strong>, entrando em vigor em 1.º de janeiro de 1917.</p>
    </div>

    <div class="sp" id="h1t3">
      <div class="sl">Código Civil de 2002</div>
      <p>Os trabalhos para substituição do CC 1916 começaram em <span class="hl">1969</span>, com comissão presidida por <span class="hl">Miguel Reale</span>. Após décadas de tramitação, o projeto foi aprovado como <strong>Lei 10.406/2002</strong>, entrando em vigor em 11 de janeiro de 2003.</p>
      <div class="sl">Três Princípios Norteadores (Miguel Reale)</div>
      <div class="g3">
        <div class="card ch">
          <div class="ct">Eticidade</div>
          <p style="font-size:.82rem;color:#aeaab8;margin-top:.4rem;line-height:1.65">Prevalência dos valores éticos sobre o formalismo. Boa-fé objetiva como princípio central. Cláusulas gerais permitem ao juiz decidir com base em valores.</p>
        </div>
        <div class="card ch">
          <div class="ct">Socialidade</div>
          <p style="font-size:.82rem;color:#aeaab8;margin-top:.4rem;line-height:1.65">Superação do individualismo do CC 1916. Função social da propriedade e do contrato. O individual cede ao coletivo quando em conflito.</p>
        </div>
        <div class="card ch">
          <div class="ct">Operabilidade</div>
          <p style="font-size:.82rem;color:#aeaab8;margin-top:.4rem;line-height:1.65">Simplicidade e praticidade. Distinção clara entre prescrição e decadência. Linguagem acessível para facilitar a aplicação.</p>
        </div>
      </div>
      <div class="sl">Principais Mudanças em Relação ao CC 1916</div>
      <ul>
        <li>Unificação das obrigações civis e empresariais (Livro do Direito de Empresa)</li>
        <li>Eliminação de categorias discriminatórias (filho legítimo/ilegítimo)</li>
        <li>Reconhecimento da função social da propriedade e dos contratos</li>
        <li>Adoção de cláusulas gerais e conceitos indeterminados (boa-fé, função social)</li>
        <li>Reformulação completa do sistema de incapacidades (aprofundada pela Lei 13.146/2015)</li>
      </ul>
      <div class="co cs"><span class="co-ico">✓</span><div><strong>Para a prova:</strong> Saiba os três princípios de Miguel Reale (eticidade, socialidade, operabilidade), o nome do autor do CC 1916 (Clóvis Beviláqua), e que as Ordenações Filipinas vigoraram no Brasil até 1916.</div></div>
    </div>
  </div>
</div>
```

- [ ] **Step 2: Tornar módulo Historicidade ativo por padrão e desativar Pessoa Natural**

O primeiro `<div class="mod active"` agora deve ser o módulo hist. O módulo nat (Pessoa Natural) deve ter apenas `class="mod"` (sem active).

Verificar que `id="mod-hist"` tem `class="mod active"` e `id="mod-nat"` tem apenas `class="mod"`.

- [ ] **Step 3: Verificar**

```bash
grep -n "mod-hist\|h1t1\|h1t2\|h1t3\|Historicidade" BRUNAO/civil/prova-1.html | wc -l
```
Esperado: mais de 5 ocorrências.

---

### Task 5: Substituir módulo Capacidade Civil por Direitos da Personalidade

**Files:**
- Modify: `BRUNAO/civil/prova-1.html`

Contexto: após a Task 1, o antigo módulo Capacidade Civil passou a ter `id="mod-dir"` e `data-c="dir"`. Em vez de inserir um novo módulo (o que criaria IDs duplicados), substituímos o conteúdo interno desse módulo pelo conteúdo de Direitos da Personalidade.

- [ ] **Step 1: Substituir o HTML interno do módulo mod-dir**

Localizar o bloco que começa com `<!-- ═══ MÓDULO 3: CAPACIDADE CIVIL ═══ -->` (ou similar) e substituir o elemento `<div class="mod" id="mod-dir">...</div>` inteiro pelo seguinte:

```html
<!-- ═══ MÓDULO 5: DIREITOS DA PERSONALIDADE ═══ -->
<div class="mod" id="mod-dir">
  <div class="mhd" data-c="dir">
    <div class="mi" data-c="dir">🛡</div>
    <div>
      <div class="mnum">Módulo 05</div>
      <div class="mtitle">Direitos da Personalidade</div>
      <div class="mdesc">Atributos físicos, psíquicos e morais da pessoa. Arts. 11–21 CC.</div>
    </div>
  </div>
  <div class="mbody">
    <div class="stabs">
      <button class="stab active" data-c="dir" onclick="switchTab(this,'d1t1')">Conceito e Características</button>
      <button class="stab" data-c="dir" onclick="switchTab(this,'d1t2')">Tipos</button>
      <button class="stab" data-c="dir" onclick="switchTab(this,'d1t3')">Proteção</button>
    </div>

    <div class="sp active" id="d1t1">
      <div class="sl">Conceito</div>
      <p>Direitos da personalidade são aqueles que têm por objeto os <span class="hl">atributos físicos, psíquicos e morais da pessoa</span>, em sua projeção interior e social. São direitos inerentes à condição humana, reconhecidos tanto pelo Código Civil (arts. 11–21) quanto pela Constituição Federal.</p>
      <div class="co ci"><span class="co-ico">ℹ</span><div><strong>Art. 11 CC:</strong> Com exceção dos casos previstos em lei, os direitos da personalidade são intransmissíveis e irrenunciáveis, não podendo o seu exercício sofrer limitação voluntária.</div></div>
      <div class="sl">Características</div>
      <div class="g2">
        <div class="card cd">
          <div class="ct">Características Positivas</div>
          <ul>
            <li><strong>Absolutos:</strong> oponíveis erga omnes</li>
            <li><strong>Extrapatrimoniais:</strong> sem valor econômico direto</li>
            <li><strong>Vitalícios:</strong> duram toda a vida</li>
            <li><strong>Inatos:</strong> adquiridos com o nascimento</li>
          </ul>
        </div>
        <div class="card cd">
          <div class="ct">Características Negativas</div>
          <ul>
            <li><strong>Intransmissíveis:</strong> não se transferem a terceiros</li>
            <li><strong>Irrenunciáveis:</strong> não se pode abrir mão</li>
            <li><strong>Imprescritíveis:</strong> não se extinguem pelo não uso</li>
            <li><strong>Indisponíveis:</strong> em regra, não podem ser alienados</li>
          </ul>
        </div>
      </div>
      <div class="co cw"><span class="co-ico">⚠</span><div><strong>Exceção à irrenunciabilidade:</strong> A lei admite limitação voluntária em casos específicos (ex: doação de sangue, autorização de uso de imagem para fins publicitários). A limitação deve ser temporária e não pode abranger a totalidade dos direitos.</div></div>
    </div>

    <div class="sp" id="d1t2">
      <div class="sl">Principais Direitos da Personalidade no CC</div>
      <div class="tw"><table>
        <thead><tr><th>Direito</th><th>Artigo</th><th>Conteúdo</th></tr></thead>
        <tbody>
          <tr><td><strong>Integridade física</strong></td><td>Art. 13</td><td>Proibição de atos de disposição do próprio corpo que importem diminuição permanente da integridade ou contrariem os bons costumes</td></tr>
          <tr><td><strong>Integridade moral</strong></td><td>Arts. 16–19</td><td>Direito ao nome, pseudônimo e proteção contra uso indevido</td></tr>
          <tr><td><strong>Direito ao nome</strong></td><td>Art. 16</td><td>Nome é composto de prenome e sobrenome; é direito e dever da pessoa</td></tr>
          <tr><td><strong>Direito à imagem</strong></td><td>Art. 20</td><td>Proibição de divulgação de escritos, transmissão de palavra, publicação ou exposição da imagem sem autorização</td></tr>
          <tr><td><strong>Vida privada</strong></td><td>Art. 21</td><td>A vida privada da pessoa natural é inviolável; juiz pode adotar providências para impedir ou fazer cessar violação</td></tr>
        </tbody>
      </table></div>
      <div class="co cs"><span class="co-ico">✓</span><div><strong>Art. 14 CC:</strong> É válida, com objetivo científico, ou altruístico, a disposição gratuita do próprio corpo, no todo ou em parte, para depois da morte. Exemplo de limitação legal à indisponibilidade.</div></div>
    </div>

    <div class="sp" id="d1t3">
      <div class="sl">Proteção — Art. 12 CC</div>
      <p>O <span class="art">art. 12 CC</span> estabelece que pode-se exigir que <span class="hl">cesse a ameaça ou a lesão a direito da personalidade</span>, e reclamar perdas e danos, sem prejuízo de outras sanções previstas em lei.</p>
      <div class="g2">
        <div class="card cd"><div class="ct">Tutela Inibitória</div><ul><li>Impede a prática ou continuação da violação</li><li>Não exige dano já consumado</li><li>Pode ser concedida <em>inaudita altera parte</em></li><li>Ex: liminar para retirar conteúdo da internet</li></ul></div>
        <div class="card cd"><div class="ct">Tutela Ressarcitória</div><ul><li>Indenização por danos materiais e morais</li><li>Pressupõe dano já ocorrido</li><li>Cumulável com tutela inibitória</li><li>Dano moral: prescinde de prova do prejuízo</li></ul></div>
      </div>
      <div class="sl">Proteção Post Mortem</div>
      <p>O <span class="art">art. 12, §único CC</span> prevê que, em se tratando de morto, o cônjuge sobrevivente ou qualquer parente em linha reta ou colateral até o quarto grau tem legitimidade para exigir a cessação da ameaça ou lesão e reclamar perdas e danos.</p>
      <div class="co ci"><span class="co-ico">ℹ</span><div><strong>STJ — Súmula 37:</strong> São cumuláveis as indenizações por dano material e dano moral oriundos do mesmo fato. Aplicável às violações de direitos da personalidade.</div></div>
    </div>
  </div>
</div>
```

- [ ] **Step 2: Verificar IDs únicos**

```bash
grep -c 'id="mod-dir"' BRUNAO/civil/prova-1.html
```
Esperado: 1 (apenas o novo módulo Direitos da Personalidade).

```bash
grep -c 'id="mod-eman"' BRUNAO/civil/prova-1.html
```
Esperado: 1 (módulo Emancipação).

---

### Task 6: Atualizar o quiz

**Files:**
- Modify: `BRUNAO/civil/prova-1.html`

Remover 2 questões sobre morte/comoriência e adicionar 2 questões sobre Historicidade. Total permanece 20.

- [ ] **Step 1: Remover questão sobre comoriência (questão 13 no array)**

Remover o objeto inteiro:
```js
{q:"A comoriência, prevista no art. 8.º CC, é aplicável quando:",opts:["A) Há dúvida sobre qual dos mortos faleceu primeiro","B) Ambos morrem em acidente de trânsito no mesmo dia","C) Os mortos eram cônjuges","D) Há dúvida sobre a causa da morte"],ans:0,fb:"A comoriência (art. 8.º CC) se aplica quando há <strong>dúvida sobre qual morreu primeiro</strong>, presumindo-se simultaneidade. Não exige que tenham morrido no mesmo lugar ou que sejam parentes."},
```

- [ ] **Step 2: Remover questão sobre morte presumida (questão 20 no array)**

Remover o objeto inteiro:
```js
{q:"A morte presumida sem declaração de ausência (art. 7.º CC) é cabível quando:",opts:["A) A pessoa desaparece por mais de 10 anos","B) O desaparecido estava em situação de perigo de vida ou em campanha militar","C) O cônjuge pede a declaração após 5 anos","D) O desaparecido não tem herdeiros conhecidos"],ans:1,fb:"O art. 7.º CC permite declarar a morte presumida, <strong>sem necessidade de abertura de sucessão de ausência</strong>, quando o desaparecido estava em situação de extremo perigo de vida (art. 7.º, I) ou em campanha militar (art. 7.º, II)."}
```

- [ ] **Step 3: Adicionar 2 questões de Historicidade ao final do array**

Antes do `];` que fecha o array `questions`, adicionar:
```js
  {q:"A compilação jurídica que unificou o Direito Romano e serve como principal fundamento do sistema da civil law é:",opts:["A) Lei das XII Tábuas","B) Corpus Juris Civilis de Justiniano","C) Ordenações Filipinas","D) Código Napoleônico de 1804"],ans:1,fb:"O <strong>Corpus Juris Civilis</strong> (529–534 d.C.), compilado por ordem do Imperador Justiniano, é a principal fonte do Direito Civil ocidental. É composto pelas Institutas, Digesto, Codex e Novelas."},
  {q:"O Código Civil de 1916 (Lei 3.071/1916) foi elaborado por:",opts:["A) Teixeira de Freitas","B) Rui Barbosa","C) Miguel Reale","D) Clóvis Beviláqua"],ans:3,fb:"O projeto do <strong>Clóvis Beviláqua</strong> foi o aprovado como CC 1916. Teixeira de Freitas elaborou o Esboço (influenciou a Argentina), mas seu projeto não foi adotado. Miguel Reale presidiu a comissão do CC 2002."}
```

- [ ] **Step 4: Atualizar o cabeçalho do quiz e o total exibido**

Verificar que o `<div class="mdesc">` do módulo quiz ainda diz "Pessoa Natural · Nascituro · Capacidade · Emancipação". Atualizar para:
```html
<div class="mdesc">Historicidade · Arts. 1–5 · Nascituro · Emancipação · Direitos da Personalidade</div>
```

- [ ] **Step 5: Verificar contagem**

```bash
grep -o "ans:" BRUNAO/civil/prova-1.html | wc -l
```
Esperado: 20

---

### Task 7: Commit final

**Files:**
- Modify: `BRUNAO/civil/prova-1.html`

- [ ] **Step 1: Verificação visual**

Abrir `http://localhost:8000/BRUNAO/civil/prova-1.html` (com `python -m http.server` na raiz do projeto) e checar:
- Nav tem 6 pills: Historicidade, Pessoa Natural, Nascituro, Emancipação, Direitos da Personalidade, Quiz
- Historicidade abre por padrão com 3 subtabs funcionando
- Pessoa Natural tem apenas 2 subtabs (Conceito e Início da Personalidade)
- Emancipação funciona normalmente
- Direitos da Personalidade tem 3 subtabs (Conceito, Tipos, Proteção)
- Quiz tem 20 questões sem nenhuma sobre morte/comoriência
- Botão "Próxima" é verde (não transparente/quebrado)
- Dark e light mode funcionam

- [ ] **Step 2: Commit**

```bash
git add BRUNAO/civil/prova-1.html
git commit -m "fix: corrigir conteúdo da Prova 1 Civil — adicionar Historicidade, promover Direitos da Personalidade, remover morte/comoriência"
```
