# Python (10.º Ano) - 00 · Exercicios de preparação

> **Objetivo deste ficheiro**  
> Preparar os alunos para as avaliações, através de exercícios que envolvem os conceitos básicos de Python.

## Preparação para o teste de 05/02/2026

### Exercícios

**Fundamentos (variáveis, operadores, controlo de fluxo, listas e dicionários)**

1. Lê dois números inteiros com `input()`, converte para `int` e imprime a soma, a diferença, o produto, a divisão inteira e o resto.

> Resolução:

```python
num1 = int(input("Introduz o primeiro número inteiro: "))
num2 = int(input("Introduz o segundo número inteiro: "))

soma = num1 + num2
diferenca = num1 - num2
produto = num1 * num2
divisao_inteira = num1 // num2
resto = num1 % num2

print(f"Soma: {soma}")
print(f"Diferença: {diferenca}")
print(f"Produto: {produto}")
print(f"Divisão Inteira: {divisao_inteira}")
print(f"Resto: {resto}")
```

2. Lê uma temperatura em Celsius (`float`) e converte para Fahrenheit. A conversão é dada por: `F = C * 9/5 + 32`. Imprime o resultado.

> Resolução:

```python
celsius = float(input("Introduz a temperatura em Celsius: "))
fahrenheit = celsius * 9/5 + 32
print(f"Temperatura em Fahrenheit: {fahrenheit}")
```

3. Pede ao utilizador o nome e a idade. Imprime uma frase de boas-vindas e indica se é maior de idade.

> Resolução:

```python
nome = input("Introduz o teu nome: ")
idade = int(input("Introduz a tua idade: "))
if idade >= 18:
    status = "maior de idade"
else:
    status = "menor de idade"

print(f"Bem-vindo, {nome}! És {status}.")
```

4. Lê um número inteiro `N` e imprime todos os números pares entre 0 e `N` (inclusive), um por linha.

> Resolução:

```python
N = int(input("Introduz um número inteiro N: "))

for i in range(0, N + 1, 2):
    print(i)

# ou usando condição

for i in range(N + 1):
    if i % 2 == 0:
        print(i)
```

5. Lê 5 notas (0-20), guarda numa lista, calcula a média e indica quantas negativas existem.

> Resolução:

```python
notas = []

for i in range(5):
    nota = float(input(f"Introduz a nota {i + 1} (0-20): "))
    notas.append(nota)

media = sum(notas) / len(notas)
negativas = 0

for nota in notas:
    if nota < 10:
        negativas += 1

print(f"Média: {media}")
print(f"Número de negativas: {negativas}")
```

6. Cria um dicionário para representar um aluno com as chaves `nome`, `turma` e `notas` (lista com 3 valores). Calcula e imprime a média desse aluno.

> Resolução:

```python
aluno = {
    "nome": input("Introduz o nome do aluno: "),
    "turma": input("Introduz a turma do aluno: "),
    "notas": [10, 15, 17, 12]  # Exemplo de notas
}

media = sum(aluno["notas"]) / len(aluno["notas"])
print(f"Média do aluno {aluno['nome']}: {media}")
```

---

**Funções Simples sem retorno**

7. Escreve uma função chamada `saudacao` que recebe um nome como parâmetro e imprime uma mensagem de saudação personalizada.

> Resolução:

```python
def saudacao(nome):
    print(f"Olá, {nome}! Bem-vindo!")

saudacao("Ana")
```

8. Escreve uma função para cada uma das operações matemáticas básicas (adição, subtração, multiplicação, divisão) que recebe dois números como parâmetros e imprime o resultado da operação.

> Resolução:

```python
def adicionar(a, b):
    print(f"Soma: {a + b}")

def subtrair(a, b):
    print(f"Subtração: {a - b}")

def multiplicar(a, b):
    print(f"Multiplicação: {a * b}")

def dividir(a, b):
    if b != 0:
        print(f"Divisão: {a / b}")
    else:
        print("Erro: Divisão por zero não é permitida.")

adicionar(5, 3)
subtrair(5, 3)
multiplicar(5, 3)
dividir(5, 0)
```

9. Cria uma função que calcule a área de um retângulo. A função deve receber a largura e a altura como parâmetros e imprimir a área.

> Resolução:

```python
def area_retangulo(largura, altura):
    area = largura * altura
    print(f"Área do retângulo: {area}")

area_retangulo(5, 10)
```

10. Escreve uma função que receba uma lista de números e imprima cada número multiplicado por 2.

---

**Funções**

11. Rescreve as funções dos exercícios 8 e 9 para que retornem o resultado em vez de o imprimir. Testa as funções imprimindo os valores retornados.

12. Cria uma função que receba uma lista de números e retorne a soma de todos os números pares na lista.

13. Escreve uma função que receba uma string e retorne o número de vogais na string.

14. Cria uma função que receba uma lista de palavras e retorne a palavra mais longa da lista.

15. Escreve uma função que recebe dois parâmetros: uma lista de números e um número. A função deve retornar `True` se o número estiver na lista e `False` caso contrário.

16. Cria uma função que recebe um dicionário e o mostre de forma organizada.

17. Cria uma função que receba uma lista de dicionários (cada dicionário representa uma pessoa com nome e idade) e retorne a média das idades.

18. Considera um dicionário com o seguinte formato:

```python
{
    1 : {
        "nome": "Ana",
        "notas": {
            "Matemática": 18,
            "Física": 16,
            "Química": 17
        },
        "faltas": {
            "Matemática": 2,
            "Física": 0,
            "Química": 1
        }
    }
}
```

Cria funções para:

- Calcular a média das notas de um aluno.
- Calcular o total de faltas de um aluno.
- Mostrar todos os alunos de forma organizada.

---

**Argumentos variáveis (\*args)**

19. Cria uma função que receba um número variável de argumentos e retorne a soma de todos os argumentos.

20. Cria uma função que receba um número variável de argumentos e retorne o maior e o menor número entre eles.

21. Cria uma função que receba um número variável de argumentos e diga quantos são pares e quantos são ímpares.

---

**Ficheiros JSON**

22. Pede ao utilizador para introduzir o nome, idade e cidade. Guarda estes dados num ficheiro JSON com o formato de um dicionário.

23. Lê o ficheiro JSON criado no exercício anterior e imprime os dados de forma organizada.

24. Cria uma função que receba uma lista de dicionários (cada dicionário representa uma pessoa com nome e idade) e guarde esta lista num ficheiro JSON.

25. Cria uma função que leia o ficheiro JSON criado no exercício anterior e retorne a lista de dicionários.

26. Cria um programa que permita ao utilizador gerir uma lista de tarefas (to-do list). O programa deve permitir adicionar, remover e listar tarefas. Os dados devem estar guardados num ficheiro JSON. Sem usar exceções.

27. Cria as funções para um programa que faça a gestão das notas de alunos de uma turma. O programa deve poder guardar os nomes dos alunos e as suas notas nas diferentes disciplinas. O programa deve manter os dados num ficheiro JSON. Deve ser possível consultar a média de cada aluno e se um determinado aluno tem negativas (e quantas).
    O programa deve ter as seguintes funções:
    guardar_dados_alunos -> Função que recebe uma lista de alunos e a grava num ficheiro.
    ler_dados_alunos -> Função que devolve uma lista com os dados dos alunos gravados em ficheiro
    calcula_media -> Função que recebe uma lista de alunos e mostra a média de cada aluno na lista
    devolve_negativas -> Função que recebe um aluno e devolve quantas negativas esse aluno tem.

---

**Exceções e tratamento de erros**

28. Pede um número inteiro ao utilizador e repete o pedido até a conversão para `int` ser válida. Usa `try`/`except` com `ValueError`.

29. Pede dois números e imprime o resultado da divisão. Se o divisor for 0, mostra uma mensagem amigável usando `ZeroDivisionError`.

30. Lê o nome de um ficheiro de texto e tenta abri-lo. Se não existir, mostra uma mensagem adequada usando `FileNotFoundError`.

31. Cria uma função `calcular_raiz_quadrada(n)` que lança `ValueError` se `n` for negativo. Testa a função com valores positivos e negativos.

---

**Módulos e organização de projetos**

32. Cria um módulo `math_utils.py` com as funções `soma(a, b)` e `media(valores)`. Usa-o num `main.py` com `import math_utils`.

33. No mesmo módulo, adiciona testes simples dentro de `if __name__ == "__main__":` e confirma que não correm quando o módulo é importado.

34. Cria um módulo `texto_utils.py` com a função `contar_vogais(texto)` e usa `from texto_utils import contar_vogais` num ficheiro principal.

35. Usa `import random as rd` para gerar 5 números aleatórios entre 1 e 100 e guarda-os numa lista.
