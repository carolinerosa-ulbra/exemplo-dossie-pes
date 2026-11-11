# 02. Requisitos (A4, A5)

## Histórias de usuário

| ID | História | Origem |
|---|---|---|
| HU01 | Como operador, quero registrar a entrada de um veículo com placa e vaga, para saber há quanto tempo ele está estacionado. | R01 |
| HU02 | Como operador, quero que o sistema calcule o valor na saída, para cobrar sem fazer conta e sem discussão com o cliente. | R02, R03 |
| HU03 | Como gerente, quero ver quantas vagas estão livres, para avisar os condôminos. | R07 |
| HU04 | Como gerente, quero alterar a tabela de preços, para atualizar os valores no começo do ano sem depender de programador. | R08 |

## Requisitos funcionais

| ID | Requisito | HU |
|---|---|---|
| RF01 | O sistema deve registrar a entrada de um veículo com placa, vaga e horário. | HU01 |
| RF02 | O sistema deve calcular o valor a pagar no registro da saída, conforme RN01, RN02, RN03 e RN05. | HU02 |
| RF03 | O sistema deve informar a quantidade de vagas disponíveis por tipo. | HU03 |
| RF04 | O sistema deve permitir ao gerente alterar os valores da tabela de preços. | HU04 |

## Requisitos não funcionais

| ID | Requisito | Característica (ISO/IEC 25010) |
|---|---|---|
| RNF01 | O valor deve ser exibido em até 1 segundo após o registro da saída. | Eficiência de desempenho |
| RNF02 | Um operador novo deve conseguir registrar uma saída sem ajuda após 5 minutos de demonstração. | Capacidade de interação |

## Regras de negócio

| ID | Regra | Origem |
|---|---|---|
| RN01 | A primeira hora, ou fração dela, custa R$ 4,00. | R04 |
| RN02 | Cada hora adicional, ou fração dela, custa R$ 6,00. | R04 |
| RN03 | Veículo mensalista não paga na saída. | R05 |
| RN04 | Uma vaga só pode estar ocupada por um veículo de cada vez. | R06 |
| RN05 | Permanência de até 15 minutos não é cobrada; acima disso, aplicam-se RN01 e RN02 desde o início. | SM-01 (v1.1.0) |

## Critérios de aceitação (requisito prioritário)

**CA02 (RF02):**
- Dado que um veículo avulso ficou 60 minutos, quando a saída for registrada, então o valor exibido é R$ 4,00.
- Dado que um veículo avulso ficou 61 minutos, quando a saída for registrada, então o valor exibido é R$ 10,00.
- Dado que um veículo mensalista ficou 5 horas, quando a saída for registrada, então o valor exibido é R$ 0,00.
- Dado que um veículo avulso ficou 15 minutos, quando a saída for registrada, então o valor exibido é R$ 0,00. (v1.1.0, SM-01)
- Dado que um veículo avulso ficou 16 minutos, quando a saída for registrada, então o valor exibido é R$ 4,00. (v1.1.0, SM-01)

**CA01 (RF01, RN04):**
- Dado que a vaga 7 está ocupada, quando o operador tentar registrar outra entrada na vaga 7, então o sistema recusa e informa que a vaga está ocupada.

## Priorização (MoSCoW)

| Prioridade | Itens | Justificativa |
|---|---|---|
| Must | RF01, RF02, RN01 a RN05 | Sem eles não existe o fluxo de entrada e saída; resolvem as discussões (R03). RN05 entrou como Must pela SM-01 |
| Should | RF03, RNF01, RNF02 | Importantes para a fila e para o gerente, mas o fluxo funciona sem eles |
| Could | RF04 | Os preços mudam uma vez por ano; pode ser feito por manutenção até lá |
| Won't (agora) | Pagamento por cartão no sistema | Fora do escopo do semestre; a cabine já tem maquininha |
