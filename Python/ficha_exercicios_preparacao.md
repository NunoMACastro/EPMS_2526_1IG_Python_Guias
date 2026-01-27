# Ficha de Exercicios - Preparacao (Python 10.º Ano)

## A) Escolha multipla (4 perguntas)

1. Qual e o resultado do seguinte codigo?

```python
a = 17
b = 5
print(a // b, a / b)
```

A) `3 3.4`  
B) `3.4 3`  
C) `2 3.4`  
D) `3 4`

2. Qual das opcoes faz corretamente a leitura de um numero inteiro?

A) `n = input()`  
B) `n = int(input())`  
C) `n = input(int)`  
D) `n = int`

3. O que imprime este codigo?

```python
valores = [0, 1, 2, 3]
for v in valores:
    if v % 2 == 0:
        continue
    print(v)
```

A) `0 2`  
B) `1 3`  
C) `0 1 2 3`  
D) Nada

4. Qual a forma correta de abrir um ficheiro para escrita em Python?

A) `with open("ficheiro.txt", "r") as f:`
B) `with open("ficheiro.txt", "w") as f:`  
C) `with open("ficheiro.txt", "a") as f:`  
D) `with open("ficheiro.txt", "x") as f:`

---

## B) Perguntas gerais(6 perguntas)

1. Le dois numeros inteiros e imprime qual e o maior. Se forem iguais, imprime "Iguais".

2. Le um numero inteiro `N` e mostra todos os números pares entre 1 e N (inclusive).

3. Pede 5 números ao utilizador, guarda numa lista e mostra os números que são positivos.

4. Cria um dicionario para representar um produto com as chaves `nome`, `preco` e `quantidade`. Calcula o valor total de todos os produtos e mostra-o.

5. Escreve uma funcao `media(*numeros)` que receba um numero variavel de argumentos e devolva a media. Testa com pelo menos 4 numeros.

---

## C) Pergunta mais dificil (1 pergunta)

6. Cria um pequeno programa de gestao de alunos com **ficheiro JSON**:

- Cada aluno tem `nome` e `notas` (lista com dicionário).
- O programa deve:
    - ler os dados do ficheiro (se existir)
    - permitir adicionar um novo aluno
    - listar todos os alunos com a media e o numero de negativas
- Organiza o programa em funcoes.

> A resolução deve ser entregue ao professor no final da aula.
