# Memória (10.º Ano) - 04 · Heap, Stack, Frames e Execução de Código Python (v2)

> **Objetivo deste ficheiro**  
> Entender, passo a passo, como um programa Python é preparado e executado, onde vivem os dados durante a execução (**stack** e **heap**), e o que acontece em chamadas de função, retorno e recursão.  
> No fim, deves conseguir “ver” mentalmente o que está a acontecer quando o teu código corre — e usar isso para **depurar erros** com mais confiança.

---

## Índice

- [1. O mapa geral: processo, código, stack e heap](#1-o-mapa-geral-processo-código-stack-e-heap)
- [2. O que realmente acontece quando corres um `.py`](#2-o-que-realmente-acontece-quando-corres-um-py)
- [3. Compilar vs interpretar (com mais detalhe)](#3-compilar-vs-interpretar-com-mais-detalhe)
- [4. Python: modelo híbrido (fonte -> bytecode -> execução)](#4-python-modelo-híbrido-fonte---bytecode---execução)
- [5. Bytecode e pasta `__pycache__`](#5-bytecode-e-pasta-__pycache__)
- [6. PVM: o "motor" de execução do Python](#6-pvm-o-motor-de-execução-do-python)
- [7. Memória de execução: stack vs heap](#7-memória-de-execução-stack-vs-heap)
- [8. Stack frames: o que um frame contém](#8-stack-frames-o-que-um-frame-contém)
- [9. Tornar o invisível visível: `locals()`, `id()` e `dis`](#9-tornar-o-invisível-visível-locals-id-e-dis)
- [10. Exemplo completo de chamada de função (com desenho)](#10-exemplo-completo-de-chamada-de-função-com-desenho)
- [11. Exemplo com várias funções (pilha em camadas)](#11-exemplo-com-várias-funções-pilha-em-camadas)
- [12. Retorno, vida dos objetos e garbage collection](#12-retorno-vida-dos-objetos-e-garbage-collection)
- [13. Recursão e `RecursionError`: causa real](#13-recursão-e-recursionerror-causa-real)
- [14. Debug real: o traceback é a stack “impressa”](#14-debug-real-o-traceback-é-a-stack-impressa)
- [15. Erros comuns de alunos neste tema](#15-erros-comuns-de-alunos-neste-tema)
- [16. Exercícios de consolidação](#16-exercícios-de-consolidação)
- [17. Resumo final](#17-resumo-final)
- [18. Changelog](#18-changelog)

---

## 1. O mapa geral: processo, código, stack e heap

### 1.1 Quando corres Python, crias um “processo”

Um **processo** é, de forma simples, “um programa a correr”.

Esse processo tem:

- **código** a ser executado,
- **memória** disponível para o programa,
- **estado de execução** (o que está a fazer agora).

### 1.2 Dentro desse processo, pensa em duas “zonas” lógicas

- **Stack (pilha de execução)**: guarda o contexto das funções ativas (frames).
- **Heap**: guarda os objetos (listas, dicionários, strings, instâncias, etc.).

> Nota importante: isto não são “peças físicas separadas”.  
> É uma divisão **lógica** útil para entender o que acontece durante a execução.

Mais à frente, vamos ver o que são na realidade estas duas “zonas” e como interagem.

---

## 2. O que realmente acontece quando corres um `.py`

Quando clicas em “Run” num ficheiro Python, o processo real (simplificado) é:

1. o interpretador Python abre o ficheiro `.py`;
2. verifica sintaxe;
3. converte para **bytecode**;
4. a máquina virtual do Python executa o bytecode passo a passo;
5. durante execução, cria objetos, chama funções e interage com o sistema operativo.

Ponto importante:

> O CPU não executa texto Python diretamente.  
> Ele executa o **interpretador Python**, e é esse interpretador que “faz acontecer” as ações do teu código.
> Ou seja, o código que tu escreves vive numa "bolha" que é o interpretador. O Interpretador é o que tem acesso direto ao sistema operativo e à CPU, e o teu código é traduzido para algo que o interpretador consegue entender e executar.

---

## 3. Compilar vs interpretar

### Compilar

Compilar significa, em programação, transformar o código fonte de um determinado nível de abstração (ex.: Python) para outro nível (ex.: código máquina ou bytecode) **antes** de executar.

- traduz código fonte para um formato executável **antes** de correr;
- tende a gerar artefactos de compilação (objetos/executável).

### Interpretar

Interpretar significa ler o código fonte e executar as instruções **durante a execução**. As instruções são analisadas e executadas passo a passo.

- analisa e executa durante a execução;
- tende a ser mais dinâmico no desenvolvimento.

### Porque confunde em Python?

Porque Python faz os dois em sequência:

- compila para bytecode;
- executa bytecode na PVM.

Ou seja: chamar Python “só interpretado” é uma simplificação útil, mas incompleta. No entanto essa simplificação pode induzir a erros de compreensão sobre o que acontece.

---

## 4. Python: modelo híbrido (fonte -> bytecode -> execução)

Fluxo mental:

`código fonte (.py)`  
→ `bytecode`  
→ `PVM executa`  
→ `efeitos no programa (prints, cálculos, ficheiros, rede...)`

Isto explica:

- portabilidade de Python;
- porque existe `__pycache__`;
- porque stack/heap aparecem durante execução e não no texto fonte.

---

## 5. Bytecode e pasta `__pycache__`

**Bytecode**:

- é uma representação intermédia;
- não é código-fonte legível;
- não é instrução nativa final da CPU.

Basicamente é uma linguagem de baixo nível que a PVM entende e executa. A PVM vai ler o bytecode e transformar as instruções numa série de operações que o sistema operativo e a CPU conseguem executar.

A pasta `__pycache__` guarda ficheiros `.pyc` (quando aplicável) para acelerar arranques futuros.

---

## 6. PVM: o "motor" de execução do Python

A PVM (Python Virtual Machine):

- lê bytecode;
- decide que operação runtime executar;
- coordena criação/uso de objetos Python;
- pede serviços ao sistema operativo quando necessário (ex.: abrir ficheiro).

Analogia simples:

- teu código é a receita;
- bytecode é a receita em formato técnico;
- PVM é o cozinheiro que executa passos.

---

### 6.1 Diagrama sobre todo o processo usando Python

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ 1) PROGRAMADOR │
│ Escreve código Python (.py) │
└───────────────┬─────────────────────────────────────────────────────────────┘
│
v
┌─────────────────────────────────────────────────────────────────────────────┐
│ 2) FICHEIRO NO DISCO (SSD/HDD) │
│ - O .py é guardado como bytes │
│ - Não está "a correr", está só armazenado │
└───────────────┬─────────────────────────────────────────────────────────────┘
│ (Quando carregas em Run / python ficheiro.py)
v
┌─────────────────────────────────────────────────────────────────────────────┐
│ 3) SISTEMA OPERATIVO (SO) │
│ Cria um PROCESSO para o Python (o interpretador) │
│ - Reserva memória para o processo │
│ - Carrega o interpretador Python (executável) para a RAM │
│ - Dá permissões, prepara stack/heap, etc. │
└───────────────┬─────────────────────────────────────────────────────────────┘
│
v
┌─────────────────────────────────────────────────────────────────────────────┐
│ 4) INTERPRETADOR PYTHON (programa C) A CORRER NA RAM │
│ Este é o programa REAL que o CPU executa diretamente. │
│ O interpretador lê o teu .py e faz: │
│ a) parsing/validação de sintaxe │
│ b) compilação para BYTECODE (.pyc) │
└───────────────┬─────────────────────────────────────────────────────────────┘
│
│ (Opcional: guarda bytecode em **pycache** para acelerar)
v
┌─────────────────────────────────────────────────────────────────────────────┐
│ 5) BYTECODE (instruções da PVM) │
│ - Não é código de máquina do CPU │
│ - É um formato intermédio: "instruções para a máquina virtual do Python" │
└───────────────┬─────────────────────────────────────────────────────────────┘
│
v
┌─────────────────────────────────────────────────────────────────────────────┐
│ 6) PVM (Python Virtual Machine) │
│ É uma parte do interpretador que faz um loop do tipo: │
│ FETCH bytecode -> DECODE -> EXECUTE │
│ │
│ Para cada instrução de bytecode, a PVM faz operações em objetos Python: │
│ - cria/usa ints, strings, listas, dicts, etc. (heap) │
│ - chama funções (frames na stack) │
│ - pede ao SO ações (I/O: prints, ficheiros, rede, etc.) │
└───────────────┬─────────────────────────────────────────────────────────────┘
│
│ (Aqui acontece a “ponte” crucial:)
│ Bytecode NÃO é executado pelo CPU.
│ Quem executa bytecode é o interpretador (programa nativo).
v
┌─────────────────────────────────────────────────────────────────────────────┐
│ 7) CPU (ISA: x86/ARM, etc.) │
│ O CPU só entende INSTRUÇÕES DE MÁQUINA (assembly) da sua ISA. │
│ │
│ O que o CPU executa mesmo é: │
│ - o interpretador Python (código máquina) │
│ - + chamadas ao Sistema Operativo │
│ │
│ Ou seja: o CPU "percebe" o teu programa Python porque executa │
│ um programa (interpretador) que IMPLEMENTA o significado do Python. │
└─────────────────────────────────────────────────────────────────────────────┘
```

## 7. Memória de execução: stack vs heap

### 7.1 Stack (pilha de execução)

Organiza contexto das chamadas de função em frames.

Características:

- LIFO (Last In, First Out);
- cresce com chamadas;
- encolhe quando funções retornam.

### 7.2 Heap

Zona de alocação dinâmica de objetos.

Exemplos de objetos:

- listas, dicionários, strings;
- instâncias de classes;
- muitos outros tipos Python.

### 7.3 Regra prática para iniciantes

- frame da função → stack;
- objeto criado → heap;
- variável local → referência no frame, apontando para objeto no heap.

---

## 8. Stack frames: o que um frame contém

Quando uma função é chamada, Python cria um frame com (versão didática):

- parâmetros da função;
- variáveis locais;
- (quando aplicável) referências para contexto exterior;
- ponto/estado para onde voltar após `return`.

Quando a função termina:

- o frame é removido da stack;
- referências locais desse frame desaparecem;
- objetos no heap só desaparecem se ficarem sem referências.

> Ideia-chave: “o frame morre rápido”, mas “o objeto pode ficar vivo”.

---

## 9. Tornar o invisível visível: `locals()`, `id()` e `dis`

Esta secção é para veres o que normalmente fica escondido.

### 9.1 Ver as variáveis do frame atual com `locals()`

Dentro de uma função:

```python
def exemplo(a):
    b = a + 1
    print("locals:", locals())
    return b

exemplo(10)
```

O `locals()` devolve um dicionário com as variáveis locais do frame.
Isto ajuda a pensar: “ok, este frame tem estas referências”.

### 9.2 Ver identidade (não “endereço físico”) com `id()`

```python
x = [1, 2, 3]
y = x

print(id(x))
print(id(y))
```

Se os `id` forem iguais, é uma pista forte de que `x` e `y` apontam para o **mesmo objeto**.

> Nota pedagógica: pensa em `id()` como **identidade do objeto**.  
> Em muitas implementações, pode coincidir com detalhes internos, mas não escrevas lógica a depender disso.

### 9.3 Ver bytecode (curiosidade controlada) com `dis`

Não precisas perceber tudo, mas é útil para perceber que existe uma “camada intermédia”.

```python
import dis

def soma(a, b):
    return a + b

dis.dis(soma)
```

Vais ver instruções internas que a PVM executa.

---

## 10. Exemplo completo de chamada de função (com desenho)

```python
def dobrar(n):
    resultado = n * 2
    return resultado

x = 5
y = dobrar(x)
print(y)
```

### Passo a passo

1. `x = 5`
    - no frame global existe a referência `x`
    - `x` aponta para o objeto `5` (imutável)

2. chama `dobrar(x)`
    - cria-se um frame novo na stack: frame `dobrar`
    - `n` aponta para o mesmo objeto que `x` (5)

3. `resultado = n * 2`
    - cria-se (ou obtém-se) um objeto `10`
    - `resultado` aponta para `10`

4. `return resultado`
    - devolve-se a referência para `10`
    - o frame `dobrar` é removido da stack

5. `y` (no frame global) passa a apontar para `10`

### Desenho mental

**Stack (frames):**

Durante a execução de `dobrar`:

```
Topo
[ dobrar ]   n -> (5)      resultado -> (10)
[ global ]   x -> (5)      y -> (?)
Base
```

Depois do `return`:

```
Topo
[ global ]   x -> (5)      y -> (10)
Base
```

**Heap (objetos):**

```
(5)   (10)
```

---

## 11. Exemplo com várias funções (pilha em camadas)

```python
def c():
    return "fim"

def b():
    return c()

def a():
    return b()

print(a())
```

Evolução da stack:

1. frame global chama `a()` → `[global, a]`
2. `a()` chama `b()` → `[global, a, b]`
3. `b()` chama `c()` → `[global, a, b, c]`
4. `c()` retorna → remove `c`
5. `b()` retorna → remove `b`
6. `a()` retorna → remove `a`
7. global recebe valor final

Isto é LIFO puro: **a última função a entrar é a primeira a sair**.

---

## 12. Retorno, vida dos objetos e garbage collection

Erro mental clássico:

> “A função acabou, logo o objeto desapareceu.”

Nem sempre.

```python
def criar():
    dados = [1, 2, 3]
    return dados

z = criar()   # a lista continua viva
```

O frame de `criar` desaparece, mas a lista continua porque `z` aponta para ela.

### Regra simples

- um objeto vive enquanto houver **referências** para ele;
- se ficar sem referências, torna-se elegível para limpeza (contagem de referências + GC).

---

## 13. Recursão e `RecursionError`: causa real

Cada chamada recursiva cria um frame novo.

Sem condição de paragem adequada:

- frames acumulam;
- o Python atinge o limite de recursão;
- surge `RecursionError`.

Exemplo incorreto:

```python
def infinito(n):
    return infinito(n + 1)
```

Exemplo correto (com caso base):

```python
def contar(n):
    if n == 0:
        return 0
    return contar(n - 1)
```

Ponto-chave:

- o problema não é “falta de RAM”;
- o problema é **lógica sem paragem**, que continua a empilhar frames.

---

## 14. Debug real: o traceback é a stack “impressa”

Quando há erro, Python mostra um **traceback**.
Isso é (quase literalmente) a lista das chamadas de função que estavam ativas.

Exemplo:

```python
def c():
    return 10 / 0

def b():
    return c()

def a():
    return b()

a()
```

O traceback mostra:

- o erro (divisão por zero),
- e o caminho `a()` → `b()` → `c()`.

### Como ler (regra prática)

- o traceback é o histórico de chamadas;
- encontras o ponto do problema na linha onde o erro aconteceu (no fundo da cadeia do erro).

Isto liga stack frames a uma coisa prática: **depuração**.

---

## 15. Erros comuns de alunos neste tema

### Erro 1

“Stack e heap são duas peças físicas separadas.”

**Correção:** são regiões lógicas do espaço de memória do processo (modelo mental útil).

### Erro 2

“Variável local guarda o objeto inteiro.”

**Correção:** guarda uma **referência** para o objeto.

### Erro 3

“Return copia sempre tudo.”

**Correção:** muitas vezes passa referências (modelo mental certo para este nível).

### Erro 4

“Se está no heap, nunca sai.”

**Correção:** sai quando deixa de haver referências e o runtime faz limpeza.

### Erro 5

“Recursão falha porque o PC não tem RAM.”

**Correção:** falha porque empilha frames até ao limite (`RecursionError`).

---

## 16. Exercícios de consolidação

> Faz primeiro sem olhar para explicações anteriores. O objetivo é confirmares se a “imagem mental” ficou certa.

### Exercício 1 — o objeto continua vivo?

```python
def f():
    a = [1, 2]
    return a

x = f()
print(x)
```

Responde:

1. A lista continua viva depois do `return`? Porquê?
2. O frame `f` continua vivo? Porquê?

### Exercício 2 — desenha a stack

```python
def c(): return 1
def b(): return c()
def a(): return b()

a()
```

Desenha a stack no momento em que `c()` está a executar.

### Exercício 3 — recursão

Explica porque isto dá erro:

```python
def g():
    return g()
```

E como corrigias (em 1 frase).

### Exercício 4 — traceback (stack visível)

Cria um erro propositado com 3 funções em cadeia (`a()` chama `b()` chama `c()`).
Depois explica o traceback com as tuas palavras:

- “o que me está a dizer?”
- “onde está a linha que interessa?”

### Exercício 5 — referências e alias

```python
a = [1, 2, 3]
b = a
b.append(4)
print(a)
```

Responde:

1. Porque é que `a` também muda?
2. O que quer dizer “alias” neste contexto?

---

## 17. Resumo final

- Python não executa texto fonte diretamente; executa via **bytecode + PVM**.
- Cada chamada de função cria um **frame** na stack.
- Objetos vivem tipicamente no **heap**; frames guardam referências locais.
- `return` remove o frame chamado, mas objetos podem continuar vivos se forem referenciados fora.
- Recursão sem caso base acumula frames até `RecursionError`.
- Traceback é a stack “visível” e é uma ferramenta essencial de debug.

---

## 18. Changelog

- **2026-02-04**: versão inicial do módulo 04.
- **2026-02-05**: v2 (mapa mental + observação com ferramentas + debug + exercícios).
