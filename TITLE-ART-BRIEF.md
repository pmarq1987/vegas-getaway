# Vegas Getaway — Arte da tela de título (Didi e Tami)

Duas peças em alta para as laterais da tela de início, no formato Marvel vs
Capcom. **Não são sprites de jogo** — são ilustração de apresentação, e por isso
podem ter muito mais detalhe do que os 80px de altura da folha de gameplay.

O código já está preparado: se os arquivos existirem, ele os usa; se não,
continua com o sprite ampliado. Não precisa mexer em nada além de salvar.

---

## Entrega

```
casino-escape/sprites/
  title-didi.png
  title-tami.png
```

| Item | Valor |
|---|---|
| Altura | **1024 px** (largura livre, proporcional) |
| Fundo | **Transparente** (alpha real, não branco nem verde) |
| Ancoragem | Personagem **encostado na borda de baixo** do PNG — os pés são o último pixel |
| Enquadramento | Corpo inteiro, folga lateral mínima |
| Direção | Virado para a **direita** (o código espelha a Tami sozinho) |

O jogo reduz para 430px de altura com suavização, então 1024 dá margem
confortável para telas retina sem pesar no carregamento.

---

## O que manter igual ao que já existe

Este é o ponto crítico: **é o mesmo personagem, no mesmo ângulo**, só que
desenhado com mais resolução. Use os sprites atuais como referência de modelo —
`sprites/didi.png` e `sprites/tami.png`, primeira célula da linha 0 (idle).

- **Mesma vista lateral**, mesma postura de idle relaxado
- **Mesmo rosto, mesmo corte de cabelo, mesma barba**
- **Mesma roupa** — não reinterprete o figurino
- **Mesma paleta** (tabela abaixo)

### Didi
| Parte | Hex |
|---|---|
| Pele | `#d9a066` (sombra `#9b633c`, luz `#f0bf8a`) |
| Cabelo / barba | `#241a12` |
| Colete e calça | `#141220` — **preto**, não roxo |
| Camisa | `#f3ead9` |
| Gravata-borboleta | `#ff2f76` |

### Tami
| Parte | Hex |
|---|---|
| Pele | `#caa27c` (sombra `#956d51`, luz `#e6be95`) |
| Cabelo | `#2a1420` |
| Vestido | luz `#5ab4ff` · base `#2e8dff` · sombra `#1b4e9b` |
| Brincos / salto | `#ffcb4d` |

> Existe também uma variante de vestido vermelho em `sprites/tami-red.png`.
> Se a decisão for pelo vermelho, use `#c8123f` / `#8f1030` / `#e8476d` e me avise
> para eu trocar a referência.

---

## Prompts

### Didi

```
High-resolution 16-bit style character illustration for an arcade
character-select screen, in the spirit of Marvel vs Capcom select art.
Full body, SIDE VIEW facing RIGHT, relaxed standing idle pose,
weight on one leg, confident friendly expression.

Brazilian man in his 30s, heavyset with a large round belly and thick arms,
short dark brown hair, full dark beard.
BLACK casino dealer waistcoat (not purple) over a cream dress shirt with
rolled sleeves, magenta bow tie, black trousers, black shoes.

Crisp clean lineart, bold black outline, rich cel shading with clear
light and shadow separation, dramatic rim light from above.
Dark navy casino palette with gold and magenta accents.
Transparent background. No scenery, no text, no logo.
Character fills the frame vertically, feet at the very bottom edge.
```

### Tami

```
High-resolution 16-bit style character illustration for an arcade
character-select screen, in the spirit of Marvel vs Capcom select art.
Full body, SIDE VIEW facing RIGHT, relaxed standing idle pose,
weight on one hip, confident poised expression, holding a casino chip.

Brazilian woman in her 30s, long wavy dark hair past the shoulders,
bright royal blue cocktail dress, gold hoop earrings, gold high heels.

Crisp clean lineart, bold black outline, rich cel shading with clear
light and shadow separation, dramatic rim light from above.
Dark navy casino palette with gold and magenta accents.
Transparent background. No scenery, no text, no logo.
Character fills the frame vertically, feet at the very bottom edge.
```

---

## Duas armadilhas que valem cuidado

**Fundo transparente de verdade.** Aqui o fundo verde não serve: a arte tem
suavização nas bordas, e recortar por cor deixa uma franja verde no contorno.
Se a ferramenta só entregar fundo chapado, prefira branco e me avise — eu removo
por preenchimento a partir da borda, que preserva a transição.

**Consistência entre as duas peças.** Didi e Tami vão aparecer lado a lado na
mesma tela. Gere as duas com a mesma iluminação e o mesmo nível de acabamento,
de preferência em sequência com a mesma seed — se uma vier com traço mais
detalhado que a outra, a tela desmonta.
