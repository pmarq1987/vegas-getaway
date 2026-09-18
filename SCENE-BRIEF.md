# Vegas Getaway — Briefing de Inimigos e Cenário

Fase 2 do jogo interno Rivalo. Complementa o `SPRITE-BRIEF.md` (Didi, Tami e os
7 NPCs de resgate, já entregues). Uso interno — não é material de campanha.

> **Atenção:** a paleta abaixo **substitui** a do briefing anterior. O jogo saiu
> do roxo e foi para o azul-marinho da marca. Arte feita na paleta antiga vai
> destoar do cenário atual.

---

## 1. Como a resolução funciona neste jogo

A câmera trabalha com zoom inteiro **2×**: a tela mostra **480 × 270 unidades de
mundo**, rasterizadas em 960 × 540 pixels de tela.

**Autore toda a arte em unidades de mundo** — ou seja, 1 pixel do PNG = 1 unidade
= 2 pixels na tela do jogador. É a resolução nativa do pixel art; arte maior
será reduzida e vira papa, arte menor é ampliada e borra.

Referência de escala já em jogo: **Didi e Tami têm ~80 unidades de altura**
(frame de 96). Use isso para dimensionar tudo.

Regras gerais, iguais às do briefing anterior:

- PNG com transparência **binária** (alpha 0 ou 255), sem dithering.
- Contorno preto sólido de 1px, sombreamento em **3 tons chapados** por material.
- Sem anti-aliasing, sem gradiente, sem brilho suave.
- Personagens virados para a **direita** (o código espelha sozinho).
- Fundo de geração: verde puro `#00FF00`.

---

## 2. Paleta (atual — marinho)

### Ambiente

| Uso | Hex |
|---|---|
| Fundo profundo | `#050b16` |
| Parede ao fundo (topo) | `#0a1730` |
| Parede ao fundo (base) | `#0f2444` |
| Props / mobiliário | `#132a4e` |
| Superfícies elevadas | `#1d4174` |
| Contorno | `#050308` |

### Acentos (luz de cassino — use com parcimônia)

| Uso | Hex |
|---|---|
| Azul Rivalo | `#2e8dff` |
| Azul claro | `#5ab4ff` |
| Magenta neon | `#ff2f76` |
| Teal neon | `#1fe8c9` |
| Dourado | `#ffcb4d` |
| Creme | `#f3ead9` |

Regra de composição: **o cenário é escuro e dessaturado; o neon é pontual.**
Didi e Tami precisam se destacar contra o fundo — se a parede competir em
saturação com os personagens, a silhueta se perde.

---

## 3. Inimigos

Cinco no total. Todos com âncora nos **pés** (última linha de pixel do corpo).

| Inimigo | Frame | Âncora | Altura do corpo | Papel |
|---|---|---|---|---|
| Segurança Carteador | 96 × 96 | 48, 90 | ~80 | Atira cartas à distância |
| Dado Brutamontes | 80 × 80 | 40, 74 | ~64 | Rola em direção ao jogador |
| Sentinela Caça-Níquel | 96 × 96 | 48, 90 | ~84 | Fixa, cospe cerejas em arco |
| Roleta Giratória | 80 × 80 | 40, 74 | ~64 | Dispara em linha reta |
| **Jackpot Golem** (chefe) | 192 × 192 | 96, 180 | ~150 | Chefe final |

### Folhas por inimigo

**Segurança Carteador** — `enemy-cardshark.png`, 576 × 384 (6 col × 4 lin)

| Linha | Animação | Frames |
|---|---|---|
| 0 | idle | 4 |
| 1 | walk | 6 |
| 2 | throw (arremesso de carta) | 3 |
| 3 | hurt | 1 |

**Dado Brutamontes** — `enemy-dice.png`, 640 × 160 (8 col × 2 lin)

| Linha | Animação | Frames |
|---|---|---|
| 0 | roll (ciclo de rolagem fechado) | 8 |
| 1 | hurt | 1 |

O dado tem duas faces de vida: com 2 HP mostra 5 pontos, com 1 HP mostra 2.
Entregue as duas variações nas colunas 1 e 2 da linha 1.

**Sentinela Caça-Níquel** — `enemy-slot.png`, 384 × 288 (4 col × 3 lin)

| Linha | Animação | Frames |
|---|---|---|
| 0 | idle (rolos girando, luzes piscando) | 4 |
| 1 | attack (alavanca desce, cospe) | 3 |
| 2 | hurt | 1 |

**Roleta Giratória** — `enemy-roulette.png`, 640 × 160 (8 col × 2 lin)

| Linha | Animação | Frames |
|---|---|---|
| 0 | spin (rotação contínua) | 8 |
| 1 | hurt | 1 |

**Jackpot Golem** — `boss-golem.png`, 768 × 768 (4 col × 4 lin)

O chefe tem quatro estados que o código já controla. A leitura visual do
`telegraph` é o que torna o golpe justo — precisa ser inconfundível.

| Linha | Estado | Frames | Leitura |
|---|---|---|---|
| 0 | spin | 4 | Rolos girando, postura neutra |
| 1 | telegraph | 2 | **Aviso**: rolos travam em símbolo de perigo, corpo tensiona, luz vira magenta |
| 2 | slam | 3 | Braços descem e socam o chão |
| 3 | jackpot | 2 | Rolos em 777, máquina se abre e fica **vulnerável** (dano dobrado) |

---

## 4. Cenário

Camadas com parallax. Cada uma é um PNG que se repete horizontalmente —
**a emenda esquerda/direita precisa ser perfeita** (o nível tem 5300 unidades).

| Arquivo | Tamanho | Parallax | Conteúdo |
|---|---|---|---|
| `bg-far.png` | 512 × 270 | 0.25 | Parede do fundo do cassino: molduras, luminárias, textura de carpete na parte alta |
| `bg-mid.png` | 768 × 200 | 0.60 | Fileira de caça-níqueis, mesas de blackjack, roletas ao fundo, banquetas |
| `floor.png` | 256 × 120 | 1.00 | Carpete estampado de cassino + faixa de neon na quina |

Props avulsos, não repetidos:

| Arquivo | Tamanho | Conteúdo |
|---|---|---|
| `prop-pillar.png` | 64 × 270 | Coluna com tubo de neon vertical |
| `prop-exit.png` | 256 × 160 | Porta de SAÍDA — 2 frames lado a lado: trancada (vermelha) e liberada (verde/teal) |
| `prop-vitrine.png` | 128 × 128 | Vitrine de vidro vazia onde os NPCs ficam presos (o sprite do NPC é desenhado por dentro pelo código — **não desenhe personagem aqui**) |
| `prop-pit.png` | 128 × 120 | Buraco no piso: bordas quebradas, escuridão no fundo |

A linha do chão fica em `y = 90` dentro do frame de `floor.png`.

---

## 5. Prompts

Um prompt por frame. Trave a *seed* ou use img2img a partir do primeiro frame
aprovado de cada personagem — sem isso os 8 frames de rolagem do dado viram 8
dados diferentes.

### Bloco de estilo (repetir em todos)

```
Authentic SNES / Sega Genesis 16-bit pixel art. Hard square pixel edges,
solid 1px black outline, 3 flat tones per material, no antialiasing,
no gradients, no glow, no text.
Dark navy casino palette: deep navy #0a1730, mid navy #132a4e,
raised surfaces #1d4174, with sparing neon accents
Rivalo blue #2e8dff, magenta #ff2f76, teal #1fe8c9, gold #ffcb4d.
Flat pure green #00FF00 background. Square composition, ONE subject only.
```

### Segurança Carteador

```
[BLOCO DE ESTILO]
A casino security dealer: broad-shouldered man in a dark navy waistcoat
over a cream shirt, black tie, slicked hair, cold expression,
a fan of playing cards in one hand. Menacing but not gory.
Designed to read at 80 pixels tall. Full body, SIDE VIEW facing RIGHT.
[POSE]
```

Poses: `Standing idle, cards held at chest.` · `Walking forward, mid-stride.` ·
`Winding up and flinging a playing card forward, arm extended.` ·
`Recoiling backward from a hit, cards scattering.`

### Dado Brutamontes

```
[BLOCO DE ESTILO]
A large white casino die, about 64 pixels tall, with stubby black arms and
legs and an angry face on its front face. Red pips. Chunky, heavy, comedic
menace — a rolling bruiser, not a cute mascot.
[POSE]
```

Poses: `Roll cycle frame N of 8: the die tumbling forward, rotated 45×N degrees,
limbs tucked.` · `Cracked and dazed after taking a hit, showing two pips.`

### Sentinela Caça-Níquel

```
[BLOCO DE ESTILO]
A hostile slot machine standing on two short mechanical legs, about 84 pixels
tall. Navy cabinet with gold trim, three reel windows showing 7 / star /
diamond, a row of blinking bulbs across the top, a side lever, glowing
angry eye-like lights above the reels.
[POSE]
```

Poses: `Idle, reels spinning, bulbs lit.` · `Attacking: side lever pulled down,
reels locked, cabinet leaning forward as it spits a cherry projectile.` ·
`Sparking and damaged, cabinet dented, reels dark.`

### Roleta Giratória

```
[BLOCO DE ESTILO]
An animated roulette wheel about 64 pixels across, standing upright on its rim
like a wheel about to roll. Alternating red and black pockets, polished gold
hub and rim, a small white ball lodged in one pocket. Predatory feel.
[POSE]
```

Poses: `Spin cycle frame N of 8: wheel rotated 45×N degrees, motion held
in the pocket pattern.` · `Buckled and wobbling after a hit, rim bent.`

### Jackpot Golem (chefe)

```
[BLOCO DE ESTILO]
A colossal boss slot machine, about 150 pixels tall: a towering navy and gold
cabinet with two massive mechanical arms ending in fists, a wide illuminated
JACKPOT crown across the top, three huge reel windows in the chest, heavy
riveted plating, stubby anchored base. Imposing arcade boss silhouette.
[POSE]
```

Poses:
- `Idle, reels spinning, arms hanging at its sides, crown lit gold.`
- `TELEGRAPH — winding up: reels slam to a stop showing skull symbols, crown
  flares magenta, both arms raised high above the cabinet, body tensed.
  This pose must read instantly as an incoming attack.`
- `Both fists smashing down into the ground, cabinet lurching forward,
  impact cracks.`
- `VULNERABLE — reels showing 777, chest panel splits open spilling teal light
  and gold coins, arms slack at its sides.`

### Cenário

```
[BLOCO DE ESTILO]
Seamlessly tileable horizontally — the left and right edges must match exactly.
[CAMADA]
```

Camadas:
- **bg-far** — `A distant Las Vegas casino back wall, 512x270: dark navy panelled
  walls, framed mirrors, dim wall sconces, patterned upper border. Very low
  contrast, almost silhouette — this sits far behind the action.`
- **bg-mid** — `A row of casino floor furniture, 768x200: banks of slot machines
  with lit screens, blackjack tables with green felt, roulette tables, bar
  stools. Mid contrast, sparse neon highlights.`
- **floor** — `A casino carpet floor strip, 256x120, seen edge-on: ornate
  patterned carpet in navy and gold, with a glowing Rivalo blue neon strip
  running along the front edge at y=90.`

Props:
- **prop-pillar** — `A tall casino column, 64x270, navy marble with a vertical
  neon tube running its full height.`
- **prop-exit** — `A casino emergency exit door, 128x160, heavy metal with a
  push bar and a lit sign above it. Two versions side by side: locked with a
  red sign, and unlocked with a teal sign and the door ajar.`
- **prop-vitrine** — `An EMPTY glass display case, 128x128: gold frame, arched
  glass front, small pedestal inside, subtle reflections. No character inside.`
- **prop-pit** — `A hole smashed through a casino floor, 128x120: broken carpet
  and splintered boards at the edges, pure darkness below.`

---

## 6. Entrega

```
casino-escape/sprites/
  enemy-cardshark.png   576 × 384
  enemy-dice.png        640 × 160
  enemy-roulette.png    640 × 160
  enemy-slot.png        384 × 288
  boss-golem.png        768 × 768
  bg-far.png            512 × 270
  bg-mid.png            768 × 200
  floor.png             256 × 120
  prop-pillar.png        64 × 270
  prop-exit.png         256 × 160
  prop-vitrine.png      128 × 128
  prop-pit.png          128 × 120
```

Aseprite: `Sprite > Color Mode > Indexed` antes de exportar, usando a paleta
da seção 2. Um `manifest.json` no mesmo formato do anterior acelera a
integração — mas não é obrigatório, dá para inferir pelas tabelas acima.

### Checagem de emenda

Para as três camadas tileáveis, verifique antes de entregar: duplique o tile,
cole ao lado e confira se a junção some. Emenda visível vira uma listra
piscando a cada 512 unidades enquanto o jogador corre.
