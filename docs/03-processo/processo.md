# 03. Processo e planejamento (A2, A7, A8)

## Ciclo de vida e processo

**Ciclo de vida:** incremental e iterativo (A2). As regras de cobrança estavam claras (R04), mas o gerente quer ver algo funcionando cedo para validar.

**Processo:** Kanban (A7). Com uma pessoa desenvolvendo e um PO disponível uma vez por semana, Sprints com cerimônias completas não fariam sentido. O Kanban dá visibilidade do fluxo e limita o trabalho em andamento.

| Coluna | Regra |
|---|---|
| A fazer | Itens priorizados pelo PO |
| Fazendo | Limite de 2 itens (WIP) |
| Revisão | Revisão com checklist da A12 antes de seguir |
| Teste | Casos de teste do item executados |
| Pronto | Atende à definição de pronto |

**Definição de pronto:** critérios de aceitação atendidos; casos de teste executados e registrados; matriz de rastreabilidade atualizada; nenhum defeito crítico aberto; CHANGELOG atualizado.

## Backlog, estimativas e incrementos

| Item | Prioridade | Tamanho | Incremento |
|---|---|---|---|
| RF01 Registrar entrada | Must | P | 1 |
| RF02 Calcular valor na saída | Must | M | 1 |
| RN04 Bloquear vaga ocupada | Must | P | 2 |
| RF03 Vagas disponíveis | Should | M | 2 |
| SM-01 Tolerância de 15 minutos (RN05) | Must | P | 3 |
| RF04 Alterar tabela de preços | Could | G | Depois do semestre (saiu do Incremento 3 pela SM-01) |

**Item de referência para estimar:** RF01 (P). RF02 é M porque envolve três regras e arredondamento de frações.

**Incremento 1 (valor entregue):** o operador registra entrada e saída e o sistema calcula o valor. Já resolve a principal dor (R03).
**Incremento 2:** o gerente sabe quantas vagas há livres e a vaga ocupada é protegida.
**Incremento 3:** tolerância de 15 minutos (SM-01). Os preços configuráveis (RF04) foram para o próximo ciclo; veja a decisão em 06-evolucao.

## Riscos (registro original da A8)

| ID | Risco | Probabilidade | Impacto | Mitigação |
|---|---|---|---|---|
| RK1 | Regra de arredondamento entendida errado | Média | Alto | Critérios de aceitação com valores limite validados com o PO |
| RK2 | PO indisponível na semana de entrega | Média | Médio | Reunião fixa às segundas e decisões por mensagem registradas no DEVLOG |
| RK3 | Mudança de preço antes de RF04 existir | Alta | Médio | Preços concentrados em um único lugar do código |
