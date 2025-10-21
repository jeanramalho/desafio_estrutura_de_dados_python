# Desafio: Otimização do Sistema Bancário em Python

## Sobre o repositório

Este repositório contém uma versão simples de um Sistema Bancário em Python criado como desafio de estruturas de dados e refatoração usando funções. O objetivo do desafio é organizar as operações bancárias (depósito, saque e extrato) em funções reutilizáveis, tornando o código mais legível, modular e fácil de manter.

Sumário

- Visão geral
- Objetivos do desafio
- Funcionalidades implementadas
- Estrutura do projeto
- Requisitos
- Como executar
- Exemplos de uso
- Contrato das funções principais
- Casos de borda e validações
- Possíveis melhorias
- Contribuindo
- Licença

## Visão geral

O programa implementa uma interface de linha de comando (CLI) que permite criar usuários e contas, realizar depósitos e saques, e consultar o extrato. A lógica principal está em `desafio.py` e foi organizada em funções para cada operação.

## Desafio

Neste desafio, você terá a oportunidade de otimizar o Sistema Bancário previamente desenvolvido com o uso de funções Python. O objetivo é aprimorar a estrutura e a eficiência do sistema, implementando as operações de depósito, saque e extrato em funções específicas. Você terá a chance de refatorar o código existente, dividindo-o em funções reutilizáveis, facilitando a manutenção e o entendimento do sistema como um todo. Prepare-se para aplicar conceitos avançados de programação e demonstrar sua habilidade em criar soluções mais elegantes e eficientes utilizando Python.

## Objetivos do desafio

- Refatorar o sistema bancário utilizando funções Python.
- Tornar as operações (depósito, saque, extrato) reutilizáveis e testáveis.
- Demonstrar boas práticas de documentação e contratos de função.

## Funcionalidades implementadas

- Criar usuário (`nu`).
- Criar conta vinculada a usuário (`nc`).
- Listar contas (`lc`).
- Depositar (`d`).
- Sacar (`s`) com limite por saque e limite de número de saques.
- Exibir extrato (`e`).
- Encerrar o programa (`q`).

## Estrutura do projeto

- `desafio.py` - Implementação principal com todas as funções e loop interativo.

## Requisitos

- Python 3.8+ (testado com Python 3.x)

## Como executar

Abra um terminal (zsh no macOS) e execute:

```bash
python3 desafio.py
```

O programa é interativo. Após executar, o menu exibirá as opções disponíveis. Siga as instruções no terminal para fornecer valores e informações.

## Exemplos de uso (fluxo interativo)

1. Criar usuário: selecione `nu` e informe CPF, nome, data de nascimento e endereço.
2. Criar conta: selecione `nc` e informe o CPF do usuário já criado.
3. Depositar: selecione `d` e informe o valor (positivo).
4. Sacar: selecione `s` e informe o valor (obedecendo limites e número máximo de saques).
5. Extrato: selecione `e` para visualizar as transações e o saldo.

> Observação: os prompts e mensagens são exibidos em português no terminal.

## Contrato das funções principais

Abaixo está um resumo simples das funções centrais presentes em `desafio.py` (nomes, entradas, saídas e comportamento esperado):

- depositar(saldo, valor, extrato, /) -> (saldo, extrato)
  - Entrada:
    - saldo (float): saldo atual da conta.
    - valor (float): valor a ser depositado (deve ser > 0).
    - extrato (str): string acumuladora do extrato.
  - Saída:
    - saldo atualizado (float) e extrato atualizado (str).
  - Erros/validações:
    - Se `valor <= 0`, não altera saldo e imprime mensagem de erro.

- sacar(*, saldo, valor, extrato, limite, numero_saques, limite_saques) -> (saldo, extrato)
  - Entrada (apenas por keyword args):
    - saldo (float): saldo atual.
    - valor (float): valor a sacar.
    - extrato (str): string do extrato.
    - limite (float): limite máximo por saque.
    - numero_saques (int): contador de saques já realizados.
    - limite_saques (int): número máximo de saques permitidos.
  - Saída:
    - saldo atualizado (float) e extrato atualizado (str).
  - Erros/validações:
    - Verifica insuficiência de saldo, se valor excede limite e se já atingiu número máximo de saques.
    - Se `valor <= 0`, rejeita a operação.
  - Observação importante:
    - A implementação atual incrementa `numero_saques` internamente, mas não o retorna ao chamador. Para que o contador tenha efeito persistente na execução, é necessário retornar `numero_saques` ou usar um objeto mutável/estado compartilhado.

- exibir_extrato(saldo, /, *, extrato) -> None
  - Entrada:
    - saldo (float), extrato (str)
  - Comportamento:
    - Imprime o extrato (ou mensagem quando vazio) e o saldo formatado.

- criar_usuario(usuarios) -> None
  - Entrada:
    - usuarios (list): lista que será modificada (apêndice do novo usuário).
  - Comportamento:
    - Lê dados via input e adiciona um dicionário representando o usuário.

- criar_conta(agencia, numero_conta, usuarios) -> dict | None
  - Entrada:
    - agencia (str), numero_conta (int), usuarios (list)
  - Saída:
    - Dicionário com dados da conta ou `None` se o usuário não for encontrado.

## Casos de borda e validações

- Depósito com valor não positivo: rejeitado.
- Saque com valor maior que saldo: rejeitado.
- Saque com valor maior que limite por saque: rejeitado.
- Saque com número de saques excedido: rejeitado (ver Observação no contrato sobre o contador).
- Criação de usuário com CPF já existente: rejeitada.

## Possíveis melhorias (próximos passos)

1. Corrigir o fluxo de `numero_saques`: retornar o novo contador de `sacar` para que o valor persistente seja atualizado no `main`.
2. Separar a lógica de IO (inputs/prints) da lógica de negócio para facilitar testes automatizados.
3. Adicionar testes unitários (pytest) cobrindo depósitos, saques e extratos.
4. Persistência simples (JSON/SQLite) para manter usuários/contas entre execuções.
5. Implementar tratamento de entradas inválidas (try/except) para evitar crash quando o usuário digita texto onde se espera número.
6. Adicionar cobertura e integração contínua (GitHub Actions).

## Licença

Este repositório está disponível sob a licença MIT — consulte o arquivo `LICENSE` (se aplicável) para mais detalhes.

---
