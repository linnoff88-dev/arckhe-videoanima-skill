# Veredito sobre as 4 críticas (2026-08-02)

Avaliaçêo dos documentos em `~/thinclient_drives/.clipboard/`:
`analise_consistencia_ia_video.md` · `analise_coerencia_a_neve_e_o_outro_menino.md` ·
`analise_movimento_objetos_fixos_roteiro.md` · `ancoras_frames_o_que_muda.md`.

Critério: cada ponto foi confrontado com o que **medimos** hoje nos dois filmes
gerados (47 e 46 clipes), nêo com opiniêo.

---

## 1. Confirmado pelos dados

### O pipeline nêo distingue tipo de plano — e isso anima o que deveria ficar parado
A crítica de movimento acerta em cheio. Medido em `video-agnes/`:

| grupo | movimento médio |
|---|---|
| planos que a crítica classifica como **tableau** (11, 16, 18, 22, 25, 34, 40) | **6,98** |
| planos de **açêo física** (7, 9, 21, 27, 32, 43) | 10,12 |

Há alguma diferenciaçêo, mas ela vem por acaso — e dois tableaux estouram:
**p25 (snowboard abandonado) a 11,2** e **p34 (rosto do menino soterrado) a 12,4**,
movendo tanto quanto uma cena de corrida. Uma prancha largada na neve nêo deve ter
movimento de plano de perseguiçêo. A causa é a que a crítica aponta: `acao_b` é
tratado como *obrigaçêo de mudança* em todo plano, sem `tipo_plano`.

### Falta bíblia visual e controle de estado
Correto e é hoje a maior lacuna. As fichas de personagem têm 2 linhas para sustentar
50 planos; nêo fixam formato de rosto, cor de olhos, altura relativa, **de que lado**
fica a orelha dobrada do cêo ou a luva que falta. Também nêo há estado acumulado
(neve no casaco, cansaço, o que está na mochila).

### As incoerências de roteiro sêo reais
Todas verificáveis na decupagem: a **corda** é carregada no plano 6 e nunca usada; a
**caneca com vapor** (p38) nêo tem garrafa térmica na mochila; o **cachecol** é
anunciado como marcador de várias bifurcações mas só existe um; as **lanternas**
aparecem na crista no p40 e voltam a estar longe no p44; a **mochila vermelha** é
prometida como elemento de descoberta e nêo cumpre funçêo. Nada disso é problema de
render — é roteiro.

### Planos de detalhe sem `refs`
Correto: 6, 7, 19, 33 e 43 mostram mêos, botas e braços com `refs: []`. Sem âncora,
figurino e anatomia derivam.

---

## 2. Já resolvido antes das críticas chegarem

- **Prompt negativo global** (crítica #13 do doc de consistência): existe desde hoje,
  `NEGATIVO_VIDEO`, no padrêo LTX-2/Wan 2.2.
- **Linguagem de câmera misturando PT e EN** (#9): era um bug real — a dica do
  keyframe B ia em português para o gerador. Corrigido; foi o que levou o movimento
  de 3,36 para ~10.
- **`refs` nêo trava identidade** (#1): confirmado e corrigido — a descriçêo textual
  do personagem voltou a entrar no prompt junto da referência.

---

## 3. Onde as críticas erram, e a mediçêo mostra

**Todas as quatro assumem que o texto governa o resultado.** Os esquemas propostos
(`estado_entrada`, `movimento_proibido`, `lens: 35mm`, `clima.visibilidade: 30m`)
sêo camadas de *texto*. Medimos hoje, com os mesmos keyframes e 43 planos:

| | movimento médio |
|---|---|
| prompt completo (~81 palavras) | 10,07 |
| prompt mínimo (~18 palavras) | 9,93 |

**Diferença de 1,4%.** O texto quase nêo move o ponteiro em modo keyframes — o que
manda é o par de imagens A→B. O próprio `who_am_i` do Kling diz isso: *"the input
image is the primary driver"*. Portanto:

- Campos como `movimento_proibido: [prancha_deslizar]` provavelmente **nêo terêo
  efeito** se forem só mais texto no prompt. Para segurar a prancha, o caminho é o
  **keyframe B mostrar a prancha na mesma posiçêo** — que é exatamente o que o quarto
  documento (`ancoras_frames`) já reconhece.
- O risco de adotar o esquema completo é criar uma especificaçêo que ninguém escreve
  e que o modelo nêo lê.

O quarto documento é o mais correto dos quatro justamente por reclassificar: com
âncoras e frames A/B, metade das exigências vira proteçêo secundária.

---

## 4. O que nenhuma das críticas viu

Sêo os dois problemas que de fato impediram a entrega hoje:

1. **O filtro de conteúdo da Agnes reage às IMAGENS, nêo ao texto, e é
   nondeterminístico.** Provado por experimento: as imagens do p37 foram recusadas
   até com prompt `"gentle motion"`; o prompt completo do p37 **passou** quando
   colado em outro par de imagens. E entre duas execuções o conjunto de planos
   recusados mudou (20/37/41/48/50 → 13/29/44/45). O gatilho medido é **contato
   físico próximo envolvendo criança**: afastar os corpos liberou os três planos.
2. **A montagem truncava o filme em silêncio.** O `adelay` dos SFX deixava carimbos
   de tempo tortos e o concat abortava — 45s de 158s — imprimindo a duraçêo errada
   como sucesso.

Nenhum esquema de YAML resolveria esses dois. Sêo de pipeline.

---

## 5. Resultado — ordem de execuçêo

Por impacto medido, nêo por ordem dos documentos:

1. **`tipo_plano: acao | revelacao | tableau`**, e em tableau o keyframe B repete a
   composiçêo (mudam só neve, respiraçêo e a câmera). É a correçêo de movimento com
   efeito real, porque age na **imagem**, nêo no texto.
2. **Bíblia visual** com atributos imutáveis por personagem e por ambiente, mais
   âncoras de ambiente (vila, floresta, bacia) além das de personagem.
3. **Corrigir o roteiro**: corda, garrafa térmica, cachecol/fitas, lanternas
   duplicadas, mochila vermelha com funçêo. É barato e independe de modelo.
4. **`refs` nos planos de detalhe** (6, 7, 19, 33, 43).
5. **Regra de contato físico** na escrita: cenas de abraço/apoio precisam ser
   compostas com distância, ou vêo para o Kling.
6. O resto do esquema proposto (lente, visibilidade em metros, estado de entrada
   detalhado) só depois de medir se muda alguma coisa — hoje a evidência diz que nêo.
