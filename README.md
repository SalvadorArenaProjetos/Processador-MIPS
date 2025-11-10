Construção de um Processador MIPS no Logisim Evolution

Este projeto apresenta a construção de um processador baseado na arquitetura MIPS (Microprocessor without Interlocked Pipeline Stages) utilizando o simulador Logisim Evolution. Ele foi desenvolvido como parte da disciplina GCC194 – Arquitetura de Computadores e demonstra, de forma prática, os princípios fundamentais de um processador RISC (Reduced Instruction Set Computer).

Objetivos do Projeto

Entender o funcionamento interno de um processador em nível de hardware.

Projetar e implementar cada módulo do processador MIPS simplificado.

Simular o ciclo completo de execução de instruções: busca, decodificação, execução, acesso à memória e escrita no registrador.

Consolidar os conceitos teóricos de arquitetura de computadores através da implementação prática em circuito digital.

Estrutura do Projeto

O processador foi desenvolvido em quatro etapas principais, baseadas nas transmissões da série “GCC194 – Construindo um Processador ao Vivo”, com a criação de módulos independentes e integração final.

graph TD
    A[Program Counter (PC)] --> B[Memória de Instruções]
    B --> C[Banco de Registradores]
    C --> D[ULA - Unidade Lógica e Aritmética]
    D --> E[Memória de Dados]
    E --> F[Resultado / Saída]
    D -->|Sinais de Controle| G[Unidade de Controle]
    G -->|OpCode / Funct| D
    G -->|Controle de Fluxo| A

Módulos do Processador
1. Program Counter (PC) e Memória de Instruções

O Program Counter é o responsável por armazenar o endereço da próxima instrução a ser executada.
A Memória de Instruções contém o conjunto binário de instruções que o processador deve executar.

graph LR
    CLK[Clock] --> PC[Registrador - Program Counter]
    PC --> INC[Incrementador (+1)]
    INC --> MUX[MUX - Seleção de Endereço]
    MUX --> ROM[Memória de Instruções]
    ROM --> IR[Registrador de Instrução]
    MUX -->|Sinal de Desvio| JMP[Endereço de Salto]


Funções principais:

Incremento automático do contador a cada ciclo.

Capacidade de salto para execução de instruções condicionais.

Leitura contínua de instruções armazenadas em memória ROM.

2. Banco de Registradores

O Banco de Registradores é responsável pelo armazenamento temporário de dados e resultados intermediários.
Ele utiliza múltiplos registradores de 8 bits com endereçamento seletivo.

graph LR
    A[Endereço de Leitura 1] --> DEC1[Decodificador]
    B[Endereço de Leitura 2] --> DEC2[Decodificador]
    C[Endereço de Escrita] --> DEC3[Decodificador]
    DEC1 --> REGS[Registradores de 8 bits]
    DEC2 --> REGS
    DEC3 --> REGS
    REGS --> MUX1[Saída Leitura 1]
    REGS --> MUX2[Saída Leitura 2]
    MUX1 --> ULA[Entrada A]
    MUX2 --> ULA[Entrada B]


Características principais:

Leituras duplas simultâneas e escrita síncrona.

Cada registrador é endereçado por código binário.

Comunicação direta com a ULA.

3. Unidade Lógica e Aritmética (ULA)

A ULA realiza as operações matemáticas e lógicas com base nos sinais de controle vindos da unidade de controle.

graph TD
    A[Entrada A] --> ALU[ULA]
    B[Entrada B] --> ALU
    CTRL[Sinal de Controle] --> ALU
    ALU --> OUT[Saída do Resultado]
    ALU --> FLAG[Flags: Zero / Negativo / Overflow]


Operações implementadas:

Soma e subtração.

AND, OR, XOR e NOT.

Comparações e definição de flags.

A ULA também gera sinais para controle de fluxo condicional e escrita em registradores.

4. Memória de Dados

A Memória de Dados armazena informações manipuladas durante a execução de instruções.
Sua integração com a ULA permite leitura e escrita condicionadas por sinais de controle.

graph LR
    ADDR[Endereço de Memória] --> MEM[Memória RAM]
    DATAIN[Entrada de Dados] --> MEM
    MEM --> DATAOUT[Saída de Dados]
    CTRL[Sinal de Leitura/Escrita] --> MEM


Características:

Organização por endereços de 8 bits.

Controle de leitura (Read Enable) e escrita (Write Enable).

Interligação direta com o banco de registradores e a ULA.

5. Unidade de Controle

A Unidade de Controle coordena todo o funcionamento do processador, gerando sinais que definem as operações da ULA, acessos à memória e atualizações de registradores.

graph TD
    IR[Registrador de Instrução] --> DEC[Decodificador de OpCode]
    DEC --> CTRL[Gerador de Sinais de Controle]
    CTRL --> ULA
    CTRL --> MEM
    CTRL --> REG
    CTRL --> PC


Responsabilidades:

Interpretar o campo opcode e funct das instruções.

Gerar sinais de controle apropriados para cada etapa do ciclo de instrução.

Sincronizar as operações com o clock global do sistema.

6. Integração do Sistema

Na fase final do projeto, todos os módulos foram conectados para formar um processador funcional MIPS simplificado, capaz de executar instruções de forma sequencial e condicional.

graph TD
    PC[Program Counter] --> MEMI[Memória de Instruções]
    MEMI --> IR[Registrador de Instrução]
    IR --> CTRL[Unidade de Controle]
    CTRL --> ALU
    CTRL --> MEMD[Memória de Dados]
    CTRL --> REGS[Banco de Registradores]
    REGS --> ALU
    ALU --> REGS
    ALU --> MEMD

Simulação e Testes

Os testes foram realizados no Logisim Evolution, validando a execução de instruções básicas como:

Operações aritméticas (ADD, SUB).

Operações lógicas (AND, OR).

Leitura e escrita em memória.

Desvios condicionais baseados em flags.

O processador foi simulado passo a passo, observando a propagação de sinais, atualização de registradores e mudanças no fluxo de execução.

Ferramentas e Requisitos

Logisim Evolution (versão 3.8.0 ou superior).

Arquitetura MIPS simplificada de 8 bits.

Sistema operacional compatível: Windows, Linux ou macOS.

Referências

Patterson, D. A.; Hennessy, J. L. – Computer Organization and Design: The Hardware/Software Interface.

Nand2Tetris: Building a Modern Computer from First Principles.

MIPS Architecture Reference Manual.

Vídeos da série GCC194 – Construindo um Processador ao Vivo (YouTube).

Integrantes do Projeto

Aline Cristina Ribeiro de Barros – RA: 081230021

Luis Gustavo de Oliveira Carneiro – RA: 081230029

Roger Rocha da Silva – RA: 081230045

João Victor Pereira Andrade – RA: 081230010

Licença

Este projeto é de uso acadêmico e livre para consulta e aprendizado, conforme os princípios de uso educacional da disciplina GCC194.

Março de 2025
