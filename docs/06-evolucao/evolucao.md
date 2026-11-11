# 06. Mudança e evolução (A14, A15)

## Solicitação de mudança SM-01

| ID | Solicitante | Data | Descrição (nas palavras do solicitante) | Motivo | Urgência |
|---|---|---|---|---|---|
| SM-01 | Roberto (gerente, PO) | 05/11/2026 | "O shopping aqui do lado dá 15 minutos grátis. Tá todo mundo indo para lá só para buscar alguma coisa rápida. Preciso disso também." | Perda de clientes de curta permanência | Alta |

**Perguntas de esclarecimento:**
1. "Se o cliente ficar 16 minutos, ele paga desde o começo ou só o que passou dos 15?" Resposta: "Paga a primeira hora normal, R$ 4,00. A tolerância é só para quem sai rápido."
2. "Vale para mensalista?" Resposta: "Mensalista já não paga, não muda nada para ele."

**Linha de base antes da mudança:** release v1.0.1.

## Análise de impacto (seguindo a matriz)

| Item afetado | Como está | Mudança necessária | Esforço | Risco |
|---|---|---|---|---|
| RN05 (nova) | Não existe | "Permanência de até 15 minutos não é cobrada" | P | Baixo |
| RF02 | Calcula pela RN01 a RN03 | Passa a considerar também a RN05 | P | Baixo |
| CA02 | Três cenários | Acrescentar os cenários de 15 e 16 minutos | P | Baixo |
| Fluxograma de saída | Decisão "até 60 min?" | Nova decisão "até 15 min?" antes dela | P | Baixo |
| Ticket.calcularValor() | Regras RN01 a RN03 | Nova condição no início do cálculo | P | Médio: regressão em CT01 a CT06 |
| CT09 a CT11 (novos) | Não existem | Valor limite em 15, 16 e 0 minutos | P | Baixo |
| Plano de qualidade | Meta de correção sobre CT01 a CT06 | Meta passa a incluir CT09 a CT11 | P | Baixo |
| Backlog | RF04 no Incremento 3 | SM-01 entra no Incremento 3; RF04 vai para depois da entrega | | Médio: RK3 continua aberto |

**Conferidos e sem mudança:** RF01, RF03, RN04, CT07, CT08, arquitetura (a regra fica dentro do componente Cobrança).

## Alternativas e decisão

| Alternativa | Prós | Contras |
|---|---|---|
| Aprovar agora | Responde à concorrência; esforço pequeno | Empurra RF04 para depois da entrega |
| Adiar para depois da entrega | Mantém o plano | Perde clientes por mais um mês |
| Rejeitar | Nenhum trabalho | Problema de negócio real fica sem resposta |

**Decisão do PO (06/11/2026):** aprovar agora. **O que sai para caber:** RF04 (tabela de preços configurável) sai do Incremento 3 e vai para o roadmap "Próximo". **Versão:** v1.1.0 (MINOR, porque altera regra e requisito).

**Implementação:** documentação, critérios e casos de teste atualizados nesta versão. A alteração em `Ticket.calcularValor()` está prevista no Incremento 3 do protótipo; até lá, CT09 a CT11 ficam com status "Não executado".

| ID | Requisito | Técnica | Entrada | Resultado esperado | Status |
|---|---|---|---|---|---|
| CT09 | RN05 | Valor limite | Avulso, 15 min | R$ 0,00 | Não executado |
| CT10 | RN05, RN01 | Valor limite | Avulso, 16 min | R$ 4,00 | Não executado |
| CT11 | RN05 | Valor limite | Avulso, 0 min (entrou e saiu) | R$ 0,00 | Não executado |

## Registro de dívida técnica

| ID | Descrição | Onde | Tipo | Quadrante | Juros | Custo | Decisão | Quando |
|---|---|---|---|---|---|---|---|---|
| DT-01 | Arquivo Vaga.java duplicado e vazio no pacote raiz | Código | Código | Acidental e imprudente | Confunde quem lê; risco de importar a classe errada | P | Pagar | Agora |
| DT-02 | Preços fixos em constantes dentro de Ticket | Código | Código e arquitetura | Deliberada e prudente (registrada em RK3) | Toda mudança de preço exige programador e nova versão | M | Pagar com RF04 | Próximo |
| DT-03 | Ticket usa o relógio do sistema diretamente | Código | Testes | Acidental e prudente | Testes de tempo dependem de truques; difícil testar a SM-01 | P | Pagar | Agora, junto com a SM-01 |
| DT-04 | README e docs/README desatualizados em relação ao código | Documentação | Documentação | Acidental e imprudente | Quem chega ao projeto se perde | P | Pago na v1.0.1 | Pago |

## Riscos atualizados

| ID | Risco | Status no fim do semestre |
|---|---|---|
| RK1 | Regra de arredondamento entendida errado | Evitado: CA02 validado com o PO e CT02 a CT05 aprovados. Fechado |
| RK2 | PO indisponível na semana de entrega | Aconteceu na semana da A14; a decisão da SM-01 foi tomada por mensagem e registrada no DEVLOG. Mitigação funcionou |
| RK3 | Mudança de preço antes de RF04 existir | Aumentou: RF04 foi adiado pela SM-01. Probabilidade alta, impacto médio |
| RK4 (novo) | Concorrência muda regras de cobrança com frequência | Probabilidade média, impacto médio. Mitigação: tabela de preços configurável (RF04) como prioridade do próximo ciclo |

## Plano de manutenção

- **Como os pedidos chegam:** solicitação de mudança registrada em docs/06-evolucao, analisada pela matriz e decidida pelo PO.
- **Corretiva:** defeitos de cobrança são prioridade máxima e saem como PATCH (ex.: correção do D01).
- **Adaptativa:** mudança de preço anual (até RF04 existir, feita por manutenção no código).
- **Perfectiva:** novas regras pedidas pelo gerente, como a SM-01.
- **Preventiva:** pagamento de DT-01 e DT-03.
- **Versões:** uma release por incremento, com CHANGELOG.

## Roadmap

| Agora | Próximo | Depois |
|---|---|---|
| Corrigir D01 (vaga ocupada), crítico | RF04 tabela de preços configurável (paga DT-02, reduz RK3) | Pagamento por cartão integrado |
| Implementar SM-01 no código e executar CT09 a CT11 | RF03 vagas disponíveis por tipo | Relatório de faturamento diário |
| Pagar DT-01 e DT-03 | | |

## Lições aprendidas

Os testes de valor limite confirmaram a regra mais delicada (a fração de hora), mas foi o caso negativo CT07 que encontrou o defeito mais grave. Se começássemos de novo, escreveríamos os casos negativos das regras de negócio junto com os critérios de aceitação, ainda na A5, e não só na A13.
