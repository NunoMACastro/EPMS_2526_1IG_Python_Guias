# Python (10.º Ano) - 00 · Exercicios de preparação

> **Objetivo deste ficheiro**  
> Preparar os alunos para as avaliações, através de exercícios que envolvem os conceitos básicos de Python.

## Preparação para o teste de 05/02/2026

### Exercícios

**Fundamentos (variáveis, operadores, controlo de fluxo, listas e dicionários)**

1. Lê dois números inteiros com `input()`, converte para `int` e imprime a soma, a diferença, o produto, a divisão inteira e o resto.

2. Lê uma temperatura em Celsius (`float`) e converte para Fahrenheit. Mostra o resultado com 1 casa decimal.

3. Pede ao utilizador o nome e a idade. Imprime uma frase de boas-vindas e indica se é maior de idade.

4. Lê um número inteiro `N` e imprime todos os números pares entre 0 e `N` (inclusive), um por linha.

5. Lê 5 notas (0-20), guarda numa lista, calcula a média e indica quantas negativas existem.

6. Cria um dicionário para representar um aluno com as chaves `nome`, `turma` e `notas` (lista com 3 valores). Calcula e imprime a média desse aluno.

---

**Funções Simples sem retorno**

7. Escreve uma função chamada `saudacao` que recebe um nome como parâmetro e imprime uma mensagem de saudação personalizada.

8. Escreve uma função para cada uma das operações matemáticas básicas (adição, subtração, multiplicação, divisão) que recebe dois números como parâmetros e imprime o resultado da operação.

9. Cria uma função que calcule a área de um retângulo. A função deve receber a largura e a altura como parâmetros e imprimir a área.

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
