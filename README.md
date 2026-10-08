# espectador-leigo

Uma skill do [Claude](https://claude.com) que mostra seu vídeo — curta, Reel, trailer, o que for — a um "espectador leigo" simulado: sem título, sem roteiro, sem saber quem fez ou por quê. Ele assiste frio e devolve o que realmente entendeu, onde se perdeu, e o exato momento em que teria parado de assistir.

## Por quê

Depois que você faz um vídeo — ou ajuda a fazer — não dá mais pra assistir como audiência. Você já sabe o que cada plano quer dizer. Ferramentas de analytics dizem *onde* as pessoas saem, mas não *por quê*: foi confusão, corte estranho, virada que não ficou clara? Esta skill responde isso dando a um "espectador" fresco (um subagente de IA isolado) só folhas de contato e transcrição — sem roteiro, sem sinopse, sem pista nenhuma — e pedindo pra ele narrar o que realmente acompanhou.

## Como funciona

1. **Você entrega o vídeo.** A skill extrai folhas de contato (um quadro por segundo) e, se possível, transcrição das falas — e tira qualquer coisa que possa vazar a história (nome do arquivo, metadados).
2. **Um subagente novo assiste frio.** Ele recebe só as imagens (e a transcrição, se houver), com um prompt que não dá contexto nenhum além de "aqui está um vídeo curto, me diga o que você entendeu".
3. **Você recebe um relatório estruturado**: a história nas palavras do espectador, quem parecem ser os personagens, se a virada funcionou, onde ele se perdeu (com tempos), o que o vídeo parece querer dizer, como foi o final, e onde ele teria parado de assistir.
4. **Sugestões de correção** pra cada ponto de confusão, e dá pra repetir o teste com um espectador novo depois da edição, pra comparar as leituras.

Todo o mecanismo depende do isolamento — se qualquer informação do roteiro vazar pro espectador, o teste perde o valor. É nisso que a skill é rígida.

## Requisitos

- Um ambiente Claude capaz de rodar **skills** e lançar um **subagente** isolado (ex.: Claude Code, ou Claude com a ferramenta Agent/Task).
- `ffmpeg` e Python com PIL, pra gerar as folhas de contato.
- Opcional: alguma ferramenta de transcrição de áudio, pra incluir as falas no teste. Sem isso, o espectador julga só pela imagem — e o relatório deixa isso explícito.

## Como usar

### Com skills instaladas (Claude Code, por exemplo)

1. Baixe `SKILL.md` e salve numa pasta de skills do seu ambiente Claude (ou peça pro Claude: "cria essa skill pra mim" colando o conteúdo do arquivo).
2. Peça: "roda o espectador leigo nesse vídeo" e anexe o arquivo.

### Sem instalar nada (qualquer Claude, incluindo claude.ai)

1. Abra uma conversa nova — importante ser nova, sem histórico do projeto, senão o teste deixa de ser "leigo".
2. Cole o conteúdo de `SKILL.md` como primeira mensagem, junto com o pedido: "segue essas instruções com o vídeo que vou anexar".
3. Anexe o vídeo (ou as folhas de contato já extraídas, se preferir gerar você mesmo).
4. Aguarde a leitura fria.

## Licença

MIT — veja [LICENSE](LICENSE).

---

# espectador-leigo (English)

A [Claude](https://claude.com) skill that shows your video — short film, Reel, trailer, whatever — to a simulated "naive viewer" with **zero context**: no title, no script, no idea who made it or why. It watches cold and reports back what it actually understood, where it got confused, and the exact moment it would have scrolled away.

## Why

Once you've made a video — or helped make it — you can't watch it like an audience anymore. You already know what every shot means. Analytics tools can tell you *where* people drop off, but not *why*: was it confusing, a bad cut, an unclear turning point? This skill answers that by giving a fresh "viewer" (an isolated AI subagent) only contact sheets and a transcript — no script, no synopsis, no hints — and asking it to narrate what it actually followed.

## How it works

1. **You give it a video.** The skill extracts contact sheets (one frame per second) and, if possible, a dialogue transcript — and strips anything that could leak the story (filename, metadata).
2. **A fresh subagent watches cold.** It gets only the images (and transcript, if available), with a prompt that gives it zero context beyond "here's a short video, tell me what you understood."
3. **You get a structured report**: the story in the viewer's own words, who the characters seem to be, whether a turning point landed, where they got lost (with timestamps), what the video seems to be trying to say, how the ending felt, and where they'd have stopped watching.
4. **Fixes are suggested** for each confusion point, and you can re-run the test with a brand-new viewer after editing, to compare reads.

The whole mechanism depends on isolation — if any plot information reaches the viewer, the test is worthless. That's the part this skill is strict about.

## Requirements

- A Claude environment that can run **skills** and launch an isolated **subagent** (e.g. Claude Code, or Claude with the Agent/Task tool).
- `ffmpeg` and Python with PIL, to generate the contact sheets.
- Optional: an audio transcription tool, to include dialogue in the test. Without it, the viewer judges by image alone — and the report says so explicitly.

## How to use

### With skills installed (e.g. Claude Code)

1. Download `SKILL.md` and save it into your Claude environment's skills folder (or ask Claude: "create this skill for me" and paste the file's content).
2. Ask: "run the naive viewer test on this video" and attach the file.

### With no install (any Claude, including claude.ai)

1. Open a new conversation — it matters that it's new, with no project history, or the test stops being "naive."
2. Paste the content of `SKILL.md` as your first message, with the request: "follow these instructions with the video I'll attach."
3. Attach the video (or the already-extracted contact sheets, if you'd rather generate them yourself).
4. Wait for the cold read.

## License

MIT — see [LICENSE](LICENSE).
