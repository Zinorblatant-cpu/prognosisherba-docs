# PrognosisHerba — Documentação técnica

> Gestão da poda de vegetação nas margens de rodovias, da medição em campo
> até a agenda das equipes. Projeto feito para o desafio da **Motiva**
> (concessionária do Rodoanel Mário Covas).

O sistema fecha um ciclo de quatro etapas, cada uma num repositório:

```
 medir  ──▶  prever  ──▶  otimizar  ──▶  executar e acompanhar
 estação     IA de        HoroHerba      painel + app das equipes
 webcam      crescimento  (PLI)
```

| Etapa | Repositório |
|---|---|
| Medir | [prognosisherba-visao](https://github.com/Zinorblatant-cpu/prognosisherba-visao) |
| Prever | [IAs---Challenge-Motiva](https://github.com/Felipek06/IAs---Challenge-Motiva) |
| Otimizar | [prognosisherba-api](https://github.com/Zinorblatant-cpu/prognosisherba-api) |
| Planejar e acompanhar | [prognosisherba-painel](https://github.com/Zinorblatant-cpu/prognosisherba-painel) |
| Executar em campo | [prognosisherba-podadores](https://github.com/Zinorblatant-cpu/prognosisherba-podadores) |

| Documento | Conteúdo |
|---|---|
| [01 · Visão geral](01-visao-geral.md) | O problema da Motiva, a solução e o fluxo de uso |
| [02 · Arquitetura de software](02-arquitetura.md) | Contexto, containers, componentes, sequência, dados, deploy e decisões |
| [03 · Modelo matemático](03-modelo-matematico.md) | Medição por visão computacional (incluindo a grade em cm e o teorema de Pick), previsão por *gradient boosting*, derivação dos prazos, modelo de programação linear inteira e clusterização |
| [04 · Repositórios](04-repositorios.md) | Os repositórios, os contratos entre eles e como foram separados |
| [Apresentação](apresentacao/apresentacao.html) | Slides da apresentação do projeto (baixe e abra no navegador) |

As fórmulas usam a sintaxe LaTeX (`$…$` e `$$…$$`), que o GitHub
renderiza direto no Markdown. Os diagramas usam Mermaid, que o GitHub
também renderiza.

## Glossário rápido

| Termo | Significado |
|---|---|
| **Região / local** | Trecho da rodovia com uma estação de medição (`RA-01` … `RA-04`). No solver, cada região que precisa de poda vira um *local* $a \in A$ |
| **Limiar de poda** | Altura a partir da qual o trecho entra na fila de poda ($L$, hoje 9,0 cm no backend) |
| **Prazo** | Primeira semana em que a previsão cruza o limiar (`dataAlvo`) |
| **Horótima** | Nome da variável binária $H_{a,c,d}$ do modelo de otimização, herdado da família de solvers Horótimo |
| **HoroHerba / Horoprognosis** | O modelo de alocação das equipes. "HoroHerba" é o nome usado na apresentação; `horoprognosis.py` é o nome no código |
| **Capacidade diária** | Orçamento de esforço de uma equipe por dia ($K = 3$ pontos) |
| **Folga** | Dias entre o dia agendado e o prazo do local |
| **Grade** | Pontos a cada 0,5 cm gravados na calibração, com origem no chão; dão a distância em cm de qualquer pixel |
| **Grama maior** | Faixa do quadro com maior altura média, medida pelo teorema de Pick ($A = I + B/2 - 1$) |
