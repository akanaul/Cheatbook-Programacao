# Função range() em Python

- [[#Introdução|Introdução]]
- [[#Sintaxe Básica|Sintaxe Básica]]
	- [[#Sintaxe Básica#Parâmetros|Parâmetros]]
- [[#Características Importantes|Características Importantes]]
	- [[#Características Importantes#1. Objeto Range|1. Objeto Range]]
	- [[#Características Importantes#2. Conversão para Lista|2. Conversão para Lista]]
	- [[#Características Importantes#3. Eficiência de Memória|3. Eficiência de Memória]]
- [[#Exemplos Práticos|Exemplos Práticos]]
	- [[#Exemplos Práticos#Forma Básica: range(stop)|Forma Básica: range(stop)]]
	- [[#Exemplos Práticos#Forma com Início: range(start, stop)|Forma com Início: range(start, stop)]]
	- [[#Exemplos Práticos#Forma Completa: range(start, stop, step)|Forma Completa: range(start, stop, step)]]
- [[#Casos Especiais|Casos Especiais]]
	- [[#Casos Especiais#Range Decrescente|Range Decrescente]]
	- [[#Casos Especiais#Range Vazio|Range Vazio]]
	- [[#Casos Especiais#Range com Números Negativos|Range com Números Negativos]]
- [[#Aplicações Comuns|Aplicações Comuns]]
	- [[#Aplicações Comuns#1. Loops For Tradicionais|1. Loops For Tradicionais]]
	- [[#Aplicações Comuns#2. Iteração com Índices|2. Iteração com Índices]]
	- [[#Aplicações Comuns#3. Geração de Listas|3. Geração de Listas]]
	- [[#Aplicações Comuns#4. Fatiamento e Indexação|4. Fatiamento e Indexação]]
- [[#Métodos do Objeto Range|Métodos do Objeto Range]]
	- [[#Métodos do Objeto Range#count()|count()]]
	- [[#Métodos do Objeto Range#index()|index()]]
	- [[#Métodos do Objeto Range#Verificação de Pertencimento|Verificação de Pertencimento]]
- [[#Comparação com Outras Abordagens|Comparação com Outras Abordagens]]
	- [[#Comparação com Outras Abordagens#Range vs Lista Manual|Range vs Lista Manual]]
	- [[#Comparação com Outras Abordagens#Range vs While Loop|Range vs While Loop]]
- [[#Dicas e Boas Práticas|Dicas e Boas Práticas]]
	- [[#Dicas e Boas Práticas#1. Uso com enumerate()|1. Uso com enumerate()]]
	- [[#Dicas e Boas Práticas#2. Range Reverso|2. Range Reverso]]
	- [[#Dicas e Boas Práticas#3. Range em Comprehensions|3. Range em Comprehensions]]
- [[#Erros Comuns e Como Evitá-los|Erros Comuns e Como Evitá-los]]
	- [[#Erros Comuns e Como Evitá-los#1. Confundir Stop com Último Valor|1. Confundir Stop com Último Valor]]
	- [[#Erros Comuns e Como Evitá-los#2. Step Igual a Zero|2. Step Igual a Zero]]
	- [[#Erros Comuns e Como Evitá-los#3. Tipos de Dados Incorretos|3. Tipos de Dados Incorretos]]
- [[#Exercícios Práticos|Exercícios Práticos]]
	- [[#Exercícios Práticos#Exercício 1: Tabuada|Exercício 1: Tabuada]]
	- [[#Exercícios Práticos#Exercício 2: Soma de Números Pares|Exercício 2: Soma de Números Pares]]
	- [[#Exercícios Práticos#Exercício 3: Contagem Regressiva|Exercício 3: Contagem Regressiva]]
- [[#Conclusão|Conclusão]]
- [[#Referências Adicionais|Referências Adicionais]]

## Introdução

A função `range()` é uma das funções built-in mais importantes do Python, especialmente útil para criar sequências de números inteiros. É amplamente utilizada em loops, iterações e geração de sequências numéricas de forma eficiente.

## Sintaxe Básica

A função `range()` possui três formas de uso:

```python
range(stop)
range(start, stop)
range(start, stop, step)
```

### Parâmetros

- **start** (opcional): Número inicial da sequência (padrão é 0)
- **stop** (obrigatório): Número final da sequência (não incluído)
- **step** (opcional): Incremento entre os números (padrão é 1)

## Características Importantes

### 1. Objeto Range
A função `range()` não retorna uma lista, mas sim um objeto do tipo `range`. Este objeto é iterável e gera os números sob demanda (lazy evaluation).

```python
# Criando um objeto range
numeros = range(5)
print(type(numeros))  # <class 'range'>
print(numeros)        # range(0, 5)
```

### 2. Conversão para Lista
Para visualizar todos os valores, você pode converter o range em lista:

```python
numeros = range(5)
lista_numeros = list(numeros)
print(lista_numeros)  # [0, 1, 2, 3, 4]
```

### 3. Eficiência de Memória
O objeto `range` é eficiente em termos de memória, pois não armazena todos os valores na memória simultaneamente.

## Exemplos Práticos

### Forma Básica: range(stop)
```python
# Gera números de 0 até 4 (5 não incluído)
for i in range(5):
    print(i)
# Output: 0, 1, 2, 3, 4
```

### Forma com Início: range(start, stop)
```python
# Gera números de 2 até 7 (8 não incluído)
for i in range(2, 8):
    print(i)
# Output: 2, 3, 4, 5, 6, 7
```

### Forma Completa: range(start, stop, step)
```python
# Gera números de 0 até 10 com incremento de 2
for i in range(0, 11, 2):
    print(i)
# Output: 0, 2, 4, 6, 8, 10
```

## Casos Especiais

### Range Decrescente
```python
# Números decrescentes de 10 até 1
for i in range(10, 0, -1):
    print(i)
# Output: 10, 9, 8, 7, 6, 5, 4, 3, 2, 1
```

### Range Vazio
```python
# Range vazio (quando start >= stop com step positivo)
lista_vazia = list(range(5, 2))
print(lista_vazia)  # []

# Range vazio com step negativo incorreto
lista_vazia2 = list(range(2, 5, -1))
print(lista_vazia2)  # []
```

### Range com Números Negativos
```python
# Range com números negativos
negativos = list(range(-5, 0))
print(negativos)  # [-5, -4, -3, -2, -1]
```

## Aplicações Comuns

### 1. Loops For Tradicionais
```python
# Repetir uma ação N vezes
for i in range(3):
    print("Olá, mundo!")
```

### 2. Iteração com Índices
```python
frutas = ["maçã", "banana", "laranja"]
for i in range(len(frutas)):
    print(f"Índice {i}: {frutas[i]}")
```

### 3. Geração de Listas
```python
# Lista de quadrados
quadrados = [x**2 for x in range(1, 6)]
print(quadrados)  # [1, 4, 9, 16, 25]

# Lista de números pares
pares = [x for x in range(0, 21, 2)]
print(pares)  # [0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
```

### 4. Fatiamento e Indexação
```python
# Usando range para criar índices específicos
dados = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
indices_pares = list(range(0, len(dados), 2))
elementos_pares = [dados[i] for i in indices_pares]
print(elementos_pares)  # [10, 30, 50, 70, 90]
```

## Métodos do Objeto Range

### count()
```python
r = range(2, 10, 2)
print(r.count(6))  # 1 (quantas vezes 6 aparece)
print(r.count(5))  # 0 (5 não está na sequência)
```

### index()
```python
r = range(2, 10, 2)
print(r.index(6))  # 2 (índice do valor 6)
```

### Verificação de Pertencimento
```python
r = range(1, 10, 2)
print(5 in r)   # True
print(6 in r)   # False
```

## Comparação com Outras Abordagens

### Range vs Lista Manual
```python
# Usando range (eficiente)
for i in range(1000000):
    pass

# Usando lista (menos eficiente para números grandes)
# numeros = list(range(1000000))  # Consome muita memória
```

### Range vs While Loop
```python
# Com range (mais pythônico)
for i in range(5):
    print(i)

# Com while (mais verboso)
i = 0
while i < 5:
    print(i)
    i += 1
```

## Dicas e Boas Práticas

### 1. Uso com enumerate()
```python
# Quando precisar tanto do índice quanto do valor
frutas = ["maçã", "banana", "laranja"]
for indice, fruta in enumerate(frutas):
    print(f"{indice}: {fruta}")
```

### 2. Range Reverso
```python
# Forma pythônica de iterar em reverso
numeros = [1, 2, 3, 4, 5]
for i in range(len(numeros) - 1, -1, -1):
    print(numeros[i])

# Ou simplesmente
for numero in reversed(numeros):
    print(numero)
```

### 3. Range em Comprehensions
```python
# List comprehension com range
cubos = [x**3 for x in range(1, 6)]
print(cubos)  # [1, 8, 27, 64, 125]

# Dictionary comprehension com range
quadrados_dict = {x: x**2 for x in range(1, 6)}
print(quadrados_dict)  # {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

## Erros Comuns e Como Evitá-los

### 1. Confundir Stop com Último Valor
```python
# INCORRETO: range(5) não inclui o 5
# Para incluir números de 1 a 5:
correto = list(range(1, 6))  # [1, 2, 3, 4, 5]
```

### 2. Step Igual a Zero
```python
# ERRO: ValueError
# range(1, 10, 0)  # Gera erro!
```

### 3. Tipos de Dados Incorretos
```python
# ERRO: range() só aceita inteiros
# range(1.5, 5.5)  # Gera TypeError!

# Solução para números decimais
import numpy as np
decimais = np.arange(1.5, 5.5, 0.5)
```

## Exercícios Práticos

### Exercício 1: Tabuada
```python
# Criar uma tabuada do 7
numero = 7
for i in range(1, 11):
    resultado = numero * i
    print(f"{numero} x {i} = {resultado}")
```

### Exercício 2: Soma de Números Pares
```python
# Somar todos os números pares de 1 a 100
soma_pares = sum(range(2, 101, 2))
print(f"Soma dos pares: {soma_pares}")
```

### Exercício 3: Contagem Regressiva
```python
# Contagem regressiva de 10 até 1
print("Contagem regressiva:")
for i in range(10, 0, -1):
    print(i)
print("Fim!")
```

## Conclusão

A função `range()` é fundamental para programação em Python, especialmente para:

- Loops e iterações controladas
- Geração eficiente de sequências numéricas
- Trabalho com índices em estruturas de dados
- List comprehensions e outras construções pythônicas

Dominar o uso de `range()` é essencial para escrever código Python eficiente e elegante. Pratique os exemplos fornecidos e experimente diferentes combinações de parâmetros para consolidar seu aprendizado.

## Referências Adicionais

- Documentação oficial do Python: `help(range)`
- PEP 289 (Generator Expressions)
- Python Built-in Functions Documentation