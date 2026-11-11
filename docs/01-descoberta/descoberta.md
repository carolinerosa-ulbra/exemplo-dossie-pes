# 01. Descoberta (A1, A3)

## Problema

Estacionamentos controlam entradas, saídas e cobranças com papel ou planilha. Consequências relatadas pelo gerente: discussões na saída por causa do valor, filas no horário de pico e falta de informação sobre vagas livres.

## Contexto

Estacionamento de médio porte em prédio comercial, com cerca de 80 vagas, uma cabine de saída e clientes avulsos e mensalistas.

## Público (quem usa o sistema)

- **Operador de cabine:** registra entradas, saídas e cobra.
- **Motorista avulso:** paga pelo tempo de uso.
- **Motorista mensalista:** paga um valor fixo mensal e não paga na saída.

## Stakeholders (quem é afetado ou decide, além do público)

- **Gerente (Roberto):** define regras de cobrança e prioridades; atua como PO.
- **Dono do estacionamento:** paga o projeto e acompanha o faturamento.
- **Administração do prédio:** tem convênio com o estacionamento para os condôminos.
- **Legislação sobre vagas reservadas:** vagas para idosos e pessoas com deficiência precisam ser respeitadas.

> Atenção ao erro comum: o gerente não aparece em "Público" porque ele não opera o sistema no dia a dia. Ele aparece em "Stakeholders" porque decide as regras.

## Elicitação

**Técnica:** entrevista semiestruturada com o gerente, simulada com IA (prompt padrão da disciplina), complementada por observação de 20 minutos da cabine de saída no horário de pico (simulada a partir do relato).

**Por que essa técnica:** um único stakeholder com poder de decisão e pouco tempo disponível; a entrevista permite aprofundar as regras de cobrança, que são a principal fonte de conflito.

### Respostas da entrevista (falas literais numeradas)

| ID | Fala do gerente |
|---|---|
| R01 | "Hoje a gente anota a placa num caderno e o horário num ticket de papel." |
| R02 | "Na hora do almoço forma fila, o operador demora fazendo conta." |
| R03 | "O maior problema é briga na saída por causa do valor. O cliente acha que cobramos a hora cheia errado." |
| R04 | "A primeira hora é 4 reais, mesmo que fique 10 minutos. Depois é 6 reais por hora, e passou um minuto já conta outra hora." |
| R05 | "Mensalista não paga na saída, já pagou o mês." |
| R06 | "Às vezes o operador coloca dois carros na mesma vaga numerada no papel e depois ninguém sabe onde está quem." |
| R07 | "Eu queria saber de manhã quantas vagas sobraram, para avisar o pessoal do prédio." |
| R08 | "O preço muda todo começo de ano." |

### Interpretações da equipe (separadas das falas)

| ID | Interpretação | Baseada em |
|---|---|---|
| I01 | O cálculo automático do valor é a funcionalidade de maior valor, porque resolve as discussões e a fila. | R02, R03 |
| I02 | A regra de cobrança precisa estar escrita e visível, para o cliente conferir. | R03, R04 |
| I03 | Os preços não podem ficar fixos no código, porque mudam todo ano. | R08 |
