---
name: grill-ptbr
description: Questione o usuário implacavelmente para aprimorar e testar sob pressão um plano, decisão, ideia ou design. Use quando o usuário quiser validar seu raciocínio, encontrar pontos fracos ou usar gatilhos relacionados a "grill".
disable-model-invocation: true
---

# Grill PT-BR

Entreviste o usuário implacavelmente até chegar a um entendimento compartilhado. Esta skill reúne em um único fluxo o comportamento de `grill-me` e sua dependência `grilling`.

Mapeie a conversa como uma **árvore de decisões**: cada decisão se ramifica nas decisões que dependem dela.

## Rodadas e fronteira

Trabalhe a árvore em **rodadas**. A **fronteira** é o conjunto de todas as decisões cujos pré-requisitos já foram resolvidos — as perguntas que você pode fazer _agora_ sem adivinhar respostas que ainda não ouviu.

Faça toda a fronteira em uma rodada: numere cada pergunta e dê sua resposta recomendada. Depois, aguarde as respostas do usuário antes da próxima rodada.

Cada pergunta deve ser formatada assim:

```
❓ **Q1** - **<título da pergunta>**: <corpo da pergunta, que pode ter vários parágrafos e várias opções>

➡️ <sua resposta recomendada>
```

## Recalcular a árvore

A cada rodada, as respostas do usuário remodelam a árvore. Decisões resolvidas empurram a fronteira para fora e desbloqueiam perguntas que dependiam delas.

Recalcule a fronteira e faça a próxima rodada. Uma pergunta cuja resposta depende de outra pergunta ainda aberta nesta rodada pertence a uma rodada _posterior_, não a esta.

## Fatos são responsabilidade do agente

Encontrar _fatos_ é sua responsabilidade, nunca a do usuário. Quando uma pergunta da fronteira precisar de um fato do ambiente — sistema de arquivos, ferramentas, código, documentação ou outras fontes disponíveis — procure esse fato por conta própria ou envie um subagente para encontrá-lo.

Não pergunte ao usuário algo que você mesmo possa consultar.

Não bloqueie o restante da entrevista enquanto uma exploração estiver em andamento. Uma exploração pendente é apenas um pré-requisito ainda não resolvido; somente as perguntas que dependem dela devem esperar. Faça imediatamente o restante da fronteira.

Os _fatos_ são responsabilidade do agente. As _decisões_ pertencem ao usuário: apresente cada decisão a ele e aguarde sua resposta.

## Quando terminar

A sessão termina quando a fronteira estiver vazia: todos os ramos relevantes da árvore de decisões foram visitados e nada ficou silenciosamente presumido.

Não execute o plano ou tome ações decorrentes dele até que o usuário confirme que vocês chegaram a um entendimento compartilhado.
