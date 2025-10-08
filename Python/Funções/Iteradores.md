# Iteradores em Python

- [[#Introdução|Introdução]]
- [[#O Protocolo de Iteração|O Protocolo de Iteração]]
	- [[#O Protocolo de Iteração#Conceitos Fundamentais|Conceitos Fundamentais]]
	- [[#O Protocolo de Iteração#Diferença entre Iterável e Iterador|Diferença entre Iterável e Iterador]]
- [[#Métodos Fundamentais|Métodos Fundamentais]]
	- [[#Métodos Fundamentais#O Método `__iter__()`|O Método `__iter__()`]]
	- [[#Métodos Fundamentais#O Método `__next__()`|O Método `__next__()`]]
- [[#A Exceção StopIteration|A Exceção StopIteration]]
- [[#Implementando Iteradores Customizados|Implementando Iteradores Customizados]]
	- [[#Implementando Iteradores Customizados#Exemplo Básico: Contador|Exemplo Básico: Contador]]
	- [[#Implementando Iteradores Customizados#Exemplo Avançado: Sequência de Fibonacci|Exemplo Avançado: Sequência de Fibonacci]]
- [[#Separando Iterável de Iterador|Separando Iterável de Iterador]]
- [[#Iteradores Built-in|Iteradores Built-in]]
	- [[#Iteradores Built-in#enumerate()|enumerate()]]
	- [[#Iteradores Built-in#zip()|zip()]]
	- [[#Iteradores Built-in#filter()|filter()]]
	- [[#Iteradores Built-in#map()|map()]]
	- [[#Iteradores Built-in#reversed()|reversed()]]
- [[#O Módulo itertools|O Módulo itertools]]
	- [[#O Módulo itertools#Iteradores Infinitos|Iteradores Infinitos]]
		- [[#Iteradores Infinitos#count()|count()]]
		- [[#Iteradores Infinitos#cycle()|cycle()]]
		- [[#Iteradores Infinitos#repeat()|repeat()]]
	- [[#O Módulo itertools#Iteradores de Terminação|Iteradores de Terminação]]
		- [[#Iteradores de Terminação#chain()|chain()]]
		- [[#Iteradores de Terminação#islice()|islice()]]
		- [[#Iteradores de Terminação#takewhile() e dropwhile()|takewhile() e dropwhile()]]
	- [[#O Módulo itertools#Iteradores Combinatórios|Iteradores Combinatórios]]
		- [[#Iteradores Combinatórios#combinations()|combinations()]]
		- [[#Iteradores Combinatórios#permutations()|permutations()]]
		- [[#Iteradores Combinatórios#product()|product()]]
- [[#Iteradores vs Geradores|Iteradores vs Geradores]]
	- [[#Iteradores vs Geradores#Iteradores|Iteradores]]
	- [[#Iteradores vs Geradores#Geradores|Geradores]]
- [[#Avaliação Preguiçosa (Lazy Evaluation)|Avaliação Preguiçosa (Lazy Evaluation)]]
	- [[#Avaliação Preguiçosa (Lazy Evaluation)#Exemplo de Eficiência de Memória|Exemplo de Eficiência de Memória]]
- [[#Técnicas Avançadas|Técnicas Avançadas]]
	- [[#Técnicas Avançadas#Iterator com Context Manager|Iterator com Context Manager]]
	- [[#Técnicas Avançadas#Iterator Bidirecional|Iterator Bidirecional]]
- [[#Boas Práticas e Padrões de Design|Boas Práticas e Padrões de Design]]
	- [[#Boas Práticas e Padrões de Design#1. Separação de Responsabilidades|1. Separação de Responsabilidades]]
	- [[#Boas Práticas e Padrões de Design#2. Tratamento de Exceções|2. Tratamento de Exceções]]
	- [[#Boas Práticas e Padrões de Design#3. Reutilização de Iteradores|3. Reutilização de Iteradores]]
	- [[#Boas Práticas e Padrões de Design#4. Eficiência de Memória|4. Eficiência de Memória]]
	- [[#Boas Práticas e Padrões de Design#5. Composição de Iteradores|5. Composição de Iteradores]]
	- [[#Boas Práticas e Padrões de Design#6. Documentação Clara|6. Documentação Clara]]
- [[#Performance e Otimização|Performance e Otimização]]
	- [[#Performance e Otimização#Comparação de Performance|Comparação de Performance]]
	- [[#Performance e Otimização#Medindo Performance|Medindo Performance]]
- [[#Cases de Uso Práticos|Cases de Uso Práticos]]
	- [[#Cases de Uso Práticos#1. Processamento de Arquivos Grandes|1. Processamento de Arquivos Grandes]]
	- [[#Cases de Uso Práticos#2. Paginação de APIs|2. Paginação de APIs]]
	- [[#Cases de Uso Práticos#3. Pipeline de Processamento de Dados|3. Pipeline de Processamento de Dados]]
- [[#Considerações Especiais|Considerações Especiais]]
	- [[#Considerações Especiais#Thread Safety|Thread Safety]]
	- [[#Considerações Especiais#Debugging e Testes|Debugging e Testes]]
	- [[#Considerações Especiais#Integração com Async/Await|Integração com Async/Await]]
- [[#Conclusão|Conclusão]]
- [[#Referências|Referências]]

## Introdução

Os iteradores são uma das funcionalidades mais fundamentais e poderosas da linguagem Python, fornecendo uma base elegante para processamento eficiente de dados e criação de loops. Eles implementam o conceito de **avaliação preguiçosa** (lazy evaluation), onde valores são gerados sob demanda, resultando em código mais eficiente em termos de memória e performance.

Um **iterador** é um objeto que contém um número contável de valores e permite percorrer todos esses valores, um de cada vez. Tecnicamente, em Python, um iterador é um objeto que implementa o **protocolo de iteração**, composto pelos métodos `__iter__()` e `__next__()`.

## O Protocolo de Iteração

### Conceitos Fundamentais

O protocolo de iteração em Python consiste em dois componentes essenciais:

1. **Iterable (Iterável)**: Um objeto que implementa o método `__iter__()`, que retorna um iterador
2. **Iterator (Iterador)**: Um objeto que implementa os métodos `__iter__()` e `__next__()`

### Diferença entre Iterável e Iterador

É crucial entender a distinção:

- **Iteráveis** são objetos que podem retornar um iterador quando passados para a função `iter()`
- **Iteradores** são objetos que mantêm estado e produzem valores sequencialmente

Listas, tuplas, dicionários, sets e strings são exemplos de objetos iteráveis built-in do Python. Eles são *containers* iteráveis dos quais você pode obter um iterador.

## Métodos Fundamentais

### O Método `__iter__()`

O método `__iter__()` é fundamental para o protocolo de iteração. Para objetos iteráveis, este método deve retornar um objeto iterador. Para os próprios iteradores, este método deve retornar `self`.

```python
def __iter__(self):
    return self
```

Este método é chamado automaticamente quando:
- Um loop `for` é iniciado
- A função built-in `iter()` é chamada
- Comprehensions são executadas

### O Método `__next__()`

O método `__next__()` é responsável por retornar o próximo item da sequência. Quando não há mais itens para retornar, deve levantar a exceção `StopIteration`.

```python
def __next__(self):
    if self.index >= len(self.data):
        raise StopIteration
    result = self.data[self.index]
    self.index += 1
    return result
```

## A Exceção StopIteration

A exceção `StopIteration` é um mecanismo fundamental do protocolo de iteração. Ela sinaliza o fim da iteração quando um iterador não tem mais elementos para retornar. Esta exceção é:

- **Levantada automaticamente** pelo método `__next__()` quando a sequência termina
- **Capturada internamente** pelos loops `for` e comprehensions
- **Essencial para o funcionamento** correto do protocolo de iteração

```python
try:
    value = next(iterator)
except StopIteration:
    print("Iteração concluída")
```

## Implementando Iteradores Customizados

### Exemplo Básico: Contador

```python
class Contador:
    def __init__(self, inicio, fim):
        self.atual = inicio
        self.fim = fim
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.atual > self.fim:
            raise StopIteration
        else:
            self.atual += 1
            return self.atual - 1

# Uso
contador = Contador(1, 5)
for num in contador:
    print(num)  # Output: 1, 2, 3, 4, 5
```

### Exemplo Avançado: Sequência de Fibonacci

```python
class FibonacciIterator:
    def __init__(self, max_count):
        self.count = 0
        self.max_count = max_count
        self.a, self.b = 0, 1
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.count >= self.max_count:
            raise StopIteration
        self.count += 1
        result = self.a
        self.a, self.b = self.b, self.a + self.b
        return result

# Uso
fibonacci = FibonacciIterator(10)
for num in fibonacci:
    print(num)  # Output: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34
```

## Separando Iterável de Iterador

Uma prática recomendada é separar a implementação do iterável da implementação do iterador:

```python
class FibonacciIterable:
    def __init__(self, max_count):
        self.max_count = max_count
    
    def __iter__(self):
        return FibonacciIterator(self.max_count)

class FibonacciIterator:
    def __init__(self, max_count):
        self.count = 0
        self.max_count = max_count
        self.a, self.b = 0, 1
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.count >= self.max_count:
            raise StopIteration
        self.count += 1
        result = self.a
        self.a, self.b = self.b, self.a + self.b
        return result

# Benefício: permite múltiplas iterações independentes
fib_iterable = FibonacciIterable(5)
for num in fib_iterable:
    print(f"Primeira iteração: {num}")

for num in fib_iterable:
    print(f"Segunda iteração: {num}")
```

## Iteradores Built-in

Python fornece diversos iteradores built-in que retornam objetos iteradores:

### enumerate()
```python
lista = ['a', 'b', 'c']
for indice, valor in enumerate(lista):
    print(f"{indice}: {valor}")
```

### zip()
```python
nomes = ['Alice', 'Bob', 'Charlie']
idades = [25, 30, 35]
for nome, idade in zip(nomes, idades):
    print(f"{nome} tem {idade} anos")
```

### filter()
```python
numeros = [1, 2, 3, 4, 5, 6]
pares = filter(lambda x: x % 2 == 0, numeros)
for par in pares:
    print(par)  # Output: 2, 4, 6
```

### map()
```python
numeros = [1, 2, 3, 4, 5]
quadrados = map(lambda x: x**2, numeros)
for quadrado in quadrados:
    print(quadrado)  # Output: 1, 4, 9, 16, 25
```

### reversed()
```python
lista = [1, 2, 3, 4, 5]
for item in reversed(lista):
    print(item)  # Output: 5, 4, 3, 2, 1
```

## O Módulo itertools

O módulo `itertools` fornece um conjunto de funções que criam iteradores para loops eficientes. É uma ferramenta poderosa para processamento avançado de dados.

### Iteradores Infinitos

#### count()
```python
from itertools import count

# Contador infinito
contador = count(start=10, step=2)
for i, valor in enumerate(contador):
    if i >= 5:
        break
    print(valor)  # Output: 10, 12, 14, 16, 18
```

#### cycle()
```python
from itertools import cycle

# Ciclo infinito através de uma sequência
cores = cycle(['vermelho', 'verde', 'azul'])
for i, cor in enumerate(cores):
    if i >= 6:
        break
    print(cor)  # Output: vermelho, verde, azul, vermelho, verde, azul
```

#### repeat()
```python
from itertools import repeat

# Repetição de um valor
for valor in repeat('Python', 3):
    print(valor)  # Output: Python, Python, Python
```

### Iteradores de Terminação

#### chain()
```python
from itertools import chain

lista1 = [1, 2, 3]
lista2 = [4, 5, 6]
lista3 = [7, 8, 9]

for item in chain(lista1, lista2, lista3):
    print(item)  # Output: 1, 2, 3, 4, 5, 6, 7, 8, 9
```

#### islice()
```python
from itertools import islice

dados = range(100)
# Fatia os elementos do índice 10 ao 20 com passo 2
for item in islice(dados, 10, 20, 2):
    print(item)  # Output: 10, 12, 14, 16, 18
```

#### takewhile() e dropwhile()
```python
from itertools import takewhile, dropwhile

numeros = [1, 3, 5, 8, 9, 11, 13]

# Pega elementos enquanto a condição for verdadeira
for item in takewhile(lambda x: x < 8, numeros):
    print(item)  # Output: 1, 3, 5

# Descarta elementos enquanto a condição for verdadeira
for item in dropwhile(lambda x: x < 8, numeros):
    print(item)  # Output: 8, 9, 11, 13
```

### Iteradores Combinatórios

#### combinations()
```python
from itertools import combinations

letras = ['A', 'B', 'C', 'D']
for combo in combinations(letras, 2):
    print(combo)  # Output: ('A', 'B'), ('A', 'C'), ('A', 'D'), ('B', 'C'), ('B', 'D'), ('C', 'D')
```

#### permutations()
```python
from itertools import permutations

letras = ['A', 'B', 'C']
for perm in permutations(letras, 2):
    print(perm)  # Output: ('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')
```

#### product()
```python
from itertools import product

numeros = [1, 2]
letras = ['A', 'B']
for item in product(numeros, letras):
    print(item)  # Output: (1, 'A'), (1, 'B'), (2, 'A'), (2, 'B')
```

## Iteradores vs Geradores

Embora relacionados, iteradores e geradores têm diferenças importantes:

### Iteradores
- Implementados como classes
- Requerem implementação explícita de `__iter__()` e `__next__()`
- Mais controle sobre o comportamento
- Adequados para lógica complexa de iteração

### Geradores
- Implementados como funções com `yield`
- Protocolo de iteração implementado automaticamente
- Sintaxe mais simples e concisa
- Ideais para sequências simples

```python
# Gerador equivalente ao FibonacciIterator
def fibonacci_generator(max_count):
    count = 0
    a, b = 0, 1
    while count < max_count:
        yield a
        a, b = b, a + b
        count += 1

# Uso idêntico
for num in fibonacci_generator(10):
    print(num)
```

## Avaliação Preguiçosa (Lazy Evaluation)

Os iteradores implementam avaliação preguiçosa, onde:

- **Valores são gerados sob demanda**: Apenas quando necessários
- **Economia de memória**: Não armazena toda a sequência na memória
- **Eficiência computacional**: Permite processamento de grandes datasets
- **Composabilidade**: Iteradores podem ser combinados facilmente

### Exemplo de Eficiência de Memória

```python
# Abordagem não-preguiçosa (ineficiente para grandes datasets)
def numeros_pares_lista(limite):
    return [x for x in range(limite) if x % 2 == 0]

# Abordagem preguiçosa (eficiente)
def numeros_pares_iterator(limite):
    for x in range(limite):
        if x % 2 == 0:
            yield x

# Para limite = 1000000, a abordagem preguiçosa usa muito menos memória
```

## Técnicas Avançadas

### Iterator com Context Manager

```python
class FileLineIterator:
    def __init__(self, filename):
        self.filename = filename
        self.file = None
    
    def __enter__(self):
        self.file = open(self.filename, 'r')
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file:
            self.file.close()
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.file:
            line = self.file.readline()
            if line:
                return line.strip()
        raise StopIteration

# Uso seguro com context manager
with FileLineIterator('arquivo.txt') as lines:
    for line in lines:
        print(line)
```

### Iterator Bidirecional

```python
class BidirectionalIterator:
    def __init__(self, data):
        self.data = data
        self.index = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.index >= len(self.data):
            raise StopIteration
        value = self.data[self.index]
        self.index += 1
        return value
    
    def __prev__(self):
        if self.index <= 0:
            raise StopIteration
        self.index -= 1
        return self.data[self.index]
    
    def previous(self):
        return self.__prev__()

# Uso
bi_iter = BidirectionalIterator([1, 2, 3, 4, 5])
print(next(bi_iter))  # 1
print(next(bi_iter))  # 2
print(bi_iter.previous())  # 1
```

## Boas Práticas e Padrões de Design

### 1. Separação de Responsabilidades
Sempre separe a implementação do iterável da implementação do iterador para permitir múltiplas iterações independentes.

### 2. Tratamento de Exceções
Implemente tratamento adequado da exceção `StopIteration` e garanta que ela seja levantada consistentemente após o esgotamento.

### 3. Reutilização de Iteradores
Lembre-se de que iteradores são "consumidos" após uma iteração completa. Para reutilizar, crie novos iteradores ou use iteráveis.

### 4. Eficiência de Memória
Prefira iteradores para grandes datasets para evitar carregar todos os dados na memória simultaneamente.

### 5. Composição de Iteradores
Use ferramentas como `itertools` para compor iteradores complexos a partir de simples.

### 6. Documentação Clara
Documente o comportamento esperado, especialmente para iteradores customizados com lógica complexa.

## Performance e Otimização

### Comparação de Performance

Os iteradores oferecem vantagens significativas de performance:

- **Menor uso de memória**: Especialmente importante para grandes datasets
- **Lazy evaluation**: Computação apenas quando necessária
- **Melhor localidade de cache**: Processamento item por item
- **Paralelização**: Mais fácil de paralelizar operações em streams

### Medindo Performance

```python
import time
import sys

# Comparação de uso de memória
def lista_completa(n):
    return [x**2 for x in range(n)]

def iterator_lazy(n):
    return (x**2 for x in range(n))

# Medindo tamanho na memória
n = 100000
lista = lista_completa(n)
iterator = iterator_lazy(n)

print(f"Tamanho da lista: {sys.getsizeof(lista)} bytes")
print(f"Tamanho do iterator: {sys.getsizeof(iterator)} bytes")
```

## Cases de Uso Práticos

### 1. Processamento de Arquivos Grandes

```python
def processar_arquivo_grande(filename):
    with open(filename, 'r') as file:
        for linha in file:  # file é um iterador
            # Processa uma linha por vez sem carregar o arquivo inteiro
            yield linha.strip().upper()

# Uso eficiente em memória
for linha_processada in processar_arquivo_grande('arquivo_gigante.txt'):
    print(linha_processada)
```

### 2. Paginação de APIs

```python
class APIPaginator:
    def __init__(self, base_url, page_size=10):
        self.base_url = base_url
        self.page_size = page_size
        self.current_page = 1
        self.has_more = True
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if not self.has_more:
            raise StopIteration
        
        # Simula chamada de API
        data = self.fetch_page(self.current_page)
        self.current_page += 1
        
        if len(data) < self.page_size:
            self.has_more = False
        
        return data
    
    def fetch_page(self, page):
        # Implementação da chamada de API
        pass
```

### 3. Pipeline de Processamento de Dados

```python
def pipeline_dados(fonte_dados):
    # Etapa 1: Filtrar
    dados_filtrados = filter(lambda x: x > 0, fonte_dados)
    
    # Etapa 2: Transformar
    dados_transformados = map(lambda x: x * 2, dados_filtrados)
    
    # Etapa 3: Processar em lotes
    def em_lotes(iterator, tamanho_lote):
        lote = []
        for item in iterator:
            lote.append(item)
            if len(lote) == tamanho_lote:
                yield lote
                lote = []
        if lote:
            yield lote
    
    return em_lotes(dados_transformados, 5)

# Uso do pipeline
dados_origem = range(-10, 20)
for lote in pipeline_dados(dados_origem):
    print(f"Processando lote: {lote}")
```

## Considerações Especiais

### Thread Safety
Iteradores não são thread-safe por padrão. Para uso em ambientes multi-thread, implemente sincronização adequada:

```python
import threading

class ThreadSafeIterator:
    def __init__(self, iterable):
        self.iterator = iter(iterable)
        self.lock = threading.Lock()
    
    def __iter__(self):
        return self
    
    def __next__(self):
        with self.lock:
            return next(self.iterator)
```

### Debugging e Testes
Iteradores podem ser desafiadores para debug devido à sua natureza lazy. Use ferramentas como `itertools.tee()` para criar cópias independentes durante testes.

### Integração com Async/Await
Python 3.5+ introduziu iteradores assíncronos com `__aiter__()` e `__anext__()` para uso com `async for`.

## Conclusão

Os iteradores representam um paradigma fundamental em Python que habilita processamento eficiente e elegante de dados. Eles são a base para muitas funcionalidades avançadas da linguagem, desde loops simples até pipelines complexos de processamento de dados.

Compreender profundamente o protocolo de iteração, as técnicas de implementação e as ferramentas disponíveis como `itertools` é essencial para desenvolver código Python eficiente, legível e escalável. A avaliação preguiçosa proporcionada pelos iteradores permite trabalhar com datasets enormes e streams infinitos de dados de forma eficiente em termos de memória e processamento.

A prática consistente com iteradores customizados e o uso apropriado das ferramentas built-in desenvolverá sua capacidade de escrever código Python mais pythônico e performático.

---

## Referências

- [Python Iterator Protocol - W3Schools](https://www.w3schools.com/python/python_iterators.asp)
- [Iterators and Iterables in Python - Real Python](https://realpython.com/python-iterators-iterables/)
- [Iterators in Python - GeeksforGeeks](https://www.geeksforgeeks.org/python/iterators-in-python/)
- [Python Iterators - Flexiple](https://flexiple.com/python/python-iterators)
- [Python Iterators (With Examples) - Programiz](https://www.programiz.com/python-programming/iterator)
- [itertools — Functions creating iterators for efficient looping - Python Documentation](https://docs.python.org/3/library/itertools.html)
- [Exploring Python: Using and Abusing the Iterator Protocol](https://fronkan.hashnode.dev/exploring-python-using-and-abusing-the-iterator-protocol)
- [Python Iterators with examples - W3Resource](https://www.w3resource.com/python/iterators-with-examples.php)
- [StopIteration | Python's Built-in Exceptions - Real Python](https://realpython.com/ref/builtin-exceptions/stopiteration/)
- [Difference between Python's Generators and Iterators - Stack Overflow](https://stackoverflow.com/questions/2776829/difference-between-pythons-generators-and-iterators)
- [Resolve Stopiteration Error in Python - GeeksforGeeks](https://www.geeksforgeeks.org/python/resolve-stopiteration-error-in-python/)
- [The Iterator Pattern - Python Patterns](https://python-patterns.guide/gang-of-four/iterator/)
- [The Difference Between Iterator And Generator In Python - Scaler](https://www.scaler.com/topics/difference-between-iterator-and-generator-in-python/)
- [Converting an object into an iterator - GeeksforGeeks](https://www.geeksforgeeks.org/python/python-__iter__-__next__-converting-object-iterator/)
- [Are there builtin iterators in Python? - Stack Overflow](https://stackoverflow.com/questions/51927652/are-there-builtin-iterators-in-python)
- [Python | Iterators - Codecademy](https://www.codecademy.com/resources/docs/python/iterators)
- [iter() | Python's Built-in Functions - Real Python](https://realpython.com/ref/builtin-functions/iter/)
- [Implementing a Custom Python Iterator - Python Programming](https://pythonprograming.com/blog/implementing-a-custom-python-iterator-patterns-best-practices-and-real-world-use-cases)
- [Iterator Method - Python Design Patterns - GeeksforGeeks](https://www.geeksforgeeks.org/python/iterator-method-python-design-patterns/)
- [Python Generators vs Iterators - Python Geeks](https://pythongeeks.org/python-generators-vs-iterators/)
- [Iterator in Python / Design Patterns](https://refactoring.guru/design-patterns/iterator/python/example)
- [Difference Between Iterator VS Generator - GeeksforGeeks](https://www.geeksforgeeks.org/python/difference-between-iterator-vs-generator/)
- [Iterator - Python Wiki](https://wiki.python.org/moin/Iterator)
- [How to Implement Custom Iterators and Iterables in Python](https://www.index.dev/blog/custom-iterators-iterables-python)
- [A Guide to Python's itertools Module - Dev.to](https://dev.to/usooldatascience/a-guide-to-pythons-itertools-module-use-cases-and-examples-59e)
- [Python Itertools Module](https://www.pythoncheatsheet.org/modules/itertools-module)
- [Python's itertools for Memory-Efficient Iteration](https://www.nb-data.com/p/pythons-itertools-for-memory-efficient)
- [Lazy Iterators in Python](https://redandgreen.co.uk/lazy-iterators-in-python/python-code/)
- [Python Itertools - GeeksforGeeks](https://www.geeksforgeeks.org/python/python-itertools/)
- [Python Iterator: Syntax, Usage, and Examples](https://mimo.org/glossary/python/iterator)
- [lazy evaluation in Python3 - Stack Overflow](https://stackoverflow.com/questions/60042702/lazy-evaluation-in-python3)
- [Python itertools By Example - Real Python](https://realpython.com/python-itertools/)
- [Performance Advantages to Iterators? - Stack Overflow](https://stackoverflow.com/questions/628903/performance-advantages-to-iterators)