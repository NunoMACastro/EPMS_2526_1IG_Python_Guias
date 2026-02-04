# Memória (10.º Ano) - 03 · Gestão de Memória em Python: Referências, Mutabilidade e Garbage Collection

> **Objetivo deste ficheiro**  
> Compreender, de forma realmente clara, como Python gere memória: o que é uma referência, o que muda entre objetos mutáveis e imutáveis, e como funciona o Garbage Collector.

---

## Índice

- [0. Como usar este ficheiro](#0-como-usar-este-ficheiro)
- [1. Ideia principal: Python gere memória automaticamente](#1-ideia-principal-python-gere-memória-automaticamente)
- [2. Variável não é "caixa de valor" em Python](#2-variável-não-é-caixa-de-valor-em-python)
- [3. Referências na prática](#3-referências-na-prática)
- [4. Mutável vs imutável](#4-mutável-vs-imutável)
- [5. Cópia, alias e efeitos laterais](#5-cópia-alias-e-efeitos-laterais)
- [6. Contagem de referências](#6-contagem-de-referências)
- [7. Garbage Collection e ciclos](#7-garbage-collection-e-ciclos)
- [8. Memory leaks: o que é e como evitar](#8-memory-leaks-o-que-é-e-como-evitar)
- [9. Boas práticas para alunos](#9-boas-práticas-para-alunos)
- [10. Resumo final](#10-resumo-final)
- [11. Changelog](#11-changelog)

---

## 0. Como usar este ficheiro

Este módulo é muito conceptual.  
Lê os exemplos devagar e tenta responder sempre:

- "Isto cria um objeto novo, ou reaproveita um objeto existente?"
- "Esta variável guarda valor, ou guarda referência?"

Se souberes responder a isto, já estás a pensar como programador com base sólida.

---

## 1. Ideia principal: Python gere memória automaticamente

Em linguagens como C, o programador costuma gerir memória de forma manual (alocar/libertar).  
Em Python, a gestão é automática na maioria dos casos.

Isto significa:

- quando precisas de objetos, Python cria-os;
- quando objetos deixam de ser necessários, Python remove-os.

Essa remoção automática acontece através de mecanismos como:

- contagem de referências;
- garbage collection (incluindo deteção de ciclos).

---

## 2. Variável não é "caixa de valor" em Python

Muitos alunos começam com a ideia:

"variável = caixa que guarda valor"

Em Python, uma visão mais correta é:

"variável = nome que aponta para um objeto"

Exemplo:

```python
x = 10
```

Aqui:

- `10` é um objeto (do tipo `int`);
- `x` é uma referência (um nome) que aponta para esse objeto.

### Consequência importante

Quando fazes:

```python
y = x
```

`y` não cria obrigatoriamente um novo objeto com o mesmo conteúdo.  
Na prática inicial, `y` passa a apontar para o mesmo objeto que `x`.

---

## 3. Referências na prática

Podemos observar referências com `id()`:

```python
x = 10
y = x

print(id(x))
print(id(y))
```

Se os `id` forem iguais, significa que `x` e `y` referem o mesmo objeto.

> Nota pedagógica: em Python, certos detalhes de otimização podem variar entre implementações.  
> Para aprendizagem base, o importante é perceberes o conceito de referência.

### Igualdade (`==`) vs identidade (`is`)

Este ponto evita muitos erros:

- `==` compara conteúdo/valor lógico;
- `is` compara identidade (se é exatamente o mesmo objeto).

Exemplo:

```python
a = [1, 2]
b = [1, 2]

print(a == b)  # True (conteúdo igual)
print(a is b)  # False (objetos diferentes)
```

Usa `is` principalmente para `None`.

---

## 4. Mutável vs imutável

Este é um dos conceitos mais importantes do módulo.

### Imutáveis

Objetos imutáveis **não podem ser alterados no local** depois de criados.

Exemplos típicos:

- `int`
- `float`
- `str`
- `tuple`
- `bool`
- `bytes`

Se "alterares" um imutável, Python cria novo objeto.

```python
x = 10
y = x
y = 20

print(x)  # 10
print(y)  # 20
```

### Mutáveis

Objetos mutáveis **podem ser alterados no mesmo local de memória**.

Exemplos típicos:

- `list`
- `dict`
- `set`
- objetos de classes personalizadas (na maioria dos casos)

```python
a = [1, 2, 3]
b = a
b.append(4)

print(a)  # [1, 2, 3, 4]
print(b)  # [1, 2, 3, 4]
```

Porquê? Porque `a` e `b` apontam para a mesma lista mutável.

---

## 5. Cópia, alias e efeitos laterais

### Alias

Quando duas variáveis apontam para o mesmo objeto, tens um alias.

Isso é útil, mas pode causar surpresas.

### Cópia superficial (`copy`)

```python
import copy

lista1 = [[1, 2], [3, 4]]
lista2 = copy.copy(lista1)
```

- Cria nova lista externa;
- elementos internos ainda podem ser referências partilhadas.

### Cópia profunda (`deepcopy`)

```python
import copy

lista1 = [[1, 2], [3, 4]]
lista2 = copy.deepcopy(lista1)
```

- Cria cópia completa, incluindo objetos internos;
- alterações em `lista2` não afetam `lista1`.

### Porque isto importa para alunos?

Porque muitos bugs aparecem quando mudamos uma lista/dicionário sem perceber que outra variável aponta para o mesmo objeto.

---

## 6. Contagem de referências

Python mantém uma contagem de quantas referências apontam para cada objeto.

Ideia simplificada:

- se o objeto tem referências ativas, continua em memória;
- se a contagem chega a zero, o objeto pode ser removido.

Exemplo conceptual:

1. `x = [1, 2]` -> objeto lista criado;
2. `y = x` -> mais uma referência;
3. `del x` -> ainda sobra `y`;
4. `del y` -> sem referências, objeto torna-se elegível para limpeza.

### Nota sobre `sys.getrefcount`

Existe forma de observar contagem de referências com `sys.getrefcount`,  
mas para iniciantes não é obrigatório agora.  
Mais importante é entender a lógica de vida dos objetos.

---

## 7. Garbage Collection e ciclos

A contagem de referências resolve grande parte dos casos, mas não todos.

### Problema dos ciclos

Dois objetos podem apontar um para o outro:

- `objA` referencia `objB`;
- `objB` referencia `objA`.

Mesmo sem variáveis externas a apontar para eles, podem manter contagem acima de zero.

### Solução

Python usa Garbage Collector para detetar e limpar ciclos de referência.

Resumo do processo:

1. Python cria objetos conforme necessário;
2. usa contagem de referências continuamente;
3. periodicamente procura ciclos;
4. remove objetos que já não são alcançáveis.

---

## 8. Memory leaks: o que é e como evitar

Em Python, leaks graves são menos comuns do que em gestão manual, mas podem acontecer.

Exemplos pedagógicos:

- guardar objetos indefinidamente em listas globais;
- criar caches sem limite;
- manter referências sem necessidade;
- abrir recursos e não libertar (ex.: ficheiros, sockets).

### Dica prática

Quando possível:

- limita o tamanho de estruturas em memória;
- reutiliza dados com critério;
- fecha recursos com `with` (ficheiros);
- evita manter referências "esquecidas".

---

## 9. Boas práticas para alunos

1. Usa nomes claros para variáveis (`lista_alunos`, `notas_turma`).
2. Evita criar aliases sem necessidade.
3. Quando precisares de independência entre listas, copia explicitamente.
4. Distingue sempre:
   - "mudar variável para novo objeto";
   - "mudar objeto existente".
5. Não uses `is` para comparar conteúdos de strings/listas; usa `==`.
6. Usa `is` principalmente para `None`.

### Bónus de compreensão: inteiros pequenos e otimizações

Em muitas execuções de CPython, inteiros pequenos (tipicamente entre `-5` e `256`) podem ser reutilizados internamente.

Isto é uma otimização de implementação (não regra pedagógica para escrever lógica).

Conclusão prática:

- não escrevas código a depender desse detalhe;
- usa `==` para comparar valores;
- usa `is` para identidade (`None`).

---

## 10. Resumo final

- Python gere memória automaticamente.
- Variáveis em Python apontam para objetos.
- Objetos imutáveis tendem a gerar novo objeto quando "alterados".
- Objetos mutáveis podem ser alterados no mesmo local.
- Contagem de referências + Garbage Collector garantem limpeza.
- Compreender referências evita muitos erros com listas e dicionários.

---

## 11. Changelog

- **2026-02-04**: versão inicial do módulo 03.
