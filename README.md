# Cassandra · auditoria pública das previsões

Este repositório guarda, todo dia, a **impressão digital (hash SHA-256) de cada previsão** publicada pelo
[Cassandra](https://cassandra.news): Noticiário (tendências e previsões com %), Mercado Financeiro e Cripto.

O objetivo é simples: provar que **nenhuma previsão foi alterada depois** de publicada. Se uma previsão
mudasse, o hash dela no dia seguinte seria diferente, e a diferença ficaria visível aqui para sempre.

## O que tem em cada dia (`selos/AAAA-MM-DD/`)

| Arquivo | Conteúdo |
| --- | --- |
| `noticiario.txt` | uma linha por tendência do Noticiário: `N-<nº>` e o hash |
| `previsoes.txt` | uma linha por previsão com % (pergunta sobre o que ainda não aconteceu): `N-<nº>-P<efeito>` e o hash |
| `mercado.txt` | uma linha por ativo de cada previsão do Mercado: `M-<nº>-<ticker>` e o hash |
| `cripto.txt` | uma linha por moeda de cada leitura da Cripto: `C-<nº>-<moeda>` e o hash |
| `raiz.txt` | o hash de cada arquivo, a quantidade de linhas e a **RAIZ** do dia |
| `raiz.txt.ots` | carimbo de tempo [OpenTimestamps](https://opentimestamps.org) da raiz, ancorado no Bitcoin |

Só os hashes são publicados — o texto das previsões continua no site (parte dele é exclusiva para assinantes).

## O que o hash cobre

Só **o que foi previsto**: texto, chance/probabilidade, direção, faixa, prazo e hora de criação.
O resultado (acertou/errou) não entra: ele é público em cassandra.news/resultados. Por isso o hash de uma
previsão não muda quando ela é conferida.

Quando um hash muda de um dia para o outro, há duas explicações possíveis, e as duas ficam registradas:
1. **Revisão automática da IA antes do prazo começar** — mostrada no card da previsão.
2. **Correção feita à mão** (ex.: texto com nome errado) — listada em cassandra.news/auditoria, com o motivo.

## Como conferir uma previsão

1. Peça ao Cassandra o registro da previsão (JSON).
2. Monte o registro canônico: chaves em ordem alfabética, sem espaços, números como no JSON.
3. Calcule o SHA-256 e compare com a linha do código no arquivo do dia.
4. Para conferir a data: `ots verify selos/AAAA-MM-DD/raiz.txt.ots`.

Nem toda previsão acerta. Não é recomendação de investimento.
