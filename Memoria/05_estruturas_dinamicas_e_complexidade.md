# Memória (10.º Ano) - 05 · Estruturas Dinâmicas e Complexidade (Big-O)

> **Objetivo deste ficheiro**  
> Introduzir estruturas dinâmicas de dados e a noção de complexidade de forma conceptual, com foco em perceber "quando usar o quê" e "porque pode ficar lento".

---

## Índice

- [0. Como usar este ficheiro](#0-como-usar-este-ficheiro)
- [1. Estruturas estáticas vs dinâmicas](#1-estruturas-estáticas-vs-dinâmicas)
- [2. Pilha (Stack)](#2-pilha-stack)
- [3. Fila (Queue)](#3-fila-queue)
- [4. Lista ligada (Linked List)](#4-lista-ligada-linked-list)
- [5. Árvore binária](#5-árvore-binária)
- [6. Dicionário (Hash Table, visão base)](#6-dicionário-hash-table-visão-base)
- [7. O que é complexidade?](#7-o-que-é-complexidade)
- [8. Big-O sem medo](#8-big-o-sem-medo)
- [9. Comparação simplificada de estruturas](#9-comparação-simplificada-de-estruturas)
- [10. Erros comuns (e correções)](#10-erros-comuns-e-correções)
- [11. Resumo final](#11-resumo-final)
- [12. Changelog](#12-changelog)

---

## 0. Como usar este ficheiro

Este ficheiro é teórico.  
O objetivo não é "decorar fórmulas", mas sim:

- perceber comportamento das estruturas;
- compreender impacto de escolhas no desempenho;
- desenvolver raciocínio para futuros exercícios/projetos.

---

## 1. Estruturas estáticas vs dinâmicas

### Estruturas estáticas (ideia)

Tamanho mais rígido/fixo no modelo clássico.

### Estruturas dinâmicas (ideia)

Podem crescer ou diminuir em execução, conforme necessidade.

### Porque usar dinâmicas?

- flexibilidade;
- melhor adaptação à quantidade de dados real;
- modelação mais natural de muitos problemas.

### Nota importante em Python

A `list` de Python já é uma estrutura dinâmica (implementada como array dinâmico).

Ou seja:

- pode crescer (`append`);
- pode diminuir (`pop`);
- mantém acesso por índice muito rápido em média.

Isto explica porque a `list` é tão usada.

---

## 2. Pilha (Stack)

Regra principal: **LIFO** (Last In, First Out).

Operações típicas:

- `push` (inserir no topo);
- `pop` (remover do topo);
- `peek/top` (ver topo sem remover).

### Exemplo do dia a dia

Pilha de pratos:

- último prato colocado é o primeiro a sair.

### Onde aparece em programação?

- chamada de funções (stack frames);
- operações de desfazer (undo);
- avaliação de expressões.

---

## 3. Fila (Queue)

Regra principal: **FIFO** (First In, First Out).

Operações típicas:

- `enqueue` (entra no fim);
- `dequeue` (sai do início).

### Exemplo do dia a dia

Fila de supermercado:

- quem entra primeiro é atendido primeiro.

### Onde aparece em programação?

- agendamento de tarefas;
- sistemas de atendimento;
- algoritmos de pesquisa em largura (BFS).

---

## 4. Lista ligada (Linked List)

Numa lista ligada, os elementos (nós) estão ligados por referências.

Cada nó costuma ter:

- valor;
- referência para próximo nó (`next`);
- (em lista dupla) referência para anterior (`prev`).

### Vantagem conceptual

Inserções/remoções em certos pontos podem ser eficientes sem mover todos os elementos.

### Desvantagem conceptual

Acesso direto por índice não é tão natural como em arrays/listas dinâmicas comuns.

---

## 5. Árvore binária

Estrutura hierárquica.

Cada nó (na versão binária):

- pode ter até dois filhos;
- normalmente chamados de filho esquerdo e filho direito.

### Vocabulário útil

- raiz (root);
- nó pai;
- nó filho;
- folha (nó sem filhos);
- subárvore.

### Aplicações

- organização hierárquica de dados;
- pesquisa;
- representação de expressões.

---

## 6. Dicionário (Hash Table, visão base)

Em Python, o `dict` é uma estrutura chave -> valor.

Exemplo:

```python
aluno = {"nome": "Ana", "nota": 17}
```

### Porque é poderoso?

Permite acesso muito rápido por chave em média.

### Atenção pedagógica

"Muito rápido em média" não significa "milagroso em todos os casos", mas no uso normal é excelente.

---

## 7. O que é complexidade?

Complexidade mede como o custo (tempo ou memória) cresce quando aumentamos o tamanho da entrada.

Pergunta mental:

"Se eu duplicar o tamanho dos dados, o trabalho cresce quanto?"

---

## 8. Big-O sem medo

Big-O descreve tendência de crescimento, não tempo exato em segundos.

### Formas comuns

- `O(1)` constante;
- `O(log n)` logarítmica;
- `O(n)` linear;
- `O(n log n)` quase linear;
- `O(n^2)` quadrática.

### Leitura intuitiva

- `O(1)`: custo praticamente fixo;
- `O(n)`: custo cresce proporcionalmente aos dados;
- `O(n^2)`: cresce muito rapidamente com dados grandes.

### Exemplo mental rápido

Se um algoritmo passa de 1 000 para 10 000 elementos:

- `O(n)` cresce cerca de 10x;
- `O(n^2)` cresce cerca de 100x.

É por isso que escolhas de estrutura importam muito em escalas maiores.

---

## 9. Comparação simplificada de estruturas

| Estrutura | Ponto forte | Limitação típica |
| --- | --- | --- |
| Lista (array dinâmico) | acesso por índice rápido | inserir/remover no meio pode ser caro |
| Pilha | inserir/remover no topo é simples e rápido | acesso restrito ao topo |
| Fila | ordem FIFO natural | acesso aleatório não é foco |
| Lista ligada | flexível em inserções/remoções | pesquisa/acesso por posição pode ser mais lento |
| Árvore binária | boa organização hierárquica | pode degradar se ficar desequilibrada |
| Dicionário | acesso por chave rápido em média | não substitui todas as estruturas |

---

## 10. Erros comuns (e correções)

### Erro 1
"A estrutura mais rápida é sempre a melhor."

**Correção:** depende da operação principal (pesquisar? inserir? remover? manter ordem?).

### Erro 2
"Big-O dá o tempo exato."

**Correção:** Big-O dá tendência de crescimento, não segundos exatos.

### Erro 3
"Dicionário resolve qualquer problema."

**Correção:** excelente para chave-valor, mas não substitui pilhas, filas, árvores, etc.

---

## 11. Resumo final

- Estruturas dinâmicas adaptam-se ao crescimento dos dados.
- Pilha usa LIFO; fila usa FIFO.
- Lista ligada usa nós e referências.
- Árvores modelam hierarquia.
- Dicionários são muito úteis para acesso por chave.
- Big-O ajuda a antecipar desempenho quando os dados crescem.

---

## 12. Changelog

- **2026-02-04**: versão inicial do módulo 05.
