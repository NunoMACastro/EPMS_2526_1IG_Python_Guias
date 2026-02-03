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

> Resolução:

```python

def multiplica_por_dois(numeros):
    for num in numeros:
        print(num * 2)

lista_numeros = [1, 2, 3, 4, 5]
multiplica_por_dois(lista_numeros)
```

---

**Funções**

11. Rescreve as funções dos exercícios 8 e 9 para que retornem o resultado em vez de o imprimir. Testa as funções imprimindo os valores retornados.

> Resolução:

```python
def adicionar(a, b):
    return a + b
def subtrair(a, b):
    return a - b
def multiplicar(a, b):
    return a * b
def dividir(a, b):
    if b != 0:
        return a / b
    else:
        return "Erro: Divisão por zero não é permitida."

print(f"Soma: {adicionar(5, 3)}")
print(f"Subtração: {subtrair(5, 3)}")
print(f"Multiplicação: {multiplicar(5, 3)}")
print(f"Divisão: {dividir(5, 0)}")

def area_retangulo(largura, altura):
    return largura * altura

print(f"Área do retângulo: {area_retangulo(5, 10)}")
```

12. Cria uma função que receba uma lista de números e retorne a soma de todos os números pares na lista.

> Resolução:

```python
def soma_pares(numeros):
    soma = 0
    for num in numeros:
        if num % 2 == 0:
            soma += num
    return soma
numeros = [1, 2, 3, 4, 5, 6]
resultado = soma_pares(numeros)
print(f"Soma dos números pares: {resultado}")
```

13. Escreve uma função que receba uma string e retorne o número de vogais na string.

> Resolução:

```python
def contar_vogais(texto):
    vogais = "aeiouAEIOUàáéíóúÀÁÉÍÓÚâêîôûÂÊÎÔÛãõÃÕ"
    contador = 0
    for char in texto:
        if char in vogais:
            contador += 1
    return contador
texto = "Olá, como estás?"
resultado = contar_vogais(texto)
print(f"Número de vogais: {resultado}")
```

14. Cria uma função que receba uma lista de palavras e retorne a palavra mais longa da lista.

> Resolução:

```python
def palavra_mais_longa(palavras):
    mais_longa = ""
    for palavra in palavras:
        if len(palavra) > len(mais_longa):
            mais_longa = palavra
    return mais_longa

palavras = ["casa", "computador", "programação", "python"]
resultado = palavra_mais_longa(palavras)
print(f"A palavra mais longa é: {resultado}")
```

15. Escreve uma função que recebe dois parâmetros: uma lista de números e um número. A função deve retornar `True` se o número estiver na lista e `False` caso contrário.

> Resolução:

```python
def numero_na_lista(lista, numero):
    return numero in lista

lista = [1, 2, 3, 4, 5]
numero = 3
resultado = numero_na_lista(lista, numero)
print(f"O número {numero} está na lista? {resultado}")
```

16. Cria uma função que recebe um dicionário e o mostre de forma organizada.

> Resolução:

```python
def mostrar_dicionario(dicionario):
    for chave, valor in dicionario.items():
        print(f"{chave}: {valor}")

meu_dicionario = {
    "nome": "João",
    "idade": 25,
    "cidade": "Lisboa"
}
mostrar_dicionario(meu_dicionario)
```

17. Cria uma função que receba uma lista de dicionários (cada dicionário representa uma pessoa com nome e idade) e retorne a média das idades.

> Resolução

```python

pessoas = [
    {
        "nome" : "Nunão",
        "idade" : 30
    },
    {
        "nome" : "Nuninho",
        "idade" : 16
    }
]

def media_idades(lista_pessoas):
    total_idade = 0
    for pessoa in lista_pessoas:
        total_idade += pessoa["idade"]
    return total_idade / len(lista_pessoas)

resultado = media_idades(pessoas)
print(f"Média das idades: {resultado}")
```

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

> Resolução:

```python
alunos = {
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
    },
    2 : {
        "nome": "Bruno",
        "notas": {
            "Matemática": 14,
            "Física": 12,
            "Química": 15
        },
        "faltas": {
            "Matemática": 1,
            "Física": 3,
            "Química": 0
        }
    }
}

def calcular_media(aluno):
    notas = aluno["notas"].values()
    return sum(notas) / len(notas)

def total_faltas(aluno):
    return sum(aluno["faltas"].values())

def mostrar_alunos(alunos):
    for id, aluno in alunos.items():
        print(f"ID: {id}, Nome: {aluno['nome']}, Média: {calcular_media(aluno)}, Total de Faltas: {total_faltas(aluno)}")

mostrar_alunos(alunos)
```

---

**Argumentos variáveis (\*args)**

19. Cria uma função que receba um número variável de argumentos e retorne a soma de todos os argumentos.

> Resolução:

```python
def soma_variavel(*args):
    return sum(args)

resultado = soma_variavel(1, 2, 3, 4, 5)
print(f"Soma dos argumentos: {resultado}")
```

20. Cria uma função que receba um número variável de argumentos e retorne o maior e o menor número entre eles.

> Resolução:

```python
def maior_menor(*args):
    return max(args), min(args)
maior, menor = maior_menor(10, 3, 5, 7, 2)
print(f"Maior: {maior}, Menor: {menor}")
```

21. Cria uma função que receba um número variável de argumentos e diga quantos são pares e quantos são ímpares.

> Resolução:

```python
def contar_pares_impares(*args):
    pares = 0
    impares = 0
    for num in args:
        if num % 2 == 0:
            pares += 1
        else:
            impares += 1
    return pares, impares
pares, impares = contar_pares_impares(1, 2, 3, 4, 5, 6)
print(f"Número de pares: {pares}, Número de ímpares: {impares}")
```

---

**Ficheiros JSON**

22. Pede ao utilizador para introduzir o nome, idade e cidade. Guarda estes dados num ficheiro JSON com o formato de um dicionário.

> Resolução:

```python
import json

def guardar_dados_json(nome_ficheiro):
    nome = input("Introduz o teu nome: ")
    idade = int(input("Introduz a tua idade: "))
    cidade = input("Introduz a tua cidade: ")

    dados = {
        "nome": nome,
        "idade": idade,
        "cidade": cidade
    }

    with open(nome_ficheiro, 'w') as ficheiro:
        json.dump(dados, ficheiro)
guardar_dados_json('dados_utilizador.json')
```

23. Lê o ficheiro JSON criado no exercício anterior e imprime os dados de forma organizada.

> Resolução:

```python
import json

def ler_dados_json(nome_ficheiro):
    with open(nome_ficheiro, 'r') as ficheiro:
        dados = json.load(ficheiro)
    print("Dados do Utilizador:")
    for chave, valor in dados.items():
        print(f"{chave.capitalize()}: {valor}")

ler_dados_json('dados_utilizador.json')
```

24. Cria uma função que receba uma lista de dicionários (cada dicionário representa uma pessoa com nome e idade) e guarde esta lista num ficheiro JSON.

> Resolução:

```python
import json

def guardar_lista_dicionarios(nome_ficheiro, lista):
    with open(nome_ficheiro, 'w') as ficheiro:
        json.dump(lista, ficheiro)

pessoas = [
    {"nome": "Ana", "idade": 25},
    {"nome": "Bruno", "idade": 30},
    {"nome": "Carla", "idade": 22}
]
guardar_lista_dicionarios('pessoas.json', pessoas)
```

25. Cria uma função que leia o ficheiro JSON criado no exercício anterior e retorne a lista de dicionários.

> Resolução:

```python

import json

def ler_lista_dicionarios(nome_ficheiro):
    with open(nome_ficheiro, 'r') as ficheiro:
        lista = json.load(ficheiro)
    return lista

pessoas = ler_lista_dicionarios('pessoas.json')
for pessoa in pessoas:
    print(f"Nome: {pessoa['nome']}, Idade: {pessoa['idade']}")
```

26. Cria um programa que permita ao utilizador gerir uma lista de tarefas (to-do list). O programa deve permitir adicionar, remover e listar tarefas. Os dados devem estar guardados num ficheiro JSON. Sem usar exceções.

> Resolução:

```python
import json

def carregar_tarefas(nome_ficheiro):
    with open(nome_ficheiro, 'r') as ficheiro:
        return json.load(ficheiro)

def guardar_tarefas(nome_ficheiro, tarefas):
    with open(nome_ficheiro, 'w') as ficheiro:
        json.dump(tarefas, ficheiro)

def adicionar_tarefa(tarefas, tarefa):
    tarefas.append(tarefa)

def remover_tarefa(tarefas, tarefa):
    if tarefa in tarefas:
        tarefas.remove(tarefa)


def listar_tarefas(tarefas):
    for tarefa in tarefas:
        print(f"- {tarefa}")

nome_ficheiro = 'tarefas.json'

try:
    tarefas = carregar_tarefas(nome_ficheiro)
except FileNotFoundError:
    tarefas = []
while True:
    print("\nGestão de Tarefas")
    print("1. Adicionar Tarefa")
    print("2. Remover Tarefa")
    print("3. Listar Tarefas")
    print("4. Sair")
    escolha = input("Escolhe uma opção: ")

    if escolha == '1':
        tarefa = input("Introduz a tarefa a adicionar: ")
        adicionar_tarefa(tarefas, tarefa)
        guardar_tarefas(nome_ficheiro, tarefas)
    elif escolha == '2':
        tarefa = input("Introduz a tarefa a remover: ")
        remover_tarefa(tarefas, tarefa)
        guardar_tarefas(nome_ficheiro, tarefas)
    elif escolha == '3':
        listar_tarefas(tarefas)
    elif escolha == '4':
        break
    else:
        print("Opção inválida. Tenta novamente.")
```

27. Cria as funções para um programa que faça a gestão das notas de alunos de uma turma. O programa deve poder guardar os nomes dos alunos e as suas notas nas diferentes disciplinas. O programa deve manter os dados num ficheiro JSON. Deve ser possível consultar a média de cada aluno e se um determinado aluno tem negativas (e quantas).
    O programa deve ter as seguintes funções:
    guardar_dados_alunos -> Função que recebe uma lista de alunos e a grava num ficheiro.
    ler_dados_alunos -> Função que devolve uma lista com os dados dos alunos gravados em ficheiro
    calcula_media -> Função que recebe uma lista de alunos e mostra a média de cada aluno na lista
    devolve_negativas -> Função que recebe um aluno e devolve quantas negativas esse aluno tem.

> Resolução:

```python

import json

def guardar_dados_alunos(nome_ficheiro, alunos):
    with open(nome_ficheiro, 'w') as ficheiro:
        json.dump(alunos, ficheiro)
def ler_dados_alunos(nome_ficheiro):
    with open(nome_ficheiro, 'r') as ficheiro:
        return json.load(ficheiro)
def calcula_media(alunos):
    for aluno in alunos:
        notas = aluno["notas"].values()
        media = sum(notas) / len(notas)
        print(f"Média de {aluno['nome']}: {media}")
def devolve_negativas(aluno):
    negativas = 0
    for nota in aluno["notas"].values():
        if nota < 10:
            negativas += 1
    return negativas
nome_ficheiro = 'alunos.json'
alunos = [
    {
        "nome": "Ana",
        "notas": {
            "Matemática": 18,
            "Física": 16,
            "Química": 17
        }
    },
    {
        "nome": "Bruno",
        "notas": {
            "Matemática": 14,
            "Física": 9,
            "Química": 15
        }
    }
]
guardar_dados_alunos(nome_ficheiro, alunos)
alunos_carregados = ler_dados_alunos(nome_ficheiro)
calcula_media(alunos_carregados)
for aluno in alunos_carregados:
    negativas = devolve_negativas(aluno)
    print(f"{aluno['nome']} tem {negativas} negativas.")
```

---

**Exceções e tratamento de erros**

28. Pede um número inteiro ao utilizador e repete o pedido até a conversão para `int` ser válida. Usa `try`/`except` com `ValueError`.

> Resolução:

```python
while True:
    entrada = input("Introduz um número inteiro: ")
    try:
        numero = int(entrada)
        print(f"Número introduzido: {numero}")
        break
    except ValueError:
        print("Erro: Por favor, introduz um número inteiro válido.")
```

29. Pede dois números e imprime o resultado da divisão. Se o divisor for 0, mostra uma mensagem amigável usando `ZeroDivisionError`.

> Resolução:

```python
num1 = float(input("Introduz o numerador: "))
num2 = float(input("Introduz o denominador: "))

try:
    resultado = num1 / num2
    print(f"Resultado da divisão: {resultado}")
except ZeroDivisionError:
    print("Erro: Divisão por zero não é permitida.")
```

30. Lê o nome de um ficheiro de texto e tenta abri-lo. Se não existir, mostra uma mensagem adequada usando `FileNotFoundError`.

> Resolução:

```python
nome_ficheiro = input("Introduz o nome do ficheiro de texto: ")
try:
    with open(nome_ficheiro, 'r') as ficheiro:
        conteudo = ficheiro.read()
        print(conteudo)
except FileNotFoundError:
    print("Erro: O ficheiro não foi encontrado.")
```

31. Cria uma função `calcular_raiz_quadrada(n)` que lança `ValueError` se `n` for negativo. Testa a função com valores positivos e negativos.

> Resolução:

```python

import math

def calcular_raiz_quadrada(n):
    if n < 0:
        raise ValueError("Não é possível calcular a raiz quadrada de um número negativo.")
    return math.sqrt(n)

try:
    print(calcular_raiz_quadrada(16))
    print(calcular_raiz_quadrada(-4))
except ValueError as e:
    print(f"Erro: {e}")
```

---

**Módulos e organização de projetos**

32. Cria um módulo `math_utils.py` com as funções `soma(a, b)` e `media(valores)`. Usa-o num `main.py` com `import math_utils`.

33. No mesmo módulo, adiciona testes simples dentro de `if __name__ == "__main__":` e confirma que não correm quando o módulo é importado.

34. Cria um módulo `texto_utils.py` com a função `contar_vogais(texto)` e usa `from texto_utils import contar_vogais` num ficheiro principal.

35. Usa `import random as rd` para gerar 5 números aleatórios entre 1 e 100 e guarda-os numa lista.
