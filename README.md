# Vegas Getaway — Rivalo Arcade

Jogo arcade interno da Rivalo. Didi e Tami precisam escapar de um cassino de
Las Vegas, libertando sete personagens presos em vitrines e enfrentando o
Jackpot Golem na porta do cofre.

**Uso interno.** Não é material de campanha. O jogo não envolve apostas reais.

---

## Rodar localmente

Não há build nem dependências — é HTML, canvas e Web Audio puros. Mas precisa
ser servido por HTTP, porque os sprites são carregados como imagens (abrir o
`index.html` direto pelo `file://` bloqueia o carregamento).

```bash
python3 -m http.server 8000
```

Depois abra `http://localhost:8000`.

## Publicar no GitHub Pages

Em **Settings → Pages**, escolha a branch `main` e a pasta `/ (root)`.
O site fica disponível em poucos minutos.

---

## Como está organizado

| Caminho | O que é |
|---|---|
| `index.html` | O jogo inteiro: lógica, render, áudio e interface |
| `sprites/` | Todas as folhas de sprite e camadas de cenário |
| `manifest.json` | Frames e animações de Didi, Tami e dos NPCs |
| `manifest-phase2.json` | Frames dos inimigos, do chefe e do cenário |
| `SCENE-BRIEF.md` | Briefing de arte de inimigos e cenário |
| `TITLE-ART-BRIEF.md` | Briefing da arte da tela de título |

## Controles

**Teclado** — setas ou WASD para mover, espaço para pular, `Z` joga ficha,
`X` golpe especial, `C` troca de personagem, `Esc` pausa.

**Toque** — os controles aparecem automaticamente em aparelhos sem mouse.
Em paisagem a experiência é bem melhor que em retrato.

## Detalhes técnicos

- **Resolução**: mundo de 480 × 270 unidades, renderizado em 960 × 540 com
  zoom inteiro 2×. A arte é autorada em unidades de mundo (1 px = 1 unidade).
- **Física**: normalizada por tempo, então o jogo não acelera em telas de 120 Hz.
- **Áudio**: sintetizado em Web Audio, sem arquivos externos e sem
  licenciamento de terceiros. Só começa após um gesto do usuário, por política
  do navegador.
- **Personagens**: Didi tem a onda de fichas (dano em área); Tami tem a
  investida (mobilidade com dano e invulnerabilidade).
