# CAEM — Sistema de Design
> Centro Acadêmico de Engenharia Mecânica · UFPA Tucuruí

---

## Direção e Sensação

**Produto:** Site institucional do CAEM — entidade representativa estudantil, FEM CAMTUC.

**Quem abre:** Estudante de Eng. Mecânica da UFPA Tucuruí, prospecto, ou empresa parceira.

**Sensação alvo:** Placa de identificação de uma máquina de grande porte. Preciso, hierárquico, força sem ornamento. Uma sede estudantil que se leva a sério. Denso de propósito, não de informação.

**Domínio explorado:** Engrenagem, Torque, Usina (Tucuruí), Forja, Touro Mecânico, Eixo, Corpo Estudantil.

**Signature:** Marcadores de seção em notação de placa técnica (`01 // 02`), presidente card full-width com watermark `⚙`, blueprint grid no hero, inputs mais escuros que o card (inset).

---

## Tokens

```css
/* Accent — domínio */
--touro:   #8C2BBE;   /* arco de solda — accent principal */
--eixo:    #4B176E;   /* eixo estrutural — accent secundário */
--magenta: #A4165A;   /* detalhe quente, uso mínimo */
--cobre:   #C99A8A;   /* cobre rosé, uso decorativo raro */

/* Superfícies — elevação em calor roxo */
--carbono: #08050D;   /* base — concreto e óleo */
--forja:   #100817;   /* superfície 1 — sections alternadas */
--nucleo:  #16091F;   /* superfície 2 — cards */
--nucleo2: #1E0D2A;   /* superfície 3 — cards elevados (hover) */

/* Texto — 4 níveis */
--aco:     #F6F4FA;   /* primário — aço polido */
--prata:   #D8D7DE;   /* secundário — prata técnica */
--grafite: #787684;   /* terciário — grafite */
--sombra:  #3A3648;   /* quaternário — placeholder / disabled */

/* Bordas — progressão de 4 níveis */
--b1: rgba(140,43,190,0.10);   /* separação padrão */
--b2: rgba(140,43,190,0.22);   /* ênfase */
--b3: rgba(140,43,190,0.45);   /* máximo */
--b4: var(--touro);             /* foco / hover vivo */

/* Semântico */
--ouro:   #D4A843;
--prata2: #9BA4B5;
--bronze: #B87333;
```

---

## Tipografia

| Nível | Fonte | Tamanho | Peso | Uso |
|---|---|---|---|---|
| Display | Bebas Neue | clamp(88px, 18vw, 180px) | — | Título hero |
| H2 | Bebas Neue | clamp(36px, 5vw, 56px) | — | Títulos de seção |
| H3 | Bebas Neue | 28–44px | — | Cards principais |
| Label técnica | Montserrat | 9–11px | 700 | Cargos, marcadores, tags |
| Corpo | Montserrat | 13–15px | 400 | Parágrafos |
| Muted | Montserrat | 11–12px | 500–600 | Matrículas, metadados |

**Tracking:**
- Títulos Bebas: `letter-spacing: 0.03–0.1em`
- Labels em caps: `letter-spacing: 0.22–0.32em`
- Corpo: padrão

---

## Depth Strategy: Borders-Only

**Regra:** Zero sombra em qualquer elemento. Toda elevação é comunicada via cor de superfície e borda.

```
carbono (base)
  └── forja (sections alternadas)
       └── nucleo (cards)
            └── nucleo2 (hover state dos cards)
```

Bordas não são decoração — são estrutura. Quanto mais `--b4`, mais importante a fronteira.

---

## Espaçamento (base 4px)

```css
--s1: 4px;   /* gap mínimo, ícone inline */
--s2: 8px;   /* gap entre elementos pequenos */
--s3: 12px;  /* padding label, gap icon+texto */
--s4: 16px;  /* padding base de cards compactos */
--s5: 24px;  /* padding padrão de cards */
--s6: 32px;  /* gap entre colunas pequenas */
--s7: 48px;  /* padding de cards grandes, gap de colunas */
--s8: 64px;  /* gap de seções internas */
--s9: 96px;  /* padding vertical de seções */
```

---

## Raio

```css
--r: 2px;   /* sharp — técnico, industrial. Único valor usado. */
```

Sem bordas arredondadas em nenhum componente. Tudo `border-radius: 2px`.

---

## Componentes Documentados

### Marcador de Seção
```html
<div class="sec-mark">
  <div class="sec-num">01</div>     <!-- borda --b2, fundo transparente -->
  <div class="sec-line"></div>      <!-- linha 1px, max-width 40px -->
  <div class="sec-label">TÍTULO</div>
</div>
```
Segue com `<h2 class="section-title">` + `<div class="title-line">` (40px, 2px, --touro).

---

### Dado-Placa (stat card)
```html
<div class="dado-placa">
  <div class="dp-label">RÓTULO</div>
  <div class="dp-valor">VALOR</div>
  <div class="dp-sub">Descrição</div>
</div>
```
- Background: `--nucleo`, border: `--b2`
- Accent vertical: `::before` 2px `--touro` na borda esquerda
- Hover: `border-color: --b3`

---

### Dir-Card (membro da diretoria)
```html
<div class="dir-card">
  <div class="dir-cargo">CARGO</div>
  <div class="dir-nome">Nome Completo</div>
  <div class="dir-mat">Mat. XXXXXXXXXX</div>
</div>
```
- Background: `--nucleo`, border: `--b1`
- Hover: background `--nucleo2`, border `--b2`
- Top accent: `::before` linha 1px que vira `--touro` no hover
- Grid: 3 colunas desktop / 2 tablet / 1 mobile

---

### Dir-Presidente (card especial)
Full-width, tratamento hero. Presidente sempre separado visualmente dos demais.
- Border: `--b3` (maior ênfase)
- Accent vertical: 3px `--touro`
- Watermark `⚙` via `::after`, 120px, opacity 0.05
- Badge lateral com nome da entidade

---

### Evento-SM (card lateral de evento)
```html
<div class="evento-sm">
  <span class="evento-sm-tipo">TIPO</span>
  <h4>Título</h4>
  <p>Descrição curta.</p>
</div>
```
- Accent esquerdo via `::after` 2px que vira `--touro` no hover

---

### Form Controls
- Inputs: background `--forja` (mais escuro que o card `--nucleo`) — comunica "inset"
- Border: `--b1` default, `--touro` no focus
- Placeholder: `--sombra`
- Sem box-shadow nem outline — só border-color

---

### Blueprint Grid (hero)
```css
background-image:
  linear-gradient(rgba(140,43,190,0.055) 1px, transparent 1px),
  linear-gradient(90deg, rgba(140,43,190,0.055) 1px, transparent 1px);
background-size: 44px 44px;
mask-image: radial-gradient(ellipse 75% 75% at 50% 50%, black 30%, transparent 80%);
```
Usado exclusivamente no hero. Não repetir em outras seções.

---

## Regras de Uso

- `--touro` apenas em: accents, hovers, CTAs, bordas de ênfase, dots indicadores. Nunca como background de área grande.
- `--magenta` e `--cobre` reservados para detalhes futuros (certificados, banners). Não usar no site base.
- Emojis em componentes (ícones de redes, contato) são aceitáveis enquanto não houver iconografia consistente.
- Sombras: **proibidas**. Se precisar elevar, suba uma camada de superfície + reforce a borda.
- Gradientes: apenas no glow do hero (`::after`) e no blueprint. Nenhum outro uso.

---

## Arquivos Locais

```
12 - Designer/CAEM/
  index.html
  .interface-design/system.md   ← este arquivo
  assets/
    logos/
      logo-caem-roxo.png    ← variante principal (colorida, transparente)
      logo-caem-branco.png  ← para fundos escuros sem contraste roxo
      logo-ufpa.png
      logo-fem.png
    fotos/                  ← fotos do IISEMEC (para galeria futura)
    estatuto/
      ESTATUTO CAEM 2024.docx
```

**Repo:** https://github.com/caemtucurui-web/CAEM  
**Live:** https://caemtucurui-web.github.io/CAEM/  
**Token PAT:** mesmo do SIMPOMEC, válido até 2027-05-30
