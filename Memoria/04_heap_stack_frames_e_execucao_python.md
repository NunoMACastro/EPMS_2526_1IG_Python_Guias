# Memória (10.º Ano) - 04 · Heap, Stack, Frames e Execução de Código Python

> **Objetivo deste ficheiro**  
> Entender onde ficam dados e referências durante a execução, perceber Stack vs Heap sem confusões e compreender o caminho básico de execução de um script Python.

---

## Índice

- [0. Como usar este ficheiro](#0-como-usar-este-ficheiro)
- [1. O que acontece quando corremos um `.py`?](#1-o-que-acontece-quando-corremos-um-py)
- [2. Compilar vs interpretar (em linguagem simples)](#2-compilar-vs-interpretar-em-linguagem-simples)
- [3. Bytecode e `__pycache__`](#3-bytecode-e-__pycache__)
- [4. PVM (Python Virtual Machine)](#4-pvm-python-virtual-machine)
- [5. Stack: chamadas de função e stack frames](#5-stack-chamadas-de-função-e-stack-frames)
- [6. Heap: objetos e estruturas dinâmicas](#6-heap-objetos-e-estruturas-dinâmicas)
- [7. Stack + Heap a trabalhar em conjunto](#7-stack--heap-a-trabalhar-em-conjunto)
- [8. Recursão e stack overflow (conceito)](#8-recursão-e-stack-overflow-conceito)
- [9. Erros comuns de compreensão](#9-erros-comuns-de-compreensão)
- [9.1 Ponte para execução real do sistema](#ponte-execucao-real)
- [10. Resumo final](#10-resumo-final)
- [11. Changelog](#11-changelog)

---

## 0. Como usar este ficheiro

Quando leres sobre Stack e Heap, não tentes decorar frases soltas.  
Tenta sempre responder a duas perguntas:

1. "Este dado é temporário de execução de função ou é objeto em memória dinâmica?"
2. "Isto vive enquanto a função está ativa, ou pode viver mais tempo?"

---

## 1. O que acontece quando corremos um `.py`?

Fluxo simplificado:

1. O Python lê o ficheiro fonte (`.py`);
2. verifica sintaxe;
3. converte para bytecode;
4. executa bytecode na máquina virtual do Python;
5. interage com sistema operativo e CPU.

Este fluxo é importante porque mostra que:

- o computador não executa diretamente o texto Python "humano";
- existe uma etapa intermédia.

---

## 2. Compilar vs interpretar (em linguagem simples)

### Compilar (ideia geral)

Converter código fonte para forma executável antes da execução.

### Interpretar (ideia geral)

Executar instruções com apoio de um interpretador durante a execução.

### E Python?

Python é normalmente apresentado como linguagem interpretada,  
mas na prática passa por etapa intermédia de compilação para bytecode.

---

## 3. Bytecode e `__pycache__`

Bytecode é uma representação intermédia do programa.

Características:

- não é código-fonte legível para humanos;
- não é código de máquina nativo final;
- é formatado para ser executado pela máquina virtual do Python.

Em muitos casos, o Python guarda bytecode em `__pycache__` (`.pyc`) para acelerar execuções seguintes.

---

## 4. PVM (Python Virtual Machine)

A PVM é o "motor" que executa o bytecode.

De forma didática:

- lê instruções de bytecode;
- coordena operações em objetos Python;
- comunica com o sistema operativo quando necessário.

Isto ajuda a portabilidade: o mesmo código Python funciona em vários sistemas com interpretador apropriado.

---

## 5. Stack: chamadas de função e stack frames

A Stack (pilha de execução) organiza chamadas de função.

Quando uma função é chamada, cria-se um **stack frame** com informação dessa chamada:

- parâmetros;
- variáveis locais (referências);
- ponto de retorno.

Quando a função termina, o frame é removido da stack.

### Comportamento LIFO

Last In, First Out:

- a última função chamada é a primeira a terminar.

---

## 6. Heap: objetos e estruturas dinâmicas

A Heap é a zona de memória onde, de forma simplificada para este nível, ficam objetos alocados dinamicamente.

Exemplos:

- listas;
- dicionários;
- instâncias de classes;
- strings e muitos outros objetos.

### Ideia essencial

Variáveis locais da função (no frame) costumam guardar referências para objetos que estão na heap.

### Nota: Heap não é "sinónimo de RAM inteira"

Heap é uma região lógica de memória usada para alocação dinâmica dentro do processo.

No nível introdutório:

- Stack: contexto de execução/chamadas;
- Heap: objetos dinâmicos.

Mais tarde verás detalhes mais técnicos de gestão interna.

---

## 7. Stack + Heap a trabalhar em conjunto

Exemplo:

```python
def criar_lista():
    dados = [10, 20, 30]
    return dados

resultado = criar_lista()
```

Leitura pedagógica:

1. `criar_lista()` cria um frame na stack;
2. a lista é criada na heap;
3. `dados` é referência local (no frame) para a lista;
4. ao `return`, referência é passada para `resultado`;
5. frame da função é removido;
6. objeto na heap continua vivo porque `resultado` ainda o referencia.

---

## 8. Recursão e stack overflow (conceito)

Cada chamada recursiva cria novo frame na stack.

Se não houver condição de paragem adequada, o número de frames cresce até exceder limite.

Resultado: erro de stack overflow/recursion limit.

Exemplo de erro conceptual:

```python
def f():
    return f()
```

Falta caso base -> chamadas infinitas -> esgotamento da stack.

### E a memória virtual nisto?

Mesmo com memória virtual (swap), stack overflow não deixa de ser problema lógico.

Isto porque:

- o programa continua a criar frames sem fim;
- a solução correta é corrigir a recursão (caso base), não "adicionar swap".

---

## 9. Erros comuns de compreensão

### Erro 1
"Stack guarda todos os dados do programa."

**Correção:** stack está focada na execução de chamadas e contexto local; muitos objetos vivem na heap.

### Erro 2
"Heap é sempre lenta e má."

**Correção:** heap é essencial para estruturas dinâmicas; não é "má", é necessária.

### Erro 3
"Quando a função termina, todos os objetos criados nela desaparecem imediatamente."

**Correção:** desaparecem referências locais do frame; o objeto só é removido se não houver outras referências.

<a id="ponte-execucao-real"></a>

## 9.1 Ponte para execução real do sistema

Este módulo explica bem a execução no contexto do Python (bytecode + PVM + heap/stack).  
Mas existe um nível mais abaixo: o sistema operativo e a CPU real.

Resumo da ponte:

- Python abstrai muito do detalhe;
- no fim, a execução passa por instruções de máquina da arquitetura da CPU;
- o sistema operativo trata de processo, carregamento e recursos.

Para a visão completa "do código à execução real", consulta:

- `Memoria/06_do_codigo_a_execucao_real_so_cpu_isa.md`

---

## 10. Resumo final

- Python executa `.py` através de bytecode e PVM.
- Stack organiza chamadas de função em frames.
- Heap armazena objetos dinâmicos.
- Frames podem desaparecer rapidamente; objetos podem continuar se referenciados.
- Recursão sem controlo pode esgotar stack.

---

## 11. Changelog

- **2026-02-04**: versão inicial do módulo 04.
