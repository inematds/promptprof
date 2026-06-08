# promptprof

Espaço de **pesquisa/experimento com prompts** (imagem, vídeo e direção de arte).
Não é um app nem repositório git — é uma pasta de trabalho onde cada subprojeto
explora um fluxo de geração diferente, da intenção ao resultado final.

> Natureza: pesquisa / educação / testes.

## O que tem aqui

| Pasta | O que é |
|---|---|
| [`kairoboost/`](kairoboost/) | **Base de conhecimento de prompts** — reconstrução aberta do "KairoBoost" da [kairogen.ai](https://kairogen.ai). Um motor "diretor de arte" que expande intenção curta em prompt cinematográfico. |
| [`hormozi-12/`](hormozi-12/) | **Vídeo 9:16** "13 anos em 47s" — 12 lições de negócios do Hormozi. Pipeline completo: plano → direção → imagens → render. |

---

## kairoboost/ — motor de prompts

Cola os 3 arquivos como system prompt em qualquer LLM e manda
`intenção: X / preset: Y / formato: Z` → sai o prompt refinado.

- `SYSTEM-PROMPT.md` — o motor (diretor de arte): estrutura fixa, regras, formato de saída.
- `presets.md` — 15 presets (Cinematográfico, Editorial, Neon noir…) → lente/luz/grading/textura/mood.
- `vocabulario.md` — dicionário de lente, luz, color grading, textura + termos por modelo (Sora/VEO/Nano/MJ/Flux).
- `README.md` — como usar.

## hormozi-12/ — vídeo das 12 lições

Vídeo dark premium âmbar, 9:16, ~58,7s, narração TTS + fundo cinematográfico
ilustrativo por lição (blur leve + movimento de câmera dirigido) + CTA INEMA.CLUB.

**Documentos de direção:**
- `prompts-kairoboost.md` — KairoBoost aplicado: 14 cenas, conceito → metáfora visual → prompt.
- `PROMPT-PLANEJAMENTO.md` — o prompt usado para planejar (system prompt + tarefa + tradução conceito→imagem).
- `MDD-PACKAGE.md` — pacote de Direção Dinâmica (storyboard 14 painéis, câmera/ação/continuidade, faixa do diretor).
- `plano-edicao.json` + `RESUMO.md` — plano de edição validado (skill video-plan-editor).

**Projeto de render (`video/`):**
- `build-index.mjs` — gerador da composição HyperFrames (HTML→MP4). Timing = fonte única (áudio + animação batidos).
- `narration.sh` — gera as 14 faixas TTS (voz pf_dora).
- `assets/img/` — 14 stills geradas no inemaimg (flux2-klein, 9:16).
- `assets/audio/` · `assets/txt/` — narração e roteiros por cena.
- `renders/` — MP4s (`hormozi-12-mdd-9x16.mp4` = versão final).

### Como re-renderizar o vídeo
```bash
cd hormozi-12/video
node build-index.mjs --vertical          # gera index.html (9:16)
npx hyperframes render --quality high --output renders/saida.mp4
```
Para regenerar a narração: `bash narration.sh`. Para regenerar imagens: usar o
client `~/projetos/mkvideos/pipeline/generate-image-inemaimg.js` (servidor
inemaimg em `localhost:8000`).

---

## Stack usada
- **Texto/prompt:** LLM + base kairoboost.
- **Imagem:** [inemaimg](../inemaimg) (FastAPI local, modelo `flux2-klein`).
- **Vídeo:** [HyperFrames](https://hyperframes.heygen.com) (HTML/CSS/GSAP → MP4) + TTS Kokoro (`pf_dora`) + FFmpeg.
- **Skills:** video-explicativo, mestre-direcao-dinamica (MDD), video-plan-editor (VPE).

## Identidade visual
Dark premium âmbar — bg `#0D1321`, painel `#1D2D44`, accent `#FFC300`.
Fontes Sora (títulos) · Inter (corpo) · JetBrains Mono (mono). CTA: **INEMA.CLUB**.
