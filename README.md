# Sistema de Estacionamento: exemplo de Dossiê de Engenharia de Software

> **Exemplo da professora** para a disciplina Processos de Engenharia de Software (ULBRA, 2026/2).
> Este dossiê é **enxuto de propósito**: mostra o formato, a ligação entre as etapas e o nível de detalhe esperado, seguindo um fio condutor (a cobrança na saída). O dossiê de vocês terá mais requisitos, mais testes e outras decisões. Use como referência, não como modelo para copiar.

**Versão atual:** v1.1.0 (veja o [CHANGELOG](CHANGELOG.md))

## O projeto em um parágrafo

Estacionamentos de shoppings, prédios comerciais e universidades controlam entradas, saídas e cobranças com papel ou planilha. Isso gera erros de cobrança, discussões e filas na saída, e ninguém sabe quantas vagas estão livres. O sistema registra entrada e saída de veículos, calcula o valor a pagar pela tabela de preços e mostra as vagas disponíveis.

## Equipe e papéis

| Pessoa | Papel |
|---|---|
| Prof.ª Caroline Pacheco da Rosa | Desenvolvedora, responsável por testes e documentação |
| Roberto (perfil fictício, gerente do estacionamento) | Product Owner: decide prioridades e aceita entregas; disponível toda segunda-feira e por mensagem durante a semana |

## Como navegar

| Pasta | O que tem |
|---|---|
| [01-descoberta](docs/01-descoberta/descoberta.md) | Problema, público, stakeholders e entrevista (R01 a R08) |
| [02-requisitos](docs/02-requisitos/requisitos.md) | Histórias de usuário, RF, RNF, regras de negócio, critérios de aceitação e priorização |
| [03-processo](docs/03-processo/processo.md) | Ciclo de vida, Kanban, papéis, backlog, incrementos, estimativas e riscos |
| [04-modelagem](docs/04-modelagem/modelagem.md) | Fluxograma da saída, diagrama de classes, arquitetura e matriz de rastreabilidade |
| [05-qualidade](docs/05-qualidade/qualidade.md) | Plano de qualidade, revisão, estratégia e casos de teste com resultados |
| [06-evolucao](docs/06-evolucao/evolucao.md) | Solicitação de mudança, dívida técnica, riscos atualizados, manutenção e roadmap |
| [DEVLOG](DEVLOG.md) | Decisões, contribuições e uso de IA |

## Protótipo

Aplicação de console em Java, no repositório [aula-poo](https://github.com/CarolCPR/aula-poo).
**Fluxo principal demonstrado:** entrada do veículo, saída e cálculo do valor (HU02, RF02, casos de teste CT01 a CT06).

## Fio condutor deste exemplo

Para ver como as etapas se conectam, siga a fala **R03** da entrevista:

R03 (entrevista) → HU02 → RF02 → RN01 e RN02 → CA02 → fluxograma da saída e classe Ticket → componente Cobrança → CT02 a CT05 → SM-01 (tolerância) → versão v1.1.0
