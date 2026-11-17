# videoanima

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

HistÃ³ria â†’ **decupagem cinematogrÃ¡fica** â†’ imagens â†’ clipes â†’ filme vertical narrado,
com provedor de imagem e de vÃ­deo escolhÃ­veis por parÃ¢metro.

> âš ï¸ **Em ajuste â€” nÃ£o Ã© versÃ£o estÃ¡vel.** O pipeline roda ponta a ponta, mas estÃ¡ em
> ciclo aberto de correÃ§Ã£o a partir dos filmes que ele mesmo produziu. O primeiro corte
> saiu ruim (cenas paradas, personagem inconsistente, narraÃ§Ã£o picotada); o que foi
> medido, e o que jÃ¡ mudou por causa disso, estÃ¡ em
> [`doc/pos-mortem-montanha-leao.md`](doc/pos-mortem-montanha-leao.md) â€” leia antes de
> usar como referÃªncia. Ainda em aberto: narraÃ§Ã£o ainda estica os planos alÃ©m do ritmo
> planejado, os SFX entram sem audiÃ§Ã£o prÃ©via, e a referÃªncia encadeada entre planos
> (plano N usando o Nâˆ’1) nÃ£o foi implementada.

## ðŸ“– Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/videoanima-skill/guia/**

```bash
python3 rodar.py exemplo --so-decupagem          # valida ritmo + custo, nÃ£o gasta
python3 rodar.py exemplo --img agnes --video agnes
python3 rodar.py exemplo --img kie   --video klingai
```

**Tudo mora no output.** Um id solto resolve para
`~/projetos/output/videoanima/<id>/decupagem.yaml` â€” texto e imagem no mesmo lugar.
`historias/<id>/` no repo Ã© sÃ³ semente: na primeira execuÃ§Ã£o a decupagem Ã© copiada
para o output e a de lÃ¡ passa a ser a viva (edite essa).

| arquivo | o que Ã© |
|---|---|
| `gramatica.py` | vocabulÃ¡rio de direÃ§Ã£o destilado de `doc/analise-estilo-fbvideo.md`: enquadramento, Ã¢ngulo, movimento, velocidade, look, ritmo â†’ fragmentos de prompt |
| `provedores.py` | adaptadores de imagem (`agnes`/`inemaimg`/`kie`) e vÃ­deo (`agnes`/`kling`/`klingai`/`kie`); cada armadilha medida mora no adaptador dela |
| `narracao.py` | inemavox chatterbox (voz por decupagem: `bella` para histÃ³ria), com a revisÃ£o de dicÃ§Ã£o antes do TTS |
| `montagem.py` | o que o gerador nÃ£o faz: slow/speed-ramp, handheld, zoom-punch, trilha com ducking, SFX, loudnorm, mediÃ§Ã£o de movimento |
| `rodar.py` | orquestra, idempotente, com preview de custo antes da primeira chamada paga |
| `~/projetos/output/videoanima/<id>/decupagem.yaml` | o contrato â€” escrito e conferido **antes** de gastar; vive junto dos artefatos |
| `historias/<id>/` | semente no repo: copiada para o output na primeira execuÃ§Ã£o |

**Movimento Ã© o que separa filme de slideshow.** Cada plano traz `acao` em verbo
contÃ­nuo e `acao_b` (onde o gesto termina) â€” Ã© a diferenÃ§a entre A e B que o gerador
anima. HÃ¡ negative prompt contra `still frame` e um portÃ£o que mede o movimento de cada
clipe e refaz o que sair parado. O porquÃª de cada uma dessas decisÃµes estÃ¡ no post-mortem.

**VÃ­deo:** `--video agnes` (US$ 0, submissÃ£o em lote) Â· `--video kling` (assinatura
prÃ³pria, via CLI, aceita caminho local) Â· `--video klingai` (Kling por **fal.ai**,
`FAL_KEY`) Â· `--video kie`. `klingai` e `kie` exigem keyframe em URL pÃºblica â†’ combine
com `--img agnes` ou `--img kie`. Personagem crianÃ§a cai no filtro da Agnes (HTTP 400):
use `--img inemaimg`.

Skill: `~/.claude/skills/videoanima/SKILL.md`

---

Projeto adaptado da comunidade INEMA TDS - Marca Arckhe