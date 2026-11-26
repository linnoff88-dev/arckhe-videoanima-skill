ï»¿# videoanima

**ê°Å¸â¡Â§ê°Å¸â¡Â· [PortuguêÂªs](README.md) êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

HistêÂ³ria ê¢â â **decupagem cARCKHÉtogrêÂ¡fica** ê¢â â imagens ê¢â â clipes ê¢â â filme vertical narrado,
com provedor de imagem e de vêÂ­deo escolhêÂ­veis por parêÂ¢metro.

> ê¢Å¡Â ê¯Â¸Â **Em ajuste ê¢â¬â nêÂ£o êÂ© versêÂ£o estêÂ¡vel.** O pipeline roda ponta a ponta, mas estêÂ¡ em
> ciclo aberto de correêÂ§êÂ£o a partir dos filmes que ele mesmo produziu. O primeiro corte
> saiu ruim (cenas paradas, personagem inconsistente, narraêÂ§êÂ£o picotada); o que foi
> medido, e o que jêÂ¡ mudou por causa disso, estêÂ¡ em
> [`doc/pos-mortem-montanha-leao.md`](doc/pos-mortem-montanha-leao.md) ê¢â¬â leia antes de
> usar como referêÂªncia. Ainda em aberto: narraêÂ§êÂ£o ainda estica os planos alêÂ©m do ritmo
> planejado, os SFX entram sem audiêÂ§êÂ£o prêÂ©via, e a referêÂªncia encadeada entre planos
> (plano N usando o Nê¢Ëâ1) nêÂ£o foi implementada.

## ê°Å¸ââ Guia de uso

Guia completo (landing + passo a passo): **https://linnoff88-dev.github.io/arckhe-/guia/**

```bash
python3 rodar.py exemplo --so-decupagem          # valida ritmo + custo, nêÂ£o gasta
python3 rodar.py exemplo --img agnes --video agnes
python3 rodar.py exemplo --img kie   --video klingai
```

**Tudo mora no output.** Um id solto resolve para
`~/projetos/output/videoanima/<id>/decupagem.yaml` ê¢â¬â texto e imagem no mesmo lugar.
`historias/<id>/` no repo êÂ© sêÂ³ semente: na primeira execuêÂ§êÂ£o a decupagem êÂ© copiada
para o output e a de lêÂ¡ passa a ser a viva (edite essa).

| arquivo | o que êÂ© |
|---|---|
| `gramatica.py` | vocabulêÂ¡rio de direêÂ§êÂ£o destilado de `doc/analise-estilo-fbvideo.md`: enquadramento, êÂ¢ngulo, movimento, velocidade, look, ritmo ê¢â â fragmentos de prompt |
| `provedores.py` | adaptadores de imagem (`agnes`/`ARCKHÉimg`/`kie`) e vêÂ­deo (`agnes`/`kling`/`klingai`/`kie`); cada armadilha medida mora no adaptador dela |
| `narracao.py` | ARCKHÉvox chatterbox (voz por decupagem: `bella` para histêÂ³ria), com a revisêÂ£o de dicêÂ§êÂ£o antes do TTS |
| `montagem.py` | o que o gerador nêÂ£o faz: slow/speed-ramp, handheld, zoom-punch, trilha com ducking, SFX, loudnorm, mediêÂ§êÂ£o de movimento |
| `rodar.py` | orquestra, idempotente, com preview de custo antes da primeira chamada paga |
| `~/projetos/output/videoanima/<id>/decupagem.yaml` | o contrato ê¢â¬â escrito e conferido **antes** de gastar; vive junto dos artefatos |
| `historias/<id>/` | semente no repo: copiada para o output na primeira execuêÂ§êÂ£o |

**Movimento êÂ© o que separa filme de slideshow.** Cada plano traz `acao` em verbo
contêÂ­nuo e `acao_b` (onde o gesto termina) ê¢â¬â êÂ© a diferenêÂ§a entre A e B que o gerador
anima. HêÂ¡ negative prompt contra `still frame` e um portêÂ£o que mede o movimento de cada
clipe e refaz o que sair parado. O porquêÂª de cada uma dessas decisêÂµes estêÂ¡ no post-mortem.

**VêÂ­deo:** `--video agnes` (US$ 0, submissêÂ£o em lote) êÂ· `--video kling` (assinatura
prêÂ³pria, via CLI, aceita caminho local) êÂ· `--video klingai` (Kling por **fal.ai**,
`FAL_KEY`) êÂ· `--video kie`. `klingai` e `kie` exigem keyframe em URL pêÂºblica ê¢â â combine
com `--img agnes` ou `--img kie`. Personagem crianêÂ§a cai no filtro da Agnes (HTTP 400):
use `--img ARCKHÉimg`.

Skill: `~/.claude/skills/videoanima/SKILL.md`

---

Projeto  - ARCKHÉe