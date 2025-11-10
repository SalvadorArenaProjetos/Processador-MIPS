# Construção de um Processador MIPS no Logisim Evolution

Este repositório apresenta a construção e documentação de um processador baseado na arquitetura MIPS, implementado no simulador **Logisim Evolution**.  
O projeto foi desenvolvido como parte da disciplina **GCC194 – Arquitetura de Computadores**, e busca demonstrar de maneira prática e visual os princípios fundamentais que regem o funcionamento interno de processadores baseados em arquitetura RISC (Reduced Instruction Set Computer).

---

## 1. Introdução

A arquitetura MIPS é amplamente utilizada em ambientes educacionais por sua estrutura limpa, modular e orientada a instruções simples.  
Seu conjunto de instruções reduzido e padronizado torna possível compreender, de forma incremental, como dados e instruções são processados, desde o nível lógico até a execução.

O projeto aqui apresentado foi desenvolvido inteiramente no Logisim Evolution, com o objetivo de **reproduzir as etapas essenciais da arquitetura MIPS** — desde o **Program Counter (PC)** e a **Memória de Instruções** até a **Unidade Lógica e Aritmética (ULA)** e a **Memória de Dados** — integrando todos os módulos para formar um processador funcional capaz de executar instruções básicas.

---

## 2. Objetivos

- Compreender o funcionamento de um processador RISC em nível de hardware lógico.  
- Desenvolver, de forma modular, os principais componentes que compõem a arquitetura MIPS.  
- Integrar todos os módulos em um único circuito funcional.  
- Simular o ciclo de instrução completo: **busca**, **decodificação**, **execução**, **memória** e **escrita de resultado**.  
- Relacionar conceitos teóricos de arquitetura de computadores com a prática de implementação digital.  

---

## 3. Estrutura do Projeto

O projeto foi desenvolvido em quatro etapas principais, baseadas nas transmissões da série **“GCC194 – Construindo um Processador ao Vivo”**.  
Cada parte foi responsável pela implementação e explicação detalhada de um módulo fundamental.

---

### Parte 1 – Program Counter e Memória de Instruções

Nesta etapa inicial, foi feita a introdução ao **Logisim Evolution** e aos blocos básicos da lógica digital.  
O foco esteve na construção do **contador de programa (PC)** e da **memória de instruções**, responsáveis pela etapa de **busca** do ciclo de instruções.

**Conceitos e implementações abordadas:**
- Revisão dos princípios de lógica combinacional e sequencial.  
- Implementação do **PC (Program Counter)** utilizando registradores de 8 bits e controle de clock.  
- Criação da **Memória de Instruções** por meio de um bloco de memória ROM configurável.  
- Introdução ao conceito de **endereçamento sequencial de instruções** e atualização do PC.  
- Aplicação de sinais de controle para **incremento automático do PC** a cada ciclo de clock.  
- Testes de funcionamento com instruções representadas em **código binário**.  

O resultado desta fase é um circuito capaz de buscar instruções armazenadas sequencialmente na memória, simulando a primeira etapa do funcionamento de um processador real.

---

### Parte 2 – Banco de Registradores

A segunda parte foi dedicada à construção do **Banco de Registradores**, responsável por armazenar temporariamente os dados manipulados pela ULA e pelas instruções.

**Principais tópicos desenvolvidos:**
- Introdução ao conceito de **registradores de propósito geral**.  
- Criação de registradores de 8 bits utilizando **flip-flops tipo D**.  
- Utilização de **demultiplexadores** e **multiplexadores** para controlar quais registradores são lidos e escritos.  
- Implementação do sinal **RegWrite**, que habilita a escrita apenas quando necessário.  
- Estrutura de leitura simultânea de dois registradores (Read Data 1 e Read Data 2).  
- Demonstração prática de operações de leitura e escrita utilizando o Logisim.  

Esta fase consolidou a base de manipulação de dados, permitindo que valores pudessem ser armazenados e recuperados de forma controlada.  
O banco de registradores se tornou o ponto de interligação entre o PC, a memória e a ULA.

---

### Parte 3 – Unidade Lógica e Aritmética (ULA) e Memória de Dados

A terceira etapa abordou dois dos blocos mais importantes da arquitetura MIPS: a **Unidade Lógica e Aritmética (ULA)** e a **Memória de Dados**.

**Implementações e conceitos trabalhados:**
- Estrutura interna da **ULA**, com operações básicas de soma, subtração, AND, OR, XOR e comparação (Set on Less Than).  
- Construção de circuitos combinacionais para seleção da operação a ser executada.  
- Implementação de um **multiplexador de controle da ULA**, selecionando a operação conforme o código de função da instrução.  
- Integração da ULA com o Banco de Registradores, permitindo operações diretas entre registradores.  
- Criação da **Memória de Dados**, responsável por armazenar os resultados de operações e variáveis utilizadas em instruções do tipo load/store.  
- Simulação completa de um ciclo de execução: leitura de dados, operação lógica ou aritmética e gravação do resultado.  

Nesta fase, o processador passou a ter capacidade de realizar **operações aritméticas completas**, simulando o comportamento de instruções MIPS como `ADD`, `SUB`, `AND`, `OR` e `LW/SW`.

---

### Parte 4 – Unidade de Controle e Integração Final

Na última fase (mencionada nos vídeos subsequentes), os módulos construídos foram integrados e coordenados por uma **Unidade de Controle**.  
Essa unidade é responsável por gerar todos os sinais de controle necessários para o funcionamento sincronizado do processador.

**Elementos principais da integração:**
- Criação da **Main Control Unit**, responsável pela geração dos sinais de controle com base no opcode das instruções.  
- Implementação da **ALU Control Unit**, que decodifica o campo “funct” e define a operação a ser executada pela ULA.  
- Integração dos caminhos de dados entre todos os módulos: PC → Memória de Instruções → Banco de Registradores → ULA → Memória de Dados.  
- Demonstração do **caminho completo de execução**: a instrução é buscada, decodificada, executada e o resultado armazenado.  
- Testes práticos com instruções completas em formato binário, simulando pequenos programas no Logisim.  

Com a integração final, o circuito passou a representar um **processador funcional simplificado**, capaz de executar um subconjunto significativo do conjunto de instruções MIPS.

---

## 4. Ferramentas Utilizadas

- **Logisim Evolution** – Simulador de circuitos digitais usado para o desenvolvimento e testes.  
- **Java Runtime Environment (JRE)** – Necessário para execução do Logisim.  
- **Editor de texto** – Utilizado para documentação e codificação das instruções em formato binário.  
- **Material de referência:** Patterson, D. A., & Hennessy, J. L. *Computer Organization and Design – The Hardware/Software Interface.*

---

## 5. Conceitos Fundamentais Aplicados

Durante o desenvolvimento do projeto, foram abordados e aplicados os seguintes conceitos:

- Lógica combinacional e sequencial  
- Portas lógicas (AND, OR, XOR, NOT)  
- Multiplexadores e demultiplexadores  
- Flip-flops tipo D e registradores  
- Contador de Programa (Program Counter)  
- Banco de Registradores  
- Unidade Lógica e Aritmética (ULA)  
- Memória de Instruções e de Dados  
- Ciclo de Clock e sincronização  
- Unidade de Controle (Main Control e ALU Control)  
- Caminho de Dados (Datapath)  
- Arquitetura RISC  

---

## 6. Execução do Projeto no Logisim Evolution

1. Abra o Logisim Evolution.  
2. Importe o arquivo `.circ` referente ao módulo desejado ou ao processador completo.  
3. Ative a simulação em “Ticks Enabled”.  
4. Observe o fluxo de dados:
   - O PC gera o endereço da instrução.  
   - A Memória de Instruções fornece a instrução ao Banco de Registradores e à ULA.  
   - A ULA processa a operação e envia o resultado à Memória de Dados.  
   - O PC é atualizado para a próxima instrução.  

Durante a execução, cada componente pode ser analisado individualmente, permitindo a compreensão detalhada de cada etapa do ciclo de instruções.

---

## 8. Referências

- Patterson, D. A., & Hennessy, J. L. *Computer Organization and Design – The Hardware/Software Interface.*  
- Stallings, W. *Computer Organization and Architecture – Designing for Performance.*  
- Série de vídeos **GCC194 – Construindo um Processador ao Vivo**:  
  1. [Parte 1 – PC e Memória de Instruções](https://youtu.be/7lCClSY4sHc)  
  2. [Parte 2 – Banco de Registradores](https://youtu.be/HUPdAYDyIAM)  
  3. [Parte 3 – ULA e Memória de Dados](https://youtu.be/Un2CYoah8tw)  
  4. [Parte 4 – Integração e Controle](https://youtu.be/20LTwGX14Qs)

---

## 9. Integrantes

Aline Cristina Ribeiro de Barros – RA: 081230021  
Luis Gustavo de Oliveira Carneiro – RA: 081230029  
Roger Rocha da Silva – RA: 081230045  
João Victor Pereira Andrade – RA: 081230010  

Novembro de 2025.
