---
name: "espectador-leigo"
description: "Mostra um vídeo (curta, reel, filme) a um espectador leigo, sem nenhum contexto do roteiro, e devolve o que ele entendeu, onde se perdeu e onde pararia de assistir. Use quando pedirem leitura fria, teste de audiência ou visão de quem não conhece a história."
---

# Espectador leigo

Quem fez o filme, e quem ajudou a fazer, não consegue mais assistir como a audiência: já sabe o que cada plano quer dizer. Esta skill resolve isso entregando o vídeo a um espectador que não sabe nada — nem título, nem roteiro, nem intenção — e trazendo de volta a leitura dele, crua.

O valor todo está no isolamento. Se qualquer pista do roteiro vazar para o espectador, o teste perde o sentido.

## 1. Receber o vídeo

- Pedir o arquivo de vídeo (anexo no chat ou numa pasta conectada).
- Perguntar só uma coisa: onde o filme termina, caso o arquivo tenha making of, créditos longos ou material extra no fim. Não perguntar sobre a história.
- Não pedir roteiro nem sinopse. Se a pessoa já tiver contado a história na conversa, isso fica com você e **nunca** passa para o espectador.

## 2. Preparar o material (sem vazar nada)

Com ffmpeg e Python/PIL, numa pasta temporária de trabalho:

1. Copiar só o trecho do filme para um arquivo com nome neutro, `filme.mov` ou `filme.mp4`. O nome original pode entregar o título.
2. Gerar folhas de contato com 1 quadro por segundo, 12 quadros por folha (6 colunas × 2 linhas), cada quadro com o tempo (m:ss) marcado num canto, arquivos `folha_01.jpg`, `folha_02.jpg`… Para vídeos longos (mais de 4 minutos), usar 1 quadro a cada 2 segundos.
3. Áudio: o espectador só vê imagens. Se houver ferramenta de transcrição disponível, transcrever as falas com os tempos e salvar em `falas.txt` — é o que a audiência ouviria. Se não houver, não inventar: o espectador vai julgar só pela imagem e o relatório deve dizer isso.

Não incluir nenhum outro arquivo na pasta.

## 3. Chamar o espectador

Se houver ferramenta para lançar um subagente (Agent/Task), lançar um agente de uso geral com exatamente o prompt abaixo, trocando apenas os caminhos, a duração e a linha de áudio. **Não acrescentar nada** sobre o tema, o título, os personagens, o gênero ou o que se espera que ele perceba.

```
Você é um espectador vendo pela primeira vez um vídeo curto de [DURAÇÃO]. Não sabe nada sobre ele: nem título, nem roteiro, nem intenção de quem fez. Assista como uma pessoa comum rolando o feed e conte honestamente o que entendeu.

Material (só leitura; não procure mais nada no sistema de arquivos nem na internet sobre este vídeo):
- Folhas de contato com um quadro por segundo, em ordem, cada quadro com o tempo marcado: [PASTA]/folha_01.jpg até folha_NN.jpg. Leia todas, em ordem.
- O arquivo de vídeo, se quiser olhar algum momento de perto: [PASTA]/filme.mov (pode extrair quadros extras com ffmpeg dentro dessa mesma pasta).
- [SE HOUVER] Transcrição das falas com tempos: [PASTA]/falas.txt. [SE NÃO HOUVER] Você não ouve o áudio; diga isso e julgue só pelas imagens.

Não tente adivinhar o que o autor quis. Relate o que um espectador realmente leva. Responda em português do Brasil, em prosa, com seções curtas:
1. A história em 4 a 6 frases, como se contasse pra um amigo.
2. Quem são os personagens e o que você entende da relação entre eles.
3. O momento de virada: existe? Onde (tempo) e o que muda? Se não ficou claro, diga.
4. Onde você ficou confuso, perdido ou achou que algo estava errado (continuidade, objetos que mudam, cortes estranhos, trechos fora de ordem ou sem sentido), com tempos.
5. O que o vídeo parece querer dizer, em uma frase. Se não souber, diga.
6. O final: o que sentiu e entendeu.
7. Em que momento você teria parado de assistir no feed e por quê.

Seja franco e específico. Uma resposta confusa e honesta vale mais que uma resposta bonita.
```

### Sem subagente disponível

Se não houver como lançar um agente separado, **não fazer a leitura você mesmo** fingindo ser leigo: você já tem contexto e o teste não seria frio. Em vez disso:

1. Entregar à pessoa as folhas de contato (e `falas.txt`, se houver).
2. Entregar o prompt acima, já com os caminhos trocados por "as imagens anexadas".
3. Orientar: abrir uma conversa nova, sem projeto e sem histórico, anexar as folhas e colar o prompt.

## 4. Devolver o resultado

Apresentar o relatório do espectador separando claramente três coisas:

- **O que ele entendeu** — a história e a mensagem, nas palavras dele. Se a leitura bate com a intenção do autor, dizer isso.
- **O que ele viu que o autor não viu** — leituras erradas, confusões, sentidos indesejados (por exemplo, uma cena lida como algo que o filme não pretende). Estes vêm primeiro, porque são o motivo de fazer o teste.
- **O que ele confirmou** — problemas que já eram conhecidos.

Para cada problema, sugerir a correção mais barata (corte, ordem, cor, som, regerar um plano). Deixar claro o que foi limitação do método — por exemplo, se ele não ouviu o áudio, ou se um ponto pode ter sido causado pela preparação do material (um quadro extra no corte, por exemplo).

Fechar lembrando que o teste definitivo continua sendo gente de verdade: duas ou três pessoas que não conhecem o projeto, contando a história com as próprias palavras.

## Ao repetir o teste

Depois das correções, rodar de novo com um espectador **novo** (outro subagente, nunca o mesmo, que já viu a versão anterior) e comparar as duas leituras.