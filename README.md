# Construindo um Processador MIPS no Logisim Evolution

Este repositório contém a implementação prática de um **processador baseado na arquitetura MIPS** desenvolvido no simulador Logisim Evolution. O projeto é resultado das aulas práticas da disciplina GCC194 - Arquitetura de Computadores, que abordam desde os conceitos básicos de lógica digital até a construção completa de um processador funcional.

## 🎯 Objetivo

Apresentar de forma didática e visual o funcionamento interno de um processador, implementando os principais componentes: **Program Counter (PC)**, **Memória de Instruções**, **Banco de Registradores**, **ULA (Unidade Lógica e Aritmética)** e **Memória de Dados**.

## 📋 Estrutura do Projeto

O projeto foi desenvolvido em quatro etapas principais, correspondentes às partes da série de vídeos:

### 🔹 Parte 1 – PC e Memória de Instruções
- Introdução ao simulador Logisim Evolution
- Revisão de conceitos fundamentais de circuitos digitais
- Implementação do **Program Counter (PC)** e da **memória de instruções**
- Funcionamento do clock, endereço de instrução e fluxo básico de execução

### 🔹 Parte 2 – Banco de Registradores
- Criação do **banco de registradores** com múltiplos registradores de 8 bits
- Funcionamento do flip-flop tipo D e sua aplicação na construção dos registradores
- Leitura e escrita em registradores via sinais de controle (`RegWrite`)
- Interligação com o PC e preparação para comunicação com a ULA

### 🔹 Parte 3 – ULA e Memória de Dados
- Implementação da **Unidade Lógica e Aritmética (ULA)**
- Operações básicas: soma, subtração e operações lógicas (AND, OR, etc.)
- Criação e integração da **memória de dados**
- Demonstração do ciclo completo de execução de instruções

### 🔹 Parte 4 – Integração e Controle
- Conexão de todos os módulos do processador
- Implementação da unidade de controle
- Execução de programas completos no processador integrado

## 🏗️ Diagrama de Blocos

```
Program Counter (PC) → Memória de Instruções → Banco de Registradores
       ↓                    ↓                       ↓
Unidade de Controle → ULA → Memória de Dados → Resultado/Saída
```

## ⚙️ Módulos Implementados

### 1. Program Counter (PC) e Memória de Instruções
- **PC**: Registrador que armazena o endereço da próxima instrução
- **Memória de Instruções**: ROM que contém o programa em código de máquina
- **Incrementador**: Soma +1 ao PC para próxima instrução sequencial
- **Controle de desvios**: Capacidade de saltos condicionais e incondicionais

### 2. Banco de Registradores
- 8 registradores de 8 bits cada
- Leituras duplas simultâneas (Read Data 1 e Read Data 2)
- Escrita síncrona controlada por sinal `RegWrite`
- Endereçamento por código binário (3 bits para 8 registradores)

### 3. Unidade Lógica e Aritmética (ULA)
- **Operações aritméticas**: Soma, subtração, multiplicação, divisão
- **Operações lógicas**: AND, OR, XOR, NOT
- **Operações de deslocamento**: Shift left, shift right
- **Flags de status**: Zero, negativo, overflow
- Entrada de função de 3 bits para seleção da operação

### 4. Memória de Dados
- Memória RAM para armazenamento de variáveis e dados
- Acesso por endereço de 8 bits
- Controle de leitura/escrita
- Integração direta com a ULA e banco de registradores

### 5. Unidade de Controle
- Decodificação de instruções (opcode e funct)
- Geração de sinais de controle para todos os módulos
- Sincronização com clock global do sistema

## 🔧 Ferramentas Utilizadas

- **Logisim Evolution** - simulador digital para projeto e teste de circuitos
- **Java Runtime** - necessário para executar o Logisim
- Arquitetura MIPS simplificada de 8 bits

## 🧠 Conceitos Envolvidos

- Portas lógicas (AND, OR, NOT, XOR)
- Multiplexadores e demultiplexadores
- Flip-flops tipo D
- Contador de programa (PC)
- Banco de registradores
- Unidade Lógica e Aritmética (ULA)
- Memória de instruções e memória de dados
- Ciclo de clock e controle de fluxo
- Decodificação de instruções

## 🚀 Como Executar

1. Baixe e instale o **Logisim Evolution** (versão 3.8.0 ou superior)
2. Abra o arquivo do projeto (.circ) no simulador
3. Ative o modo de simulação usando o controle de clock
4. Observe o fluxo dos dados entre os componentes:
   - O PC fornece o endereço da próxima instrução
   - A memória de instruções envia o código para decodificação
   - O banco de registradores fornece os operandos para a ULA
   - A ULA processa e devolve o resultado
   - O valor final é armazenado na memória de dados ou nos registradores

## 📚 Referências

- Patterson, D. A.; Hennessy, J. L. - *Computer Organization and Design: The Hardware/Software Interface*
- Nand2Tetris: *Building a Modern Computer from First Principles*
- MIPS Architecture Reference Manual
- Vídeos da série **GCC194 - Construindo um Processador AO VIVO**

## 👥 Integrantes do Projeto

- Aline Cristina Ribeiro de Barros – RA: 081230021
- Luis Gustavo de Oliveira Carneiro – RA: 081230029
- Roger Rocha da Silva – RA: 081230045
- João Victor Pereira Andrade – RA: 081230010

## 📄 Licença

Este projeto é de uso acadêmico e livre para consulta e aprendizado, conforme os princípios de uso educacional da disciplina GCC194.

**Março de 2025**
