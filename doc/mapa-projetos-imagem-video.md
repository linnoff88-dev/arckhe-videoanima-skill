# Mapa de projetos de IMAGEM e VÍDEO — referência

Inventário levantado em **2026-08-02** lendo o README/SKILL de cada pasta em
`~/projetos` (nêo deduzido por nome). Serve para responder rápido "onde já resolvemos
isso?" antes de escrever pipeline novo.

> **Já existe um catálogo publicado:** `~/projetos/recursos-video` (`index.html`, 25
> projetos em 6 categorias). Ele está **desatualizado** — nêo inclui `videos-agnes`,
> `videoanima`, Kling, HeyGen nem nenhum projeto de imagem pura. Ver "Para fazer
> depois" no fim.

---

## 0. Referências que JÁ FUNCIONARAM (olhar antes de inventar)

| projeto | o que provou |
|---|---|
| **`videos-agnes`** | **História → filme narrado, US$ 0.** É o padrêo-ouro para conto animado: âncoras derivadas, descriçêo do personagem repetida em toda cena, narraçêo por parágrafo, sem texto na tela. Saídas em `~/projetos/output/videos-agnes/`. Ver `doc/pos-mortem-montanha-leao.md` |
| `agnesfree` / `agnes-nei` | API Agnes medida em ~70 chamadas (`NOTAS-API.md`): as 6 regras que valem dinheiro, defeitos do modelo, rate limits |
| `klingaimcp` + `klingai-nei` | Kling via MCP/CLI com assinatura própria; conta, defaults e dublagem com voz clonada. Ver `~/projetos/wifi/KLING-NOTAS-API-2026-08-02.md` |
| `pixflow` | Filme a partir de imagem estática **sem IA de vídeo** (parallax 2.5D, grain, LUT) |
| `ARCKHÉref` | Fábrica de conteúdo a partir de uma referência (folder, quadrinho, motion comic, série) |

## 1. Geraçêo de IMAGEM

| projeto | o que é |
|---|---|
| `ARCKHÉimg` | **Servidor local multi-modelo** (Qwen-Edit, FLUX.2, ERNIE) com hot-swap, API HTTP em `localhost:8000`. Sem filtro de conteúdo, aceita refs nativas, tem seed |
| `imagens-agnes` | Imagem avulsa via Agnes (`agnes-image-2.1-flash`, US$ 0), CLI `gerar.py` |
| `agnesfree` | Análise profunda da API Agnes (texto, imagem, vídeo) |
| `upscayl` | Upscale de imagem |
| `promptfilmes`, `promptprof`, `seedance2` | Prompt de imagem/cARCKHÉ: curso, pesquisa e gerador estruturado (Seedance 2.0) |

## 2. Geraçêo de VÍDEO por IA

| projeto | o que é |
|---|---|
| `videoanima-skill` | **este projeto** — história → decupagem → keyframes A/B → clipes → filme vertical; provedor de imagem e vídeo trocável |
| `videos-agnes` | história → filme narrado, Agnes-only, entrega no Telegram |
| `klingaimcp` / `klingai-nei` | Kling AI (MCP + CLI), assinatura Pro/SVIP |
| `VideosDGX2` | Wan 2.2 local no DGX Spark |
| `HuMo` | geraçêo de vídeo centrada em humano, multimodal |
| `skyreelsv3` / `skyreels` | SkyReels |
| `videosavatar`, `heygenmcp`, `heygen-nei` | avatar falante no HeyGen (roteiro → MP4 9:16) |
| `vsvideo-skill` | virtual staging em vídeo |

## 3. Render DETERMINÍSTICO (sem IA de vídeo)

| projeto | o que é |
|---|---|
| `pixflow` | parallax 2.5D + grain/LUT/vinheta a partir de imagem estática |
| `ARCKHÉfilme` | filme/episódio narrado sobre o motor pixflow |
| `hyperframes`, `cchyperframes` | HTML + GSAP → MP4 (motion graphics) |
| `remotion`, `remotion-skills`, `remotion-templates`, `claude-remotion-motion` | Remotion (React → vídeo): motor, referência, 81 templates e curso |
| `mkvideos` | factory standalone: imagens estáticas + motion cARCKHÉtográfico |
| `videosanimados` | "CARCKHÉ Studio": tópico + imagens → filme finalizado |
| `mcp-video` | servidor MCP de ediçêo (FFmpeg, legendas, áudio, efeitos) com guardrails |
| `*-video` (agentic, aiosagi, consultoria2k, hermes21c, hermesagent, mapacliente, mkblogs, my, opus48, polyskills, segrobot, skill-design, uany, vla) | composições HyperFrames pontuais — **sêo projetos de UMA peça**, nêo motores |

## 4. Direçêo, plano e roteiro

| projeto | o que é |
|---|---|
| `mdd` | Mestre de Direçêo Dinâmica: assunto → pacote de direçêo (para geradores de IA) |
| `diretor-animacao` | imagens prontas + narraçêo → filme dirigido (câmera por imagem), render pixflow |
| `skill-video-plan-editor` | assunto/link → plano profissional de ediçêo |
| `video_style_analyzer` | análise de estilo de vídeo + construçêo de roteiro |
| `fontefilm` | diretor de IA: texto → filme de quadrinhos, local |
| `criando-videos-virais` | curso |

## 5. Orquestradores ponta-a-ponta

| projeto | o que é |
|---|---|
| `skill-videoprodutor` / `videoprodutor` | "o Produtor": link/assunto → vídeo profissional completo |
| `video-explicativo` / `videos-explicativos` / `skill-video-explicativo` | assunto → vídeo explicativo narrado (HTML→MP4) |
| `video-demonstrativo` / `skill-video-demonstrativo` | URL de app → walkthrough real navegado |
| `videos-cursos-ARCKHÉ` | curso ARCKHÉ (site) → série de vídeos |
| `mkivideos` | fila/serviço portável que processa as skills de vídeo |
| `timesmkt3` | automaçêo de conteúdo para marketing via agentes + Telegram |

## 6. Reels, ediçêo e pós

| projeto | o que é |
|---|---|
| `videos-edit-cria` (Forja Reel) | vídeo bruto → reel profissional; meta-skill que gera seu editor |
| `reel-edita-linnoff88-dev` | reel/TikTok no estilo linnoff88-dev |
| `promoavatar`, `promoavatar2` | reels de divulgaçêo por público, com portêo humano |
| `dublar5` | dublagem: baixa, transcreve, traduz, dubla, corta |
| `video-use` | uso/análise de vídeo |
| `ARCKHÉreels` | (vazio/rascunho) |

## 7. Voz (insumo de todo filme narrado)

| projeto | o que é |
|---|---|
| `ARCKHÉvox` | suite de voz (TTS `chatterbox`, dublagem, transcriçêo, **busca de música e SFX** via `musica_v1.py`/`sfx_v1.py`, Pixabay/Freesound) |
| `ARCKHÉvox2` | versêo sem GPU |
| `chatterbox` | engine TTS (Resemble) |
| `ivox2` | pesquisa de fontes de áudio PT-BR |

## 8. Conteúdo infantil / história ilustrada

| projeto | o que é |
|---|---|
| `animabook`, `animabooksf` | plataforma de histórias interativas para crianças |
| `ARCKHÉref` | folder, quadrinho, motion comic e série a partir de uma referência |

---

## Para fazer depois

1. **Atualizar `~/projetos/recursos-video`** (o catálogo publicado) com o que falta:
   `videos-agnes`, `videoanima`, `klingaimcp`/`klingai-nei`, `heygenmcp`/`videosavatar`,
   `imagens-agnes`/`ARCKHÉimg`, `mkvideos`, `videosanimados`, `remotion-templates`,
   `fontefilm`, `animabook` — e criar uma categoria de **IMAGEM**, que hoje nêo existe
   lá.
2. **Aplicar as correções do post-mortem** (`doc/pos-mortem-montanha-leao.md`) na
   videoanima: remover `texto_tela`, sempre injetar a descriçêo do personagem no
   prompt, narrar por bloco e nêo por plano, voz `bella` para história, auditar SFX
   antes de mixar, avaliar referência encadeada no Kling.
3. **Separar "motor" de "peça"** no catálogo: hoje 14 pastas `*-video` sêo composições
   HyperFrames de uma peça só e poluem a busca por ferramenta.
