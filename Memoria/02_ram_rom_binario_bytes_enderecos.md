# Memória (10.º Ano) - 02 · RAM, ROM, Binário, Bytes e Endereços

> **Objetivo deste ficheiro**  
> Entender, com calma e sem saltos, os conceitos fundamentais de RAM e ROM, sistema binário, bytes, unidades de memória e noções básicas de endereçamento.

---

## Índice

- [0. Como usar este ficheiro](#0-como-usar-este-ficheiro)
- [1. RAM vs ROM (diferença essencial)](#1-ram-vs-rom-diferença-essencial)
- [2. O que é um bit? O que é um byte?](#2-o-que-é-um-bit-o-que-é-um-byte)
- [3. Sistema binário (base 2)](#3-sistema-binário-base-2)
- [4. Converter decimal para binário](#4-converter-decimal-para-binário)
- [5. Converter binário para decimal](#5-converter-binário-para-decimal)
- [6. Texto em código binário (noção inicial)](#6-texto-em-código-binário-noção-inicial)
- [7. Endereço de memória (visão simples)](#7-endereço-de-memória-visão-simples)
- [8. Exercícios de consolidação (binário)](#8-exercícios-de-consolidação-binário)
- [9. Resumo final](#9-resumo-final)
- [10. Changelog](#10-changelog)

---

## 0. Como usar este ficheiro

Este tema costuma assustar no início, mas a dificuldade normalmente vem de tentar fazer tudo rápido demais.

Estratégia:

1. Lê cada secção;
2. Faz 2 ou 3 exemplos à mão;
3. Só depois avança para a secção seguinte;
4. No fim, resolve os exercícios.

Não procures velocidade. Procura clareza.

---

## 1. RAM vs ROM (diferença essencial)

### RAM (Random Access Memory)

- memória principal de trabalho;
- rápida;
- usada enquanto os programas estão a correr;
- normalmente volátil (perde conteúdo sem energia).

### ROM (Read-Only Memory)

- memória de leitura usada para guardar informação essencial do sistema;
- normalmente não volátil;
- contém firmware/instruções base de arranque.

### Comparação direta

- RAM: "mesa de trabalho";
- ROM: "manual fixo do equipamento".

---

## 2. O que é um bit? O que é um byte?

### Bit

É a menor unidade de informação digital.  
Só pode assumir dois valores:

- 0
- 1

### Byte

Um byte = 8 bits.

Exemplo:

- `01010100` é uma sequência de 8 bits (1 byte).

### Porque é importante?

Porque quase toda a informação num computador pode ser representada em bits:

- números,
- texto,
- imagens,
- áudio,
- instruções.

---

## 3. Sistema binário (base 2)

No sistema decimal (base 10), usamos os dígitos 0..9.  
No sistema binário (base 2), usamos apenas 0 e 1.

### Potências de 2 (muito importante)

| Posição | Potência de 2 | Valor |
| ------- | ------------- | ----- |
| 0       | 2^0           | 1     |
| 1       | 2^1           | 2     |
| 2       | 2^2           | 4     |
| 3       | 2^3           | 8     |
| 4       | 2^4           | 16    |
| 5       | 2^5           | 32    |
| 6       | 2^6           | 64    |
| 7       | 2^7           | 128   |

Cada posição binária representa uma potência de 2.

---

## 4. Converter decimal para binário

Método simples (divisões por 2):

1. Divide o número por 2;
2. Guarda o resto (0 ou 1);
3. Volta a dividir o quociente por 2;
4. Repete até o quociente ser 0;
5. Lê os restos de baixo para cima.

### Exemplo: 13 em binário

13 / 2 = 6 resto 1  
6 / 2 = 3 resto 0  
3 / 2 = 1 resto 1  
1 / 2 = 0 resto 1

Lendo restos de baixo para cima: **1101**

Logo: `13(10) = 1101(2)`

---

## 5. Converter binário para decimal

Método:

1. Escreve as potências de 2 por baixo dos bits;
2. Soma apenas as potências cujos bits são 1.

### Exemplo: `10110`

Posições (da direita para a esquerda):

- 0 -> 2^0 = 1
- 1 -> 2^1 = 2
- 2 -> 2^2 = 4
- 3 -> 2^3 = 8
- 4 -> 2^4 = 16

Bits de `10110`:

- 1·16 + 0·8 + 1·4 + 1·2 + 0·1
- 16 + 4 + 2
- **22**

Logo: `10110(2) = 22(10)`

---

## 6. Texto em código binário (noção inicial)

O computador guarda texto como números, e esses números em binário.

Um padrão comum de codificação é UTF-8 (no contexto moderno).

Exemplo simples (conceito):

- letra `A` -> valor 65 (em tabelas clássicas ASCII)
- 65 em binário = `01000001`

Não precisas decorar tabela completa agora.  
Precisas apenas de perceber a ideia:

**texto -> código numérico -> binário**

---

## 7. Endereço de memória (visão simples)

Quando um dado está na memória, ele está numa posição específica.

Essa posição tem um "nome técnico": **endereço de memória**.

Analogia:

- Memória = rua com casas;
- Endereço = número da casa;
- Dado = pessoa que vive nessa casa.

Sem endereço, o processador não sabe onde buscar o dado.

---

## 8. Exercícios de consolidação (binário)

> Faz primeiro sem olhar para as resoluções.

### Exercício 1 - Decimal para binário

Converte para binário:

1. `10`
2. `25`
3. `100`
4. `41`

> Resolução

1. `10` -> `1010`
2. `25` -> `11001`
3. `100` -> `1100100`
4. `41` -> `101001`

---

### Exercício 2 - Binário para decimal

Converte para decimal:

1. `1001101`
2. `101011`
3. `1111111111`
4. `1000000`

> Resolução

1. `1001101` -> 64 + 8 + 4 + 1 = `77`
2. `101011` -> 32 + 8 + 2 + 1 = `43`
3. `1111111111` -> 1023
4. `1000000` -> `64`

---

### Exercício 3 - Verdadeiro ou falso

Indica V/F:

1. 1 byte = 16 bits.
2. RAM é normalmente volátil.
3. ROM é usada para guardar firmware.
4. Em binário, usamos os dígitos 0 e 1.

> Resolução

1. Falso
2. Verdadeiro
3. Verdadeiro
4. Verdadeiro

---

### Exercício 4 - Potências de 2

Completa:

1. 2^0 = ?
2. 2^3 = ?
3. 2^5 = ?
4. 2^7 = ?

> Resolução

1. 1
2. 8
3. 32
4. 128

---

### Exercício 5 - Desafio guiado

1. Converte 84 para binário.
2. Converte `01010100` para decimal.
3. Compara os resultados.

> Resolução

1. `84` -> `01010100`
2. `01010100` -> `84`
3. São equivalentes; uma representação é decimal e a outra binária.

---

## 9. Resumo final

- RAM e ROM têm funções diferentes.
- Bit é unidade mínima (0/1); byte tem 8 bits.
- Binário usa base 2 e potências de 2.
- Conversão decimal/binário é essencial para compreender memória.
- Endereço de memória é a localização exata de um dado na RAM.

---

## 10. Changelog

- **2026-02-04**: versão inicial do módulo 02 com exercícios e resoluções.
