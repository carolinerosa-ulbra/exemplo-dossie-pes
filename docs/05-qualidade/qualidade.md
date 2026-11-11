# 05. Qualidade, revisão e testes (A11, A12, A13)

## Plano de qualidade (A11)

| Característica | Subcaracterística | Por que importa | Métrica | Meta | Como verificar | Quando |
|---|---|---|---|---|---|---|
| Adequação funcional | Correção | Discussões por valor errado (R03, RK1) | Casos de teste de cobrança aprovados | 100% de CT01 a CT06 aprovados; CT09 a CT11 a partir da SM-01 | Execução dos casos de teste | Incremento 1 |
| Capacidade de interação | Facilidade de aprendizado | Fila no pico (R02) | Operadores novos que registram uma saída sem ajuda | 4 de 5 após 5 minutos de demonstração | Teste com 5 pessoas | Incremento 2 |
| Manutenibilidade | Modificabilidade e testabilidade | Preço muda todo ano (R08, RK3) | Arquivos alterados para mudar um preço | 1 arquivo | Revisão de código | Incremento 3 |

**Deixadas para depois:** Segurança (o protótipo não guarda dados pessoais além da placa); Flexibilidade (uma única cabine, console).
**Conflito identificado:** Capacidade de interação x Adequação funcional. Confirmar o valor com o operador antes de fechar o ticket evita erro, mas aumenta a fila. Decisão do PO: sem confirmação extra; o comprovante mostra o cálculo detalhado para o cliente conferir.

## Revisão (A12)

**Tipo:** inspeção do protótipo e da documentação, com checklist. **Autora:** professora. **Revisor:** revisor simulado com IA, aplicando o checklist da professora (decisão final da autora).

| ID | Artefato | Onde | Descrição | Critério violado | Severidade | Tipo | Status |
|---|---|---|---|---|---|---|---|
| D01 | Código | Construtor de Ticket | Abre ticket em vaga já ocupada; RN04 não é verificada | Toda regra Must está implementada | Crítico | Verificação | Aberto, encontrado também pelo CT07 |
| D02 | Código | Vaga.java no pacote raiz | Arquivo duplicado e vazio (record sem uso) ao lado da classe Vaga real | Não existe código morto | Maior | Verificação | Aberto (DT-01) |
| D03 | Código e modelo | TipoVaga.MENSALISTA e Veiculo.mensalista | Dois conceitos diferentes de "mensalista"; não está claro qual vale | Cada conceito tem um único significado | Maior | Validação (perguntar ao PO) | Validado: mensalista é o veículo; vaga MENSALISTA é reservada |
| D04 | README | Estrutura do projeto | Cita pasta service/ com Main.java, mas Main está no pacote raiz | Documentação corresponde ao repositório | Menor | Verificação | Corrigido na v1.0.1 |
| D05 | docs/README | Lista de arquivos | Cita AI.md e diagramas que não existem (o arquivo é IA.md) | Documentação corresponde ao repositório | Menor | Verificação | Corrigido na v1.0.1 |

## Estratégia de testes (A13)

- **Escopo:** cobrança (RF02, RN01 a RN03) e ocupação de vaga (RF01, RN04). Fora: RF03 e RF04 (ainda não implementados).
- **Nível e tipo:** teste de unidade funcional da classe Ticket; regressão de todos os casos a cada mudança na cobrança.
- **Técnicas:** análise de valor limite nos 60 e 120 minutos; partição de equivalência entre avulso e mensalista.
- **Critério de saída:** todos os casos Must executados e nenhum defeito crítico aberto.

## Casos de teste e execução

Executados em 11/11/2026 sobre o código do repositório aula-poo (commit adf2454).

| ID | Requisito | Técnica | Entrada | Resultado esperado | Resultado obtido | Status |
|---|---|---|---|---|---|---|
| CT01 | RF02, RN01 | Partição | Avulso, 30 min | R$ 4,00 | R$ 4,00 | Passou |
| CT02 | RF02, RN01 | Valor limite | Avulso, 60 min | R$ 4,00 | R$ 4,00 | Passou |
| CT03 | RF02, RN02 | Valor limite | Avulso, 61 min | R$ 10,00 | R$ 10,00 | Passou |
| CT04 | RF02, RN02 | Valor limite | Avulso, 120 min | R$ 10,00 | R$ 10,00 | Passou |
| CT05 | RF02, RN02 | Valor limite | Avulso, 121 min | R$ 16,00 | R$ 16,00 | Passou |
| CT06 | RF02, RN03 | Partição | Mensalista, 300 min | R$ 0,00 | R$ 0,00 | Passou |
| CT07 | RF01, RN04 | Negativo | Segunda entrada na vaga 7 ocupada | Entrada recusada com aviso | Entrada aceita | **Falhou (D01)** |
| CT08 | RF01 | Partição | Saída de veículo da vaga 8 | Vaga 8 disponível | Vaga 8 disponível | Passou |

**Observação sobre testabilidade:** para simular 61 minutos sem esperar uma hora, o teste precisou alterar o horário de entrada por reflexão, porque `Ticket` usa o relógio do sistema diretamente. Isso foi registrado como dívida DT-03.

**Cobertura dos requisitos Must:** RF01, RF02 e RN01 a RN05 têm pelo menos um caso de teste especificado: 7 de 7 (100%). Destes, 6 já foram executados; RN05 (CT09 a CT11) aguarda a implementação da SM-01. RF03 e RF04 sem cobertura, justificados na matriz.
