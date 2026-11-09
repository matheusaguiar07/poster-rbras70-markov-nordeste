# Cadeias de Markov para a precipitação diária no Nordeste Brasileiro

Material complementar do pôster apresentado na **70ª RBras**.

**Autores:** Matheus Dias Aguiar (apresentador) e Jáder da Silva Jale.
**Afiliação:** Programa de Pós-Graduação em Biometria e Estatística Aplicada (PPGBEA), Universidade Federal Rural de Pernambuco (UFRPE).
**Contato:** matheus.aguiar@ufrpe.br

Este repositório reúne o que o pôster remete ao QR code: o **artigo** (resumo abaixo e o pôster em PDF), o **código** (situação abaixo) e a indicação dos **dados**.

## Resumo

**Pergunta.** Como a chuva persiste ou muda de um dia para o outro no Nordeste?

**Resultado principal.** A seca persiste mais que a chuva. A probabilidade de um dia seco ser seguido de outro dia seco varia de 0,75 a 0,90 (faixa da escala do mapa), contra 0,4 a 0,6 para um dia chuvoso seguido de outro dia chuvoso.

**Dados.** Séries diárias de precipitação da grade BR-DWGD (Xavier et al., 2022), resolução de 0,1°, 12.777 séries.
Período: 1961 a 2024.

**Estados diários.**

| Estado | Precipitação diária |
|---|---|
| seco | menor que 2,5 mm |
| úmido | de 2,5 mm a menos de 5,0 mm |
| chuvoso | 5,0 mm ou mais |

**Método.** Cadeia de Markov de ordem 1: a probabilidade do dia seguinte depende só do estado do dia atual,

p(i, j) = P(X_t = j | X_(t-1) = i), com i, j em {seco, úmido, chuvoso}.

As probabilidades são estimadas pela frequência das transições em cada série. A cadeia é homogênea: as probabilidades são as mesmas em todos os anos. A análise foi feita em R.

**Como ler os mapas.** Cada ponto mostra a probabilidade de o dia seguinte ter o segundo estado, dado o estado de hoje. Em seco → seco, é a probabilidade de amanhã ser seco quando hoje foi seco.

## Resultados

| Transição | Faixa da escala do mapa |
|---|---|
| seco → seco | 0,75 a 0,90 |
| chuvoso → chuvoso | 0,4 a 0,6 |
| seco → chuvoso | 0,04 a 0,16 |
| chuvoso → seco | 0,2 a 0,5 |

As faixas são as das escalas de cores de cada mapa, e não uma estatística resumo. Cada mapa tem escala própria. Os mapas estão no pôster (`poster/`) e foram gerados pelo Prof. Jáder da Silva Jale.

**Conclusões do pôster.**
1. O estado seco é o mais persistente.
2. A permanência no estado chuvoso é menor.
3. A mudança de estado depende do lugar: seco → chuvoso é mais provável no noroeste e no litoral leste, e chuvoso → seco, no interior.

**Próximas etapas.** Cálculo sazonal e mensal, e modelo multivariado entre regiões (Ching, Ng e Fung, 2008; Elshehawey e Qian, 2023).

## Conteúdo do repositório

| Pasta | O que tem |
|---|---|
| `poster/` | Pôster em PDF (A0), com os mapas. |

## Código

O código que gerou os mapas do pôster não está disponível neste repositório. A análise está sendo reproduzida e documentada como parte de uma tese de doutorado em andamento, e o código será disponibilizado quando esse trabalho for concluído.

## Dados

Os dados são públicos e **não estão neste repositório** (cerca de 7 GB). A grade diária da BR-DWGD está disponível na página de distribuição do autor da base:

https://sites.google.com/site/alexandrecandidoxavierufes/brazilian-daily-weather-gridded-data

## Referências

CHING, W. K.; NG, M. K.; FUNG, E. S. Higher-order multivariate Markov chains and their applications. **Linear Algebra and its Applications**, v. 428, n. 2-3, p. 492-507, 2008.

ELSHEHAWEY, A. M.; QIAN, Z. A novel high-order multivariate Markov model for spatiotemporal analysis with application to COVID-19 outbreak. **Journal of the Korean Statistical Society**, v. 52, n. 3, p. 495-521, 2023.

R CORE TEAM. **R: a language and environment for statistical computing**. Vienna: R Foundation for Statistical Computing, 2025.

XAVIER, A. C.; SCANLON, B. R.; KING, C. W.; ALVES, A. I. New improved Brazilian daily weather gridded data (1961-2020). **International Journal of Climatology**, v. 42, n. 16, p. 8390-8404, 2022.