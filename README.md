# Processador MIPS Adaptado

Este projeto implementa um processador MIPS simplificado e adaptado, desenvolvido no Logisim para fins educacionais. O processador possui uma arquitetura de 8 bits com pipeline de 3 estágios.

Confira o vídeo explicativo clicando [aqui](https://youtu.be/AuRI3dCpmVk)!

## 📋 Especificações Técnicas
- **Barramento de dados**: 8 bits
- **Barramento de endereços**: 8 bits
- **Tamanho da instrução**: 18 bits
- **Quantidade de registradores**: 8
- **Pipeline**: 3 estágios (IFU, IDU, EXU)

# Unidades
## 1. Instruction Fetch Unit (IFU)
Responsável por buscar instruções da memória e controlar o fluxo do programa.

### Componentes:
- **PC (Program Counter)**: Registrador de 8 bits
- **Instruction Memory**: ROM de 8 bits de endereço × 18 bits de dados
- **Lógica de desvio**: Controla sequência de execução

### Lógica de Controle do PC:
`Próximo PC = (J + (B × Z)) ? ID:Address/IMM : PC + 1`

Onde:
- **J**: Sinal Jump da Control Unit
- **B**: Sinal Branch da Control Unit  
- **Z**: Sinal Equals da ALU

## 2. Instruction Decode Unit (IDU)
Decodifica instruções e gera sinais de controle.

### Instruction Decoder
Separa os 18 bits da instrução em campos:

#### Formato R (Register):
`[17:15] Opcode | [14:12] Rs | [11:9] Rt | [8:6] Rd | [5:3] Shamt | [2:0] Funct`

#### Formato I (Immediate):
`[17:15] Opcode | [14:12] Rs | [11:9] Rt | [8] X | [7:0] Address/IMM`

### Control Unit (CU)
Gera sinais de controle baseados no Opcode:

| Opcode | Instrução | RegDst | RegWrite | ALUSrc | MemWrite | MemRead | MemToReg | Branch | Jump | ALUOp |
|--------|-----------|---------|----------|---------|----------|---------|----------|---------|------|-------|
| 000    | Tipo R    | 1       | 1        | 0       | 0        | 0       | 0        | 0       | 0    | 10    |
| 001    | lw        | 0       | 1        | 1       | 0        | 1       | 1        | 0       | 0    | 00    |
| 010    | sw        | X       | 0        | 1       | 1        | 0       | X        | 0       | 0    | 00    |
| 011    | beq       | X       | 0        | 0       | 0        | 0       | X        | 1       | 0    | 01    |
| 100    | addi      | 0       | 1        | 1       | 0        | 0       | 0        | 0       | 0    | 00    |
| 111    | j         | X       | 0        | X       | 0        | 0       | X        | 0       | 1    | XX    |

## 3. Execution Unit (EXU)
Executa operações e gerencia dados.

### Register File
- **8 registradores** de 8 bits
- **Portas de leitura**: 2 (Read data 1 e Read data 2)
- **Porta de escrita**: 1 (Write data)

#### Mapeamento de Registradores:
```000: $zero (sempre 0)
001: $t0
010: $t1
011: $t2
100: $t3
101: $t4
110: $t5
111: $t6
```

### ALU (Arithmetic Logic Unit)
Operações suportadas:

| ALUCtrl | Operação  | Descrição               |
|---------|-----------|-------------------------|
| 000     | add       | Soma                    |
| 001     | sub       | Subtração               |
| 010     | mult      | Multiplicação           |
| 011     | div       | Divisão                 |
| 100     | neg       | Negação                 |
| 101     | slt       | Set Less Than + Equals  |
| 110     | sll       | Shift Left Logical      |
| 111     | srl       | Shift Right Logical     |

### Data Memory
- **Memória RAM**: 8 bits de endereço × 8 bits de dados
- **Operações**: Leitura (MemRead) e Escrita (MemWrite)

## 🔧 Conjunto de Instruções

### Instruções Tipo R (Opcode: 000)
```add $rd, $rs, $rt # $rd = $rs + $rt
sub $rd, $rs, $rt # $rd = $rs - $rt
mult $rd, $rs, $rt # $rd = $rs × $rt
slt $rd, $rs, $rt # $rd = ($rs < $rt) ? 1 : 0
```

### Instruções Tipo I
```addi $rt, $rs, IMM # $rt = $rs + IMM
lw $rt, IMM($rs) # $rt = MEM[$rs + IMM]
sw $rt, IMM($rs) # MEM[$rs + IMM] = $rt
beq $rs, $rt, IMM # if ($rs == $rt) PC = IMM
```

### Instruções Tipo J
`j IMM # PC = IMM`


## 💻 Exemplo de Programação

### Programa: Soma e Multiplicação
```asm
# Soma: 12 + 8 = 20
addi $t0, $zero, 12    # $t0 = 12
addi $t1, $zero, 8     # $t1 = 8
add  $t2, $t0, $t1     # $t2 = 20

# Multiplicação: 6 × 7 = 42
addi $t4, $zero, 6     # $t4 = 6
addi $t5, $zero, 7     # $t5 = 7
mult $t6, $t4, $t5     # $t6 = 42

# Armazenar na memória
sw   $t6, 0($zero)     # MEM[0] = 42

#### Codificação em Hexadecimal:
2020C  // addi $t0, $zero, 12
20408  // addi $t1, $zero, 8
014C0  // add $t2, $t0, $t1
20A06  // addi $t4, $zero, 6
20C07  // addi $t5, $zero, 7
05DC2  // mult $t6, $t4, $t5
10E00  // sw $t6, 0($zero)
```

Coloque na ROM de Instruction Memory e teste!

### Dicas de Depuração:
- Use CLEAR antes de executar novos programas
- Execute passo a passo para verificar cada estágio
- Verifique sinais da Control Unit durante execução
- Confirme timing de escrita nos registradores

## 🚀 Fluxo de Execução
### Ciclo de Instrução:
1. IFU (Instruction Fetch)
- PC envia endereço para Instruction Memory
- Instrução é buscada e enviada para IDU
2. IDU (Instruction Decode)
- Instrução é decodificada em campos
- Control Unit gera sinais de controle
- Register File lê registradores especificados
3. EXU (Execution)
- ALU executa operação com operandos
- Data Memory realiza acesso se necessário
- Resultado é escrito no Register File

### Timing
Leitura de registradores: valor atual

Escrita em registradores: próxima borda de clock

Acesso à memória: durante estágio EXU

## 📝 Notas de Implementação
### Características Específicas:
- Instruction Memory: ROM com palavras de 18 bits
- Data Memory: RAM com palavras de 8 bits
- Todos os sinais são ativos em alto (1)
- Clock controla escrita em registradores e memória

### Limitações Conhecidas:
- Tamanho limitado de memória (256 bytes)
- Conjunto reduzido de instruções
- Não suporta interrupções ou exceções

## 👨‍🏫 Integrantes e créditos
- Aline Cristina Ribeiro de Barros – RA: 081230021
- Luis Gustavo de Oliveira Carneiro – RA: 081230029
- Roger Rocha da Silva – RA: 081230045
- João Victor Pereira Andrade – RA: 081230010
- André Mendes Garcia - RA: 081230012

### Agradecimentos Especiais
- Professor [Bruno Abreu](https://www.youtube.com/@brunoabreu8105), fornecendo a arquitetura base

- Professor [Vinícius Borges](https://www.linkedin.com/in/vinicius-borges-07a170153/), fornecendo base técnica em arquitetura de computadores


## Licença
Este projeto é de uso acadêmico e livre para consulta e aprendizado, conforme os princípios de uso educacional da disciplina Arquitetura de Computadores.

Novembro de 2025.
