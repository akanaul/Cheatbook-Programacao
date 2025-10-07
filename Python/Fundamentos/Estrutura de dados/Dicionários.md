# Dicionários em Python

Os dicionários representam uma das estruturas de dados mais versáteis e amplamente utilizadas em Python, oferecendo uma forma eficiente de armazenar e manipular dados através de pares chave-valor.

- [[#Conceitos Fundamentais|Conceitos Fundamentais]]
	- [[#Conceitos Fundamentais#Definição e Características|Definição e Características]]
	- [[#Conceitos Fundamentais#Sintaxe Básica e Criação|Sintaxe Básica e Criação]]
- [[#Operações Fundamentais|Operações Fundamentais]]
	- [[#Operações Fundamentais#Acesso e Modificação de Elementos|Acesso e Modificação de Elementos]]
	- [[#Operações Fundamentais#Remoção de Elementos|Remoção de Elementos]]
- [[#Métodos Essenciais|Métodos Essenciais]]
	- [[#Métodos Essenciais#Métodos de Consulta e Iteração|Métodos de Consulta e Iteração]]
	- [[#Métodos Essenciais#Métodos de Atualização e Combinação|Métodos de Atualização e Combinação]]
- [[#Estruturas Avançadas|Estruturas Avançadas]]
	- [[#Estruturas Avançadas#Dicionários Aninhados|Dicionários Aninhados]]
	- [[#Estruturas Avançadas#Dictionary Comprehensions|Dictionary Comprehensions]]
- [[#Casos de Uso Práticos|Casos de Uso Práticos]]
	- [[#Casos de Uso Práticos#Contadores e Frequências|Contadores e Frequências]]
	- [[#Casos de Uso Práticos#Cache e Memoização|Cache e Memoização]]
	- [[#Casos de Uso Práticos#Mapeamento e Transformação de Dados|Mapeamento e Transformação de Dados]]
- [[#Comparação com Outras Estruturas|Comparação com Outras Estruturas]]
	- [[#Comparação com Outras Estruturas#Dicionários vs Listas|Dicionários vs Listas]]
	- [[#Comparação com Outras Estruturas#Dicionários vs Tuplas Nomeadas|Dicionários vs Tuplas Nomeadas]]
- [[#Boas Práticas e Armadilhas|Boas Práticas e Armadilhas]]
	- [[#Boas Práticas e Armadilhas#Práticas Recomendadas|Práticas Recomendadas]]
	- [[#Boas Práticas e Armadilhas#Armadilhas Comuns|Armadilhas Comuns]]
- [[#Performance e Otimização|Performance e Otimização]]
	- [[#Performance e Otimização#Análise de Complexidade|Análise de Complexidade]]
	- [[#Performance e Otimização#Otimizações Avançadas|Otimizações Avançadas]]
- [[#Conclusão|Conclusão]]

## Conceitos Fundamentais

### Definição e Características

Um dicionário em Python é uma coleção não ordenada de elementos onde cada elemento é armazenado como um par chave-valor. As chaves devem ser únicas e imutáveis (strings, números, tuplas), enquanto os valores podem ser de qualquer tipo de dados, incluindo outros dicionários, listas, objetos ou funções. Esta flexibilidade torna os dicionários extremamente poderosos para modelar dados do mundo real.

A principal vantagem dos dicionários está na sua eficiência de acesso. Enquanto listas requerem busca sequencial para encontrar um elemento específico, os dicionários utilizam uma estrutura de hash table internamente, proporcionando acesso em tempo O(1) na média. Isso significa que independentemente do tamanho do dicionário, o tempo para acessar um valor específico permanece praticamente constante.

### Sintaxe Básica e Criação

A criação de dicionários pode ser realizada através de diferentes métodos, cada um adequado para situações específicas:

```python
# Criação literal com chaves
dicionario_vazio = {}
estudante = {"nome": "João", "idade": 20, "curso": "Programação"}

# Usando o construtor dict()
pessoa = dict(nome="Maria", profissao="Desenvolvedora", salario=5000)

# A partir de listas de tuplas
dados = [("a", 1), ("b", 2), ("c", 3)]
dict_from_tuples = dict(dados)

# Usando dict comprehension
numeros_quadrados = {x: x**2 for x in range(1, 6)}
```

A flexibilidade na criação permite adaptar-se a diferentes cenários de programação, desde inicializações simples até transformações complexas de dados existentes.

## Operações Fundamentais

### Acesso e Modificação de Elementos

O acesso aos valores em dicionários é realizado através das chaves correspondentes, utilizando a notação de colchetes ou métodos específicos:

```python
estudante = {"nome": "Ana", "idade": 22, "notas": [8.5, 9.0, 7.8]}

# Acesso direto
nome = estudante["nome"]
idade = estudante["idade"]

# Acesso seguro com get()
email = estudante.get("email", "não informado")
telefone = estudante.get("telefone")  # Retorna None se não existir

# Modificação de valores existentes
estudante["idade"] = 23
estudante["notas"].append(9.2)

# Adição de novos elementos
estudante["email"] = "ana@email.com"
estudante["ativo"] = True
```

O método `get()` oferece uma alternativa segura ao acesso direto, evitando erros quando uma chave não existe e permitindo a definição de valores padrão. Esta prática é essencial em código robusto, especialmente quando trabalhando com dados externos ou entrada do usuário.

### Remoção de Elementos

Python oferece múltiplas formas de remover elementos de dicionários, cada uma com comportamentos específicos:

```python
dados = {"a": 1, "b": 2, "c": 3, "d": 4}

# Usando del - remove completamente o par chave-valor
del dados["a"]

# Usando pop() - remove e retorna o valor
valor_removido = dados.pop("b")
valor_padrao = dados.pop("inexistente", "não encontrado")

# Usando popitem() - remove e retorna o último par inserido
ultimo_item = dados.popitem()

# Usando clear() - remove todos os elementos
dados.clear()
```

A escolha do método de remoção depende das necessidades específicas: `del` para remoção simples, `pop()` quando o valor removido é necessário, `popitem()` para remoção do último elemento, e `clear()` para limpeza completa.

## Métodos Essenciais

### Métodos de Consulta e Iteração

Os dicionários fornecem métodos específicos para acessar diferentes aspectos dos dados armazenados:

```python
produto = {"nome": "Notebook", "preco": 2500.00, "categoria": "Eletrônicos", "estoque": 15}

# Obter todas as chaves
chaves = produto.keys()
for chave in produto.keys():
    print(f"Chave: {chave}")

# Obter todos os valores
valores = produto.values()
total_valor = sum([v for v in produto.values() if isinstance(v, (int, float))])

# Obter pares chave-valor
items = produto.items()
for chave, valor in produto.items():
    print(f"{chave}: {valor}")

# Verificar existência de chaves
if "preco" in produto:
    print(f"Preço: R$ {produto['preco']}")

# Verificar existência de valores
if 2500.00 in produto.values():
    print("Produto de alto valor encontrado")
```

Estes métodos retornam objetos especiais (dict_keys, dict_values, dict_items) que são eficientes em memória e refletem mudanças no dicionário original. Podem ser convertidos para listas quando necessário usando `list()`.

### Métodos de Atualização e Combinação

```python
usuario_base = {"id": 1, "nome": "Pedro", "ativo": True}
novos_dados = {"email": "pedro@email.com", "telefone": "11999999999", "ativo": False}

# Usando update() para mesclar dicionários
usuario_base.update(novos_dados)
print(usuario_base)  # {'id': 1, 'nome': 'Pedro', 'ativo': False, 'email': 'pedro@email.com', 'telefone': '11999999999'}

# Usando setdefault() para adicionar apenas se não existir
usuario_base.setdefault("data_cadastro", "2024-01-01")
usuario_base.setdefault("nome", "Nome Padrão")  # Não altera pois já existe

# Combinação com operador ** (Python 3.5+)
combinado = {**usuario_base, **{"status": "premium", "pontos": 100}}

# Combinação com operador | (Python 3.9+)
resultado = usuario_base | {"nivel": "avançado", "verificado": True}
```


## Estruturas Avançadas

### Dicionários Aninhados

Dicionários podem conter outros dicionários como valores, criando estruturas hierárquicas complexas ideais para representar dados organizados:

```python
empresa = {
    "informacoes": {
        "nome": "TechCorp",
        "fundacao": 2010,
        "endereco": {
            "rua": "Av. Paulista, 1000",
            "cidade": "São Paulo",
            "cep": "01310-100"
        }
    },
    "departamentos": {
        "ti": {
            "funcionarios": 25,
            "orcamento": 500000,
            "projetos": ["Sistema Web", "App Mobile", "IA"]
        },
        "vendas": {
            "funcionarios": 15,
            "orcamento": 300000,
            "metas": {"trimestre": 1000000, "anual": 4000000}
        }
    }
}

# Acesso a dados aninhados
nome_empresa = empresa["informacoes"]["nome"]
cidade = empresa["informacoes"]["endereco"]["cidade"]
funcionários_ti = empresa["departamentos"]["ti"]["funcionarios"]

# Modificação de dados aninhados
empresa["departamentos"]["ti"]["funcionarios"] += 5
empresa["informacoes"]["endereco"]["complemento"] = "Sala 1001"
```


### Dictionary Comprehensions

As comprehensions de dicionário oferecem uma forma concisa e eficiente de criar novos dicionários baseados em iterações e condições:

```python
# Comprehension básica
quadrados = {x: x**2 for x in range(1, 11)}

# Com condição
pares_quadrados = {x: x**2 for x in range(1, 21) if x % 2 == 0}

# Transformação de dados existentes
notas = {"João": 8.5, "Maria": 9.2, "Pedro": 7.8, "Ana": 9.5}
aprovados = {nome: nota for nome, nota in notas.items() if nota >= 8.0}

# Manipulação de strings
palavras = ["python", "java", "javascript", "go"]
tamanhos = {palavra: len(palavra) for palavra in palavras}

# Combinação com funções
import math
angulos = [0, 30, 45, 60, 90]
senos = {angulo: round(math.sin(math.radians(angulo)), 4) for angulo in angulos}

# Aninhamento com listas
multiplicacao = {i: [i*j for j in range(1, 6)] for i in range(1, 6)}
```


## Casos de Uso Práticos

### Contadores e Frequências

Os dicionários são ideais para implementar contadores, oferecendo uma alternativa eficiente para análise de frequências:

```python
def contar_caracteres(texto):
    contador = {}
    for char in texto.lower():
        if char.isalpha():
            contador[char] = contador.get(char, 0) + 1
    return contador

def contar_palavras(texto):
    palavras = texto.lower().split()
    contador = {}
    for palavra in palavras:
        palavra_limpa = ''.join(c for c in palavra if c.isalnum())
        if palavra_limpa:
            contador[palavra_limpa] = contador.get(palavra_limpa, 0) + 1
    return contador

# Uso prático
texto = "Python é uma linguagem de programação Python"
freq_chars = contar_caracteres(texto)
freq_palavras = contar_palavras(texto)

print("Frequência de caracteres:", freq_chars)
print("Frequência de palavras:", freq_palavras)

# Usando Counter do módulo collections (alternativa)
from collections import Counter
counter_chars = Counter(texto.lower())
counter_palavras = Counter(texto.lower().split())
```


### Cache e Memoização

Dicionários são fundamentais para implementar sistemas de cache que melhoram a performance de funções computacionalmente caras:

```python
# Cache simples para função fibonacci
cache_fibonacci = {}

def fibonacci_com_cache(n):
    if n in cache_fibonacci:
        return cache_fibonacci[n]
    
    if n <= 1:
        resultado = n
    else:
        resultado = fibonacci_com_cache(n-1) + fibonacci_com_cache(n-2)
    
    cache_fibonacci[n] = resultado
    return resultado

# Decorator para memoização automática
def memoize(func):
    cache = {}
    def wrapper(*args):
        if args in cache:
            return cache[args]
        resultado = func(*args)
        cache[args] = resultado
        return resultado
    return wrapper

@memoize
def operacao_cara(a, b, c):
    # Simula operação computacionalmente cara
    return sum(range(a * b * c))

# Teste de performance
import time

start = time.time()
resultado1 = fibonacci_com_cache(35)
tempo1 = time.time() - start

start = time.time()
resultado2 = fibonacci_com_cache(35)  # Segundo acesso (cached)
tempo2 = time.time() - start

print(f"Primeira execução: {tempo1:.4f}s")
print(f"Segunda execução: {tempo2:.4f}s")
```


### Mapeamento e Transformação de Dados

```python
# Mapeamento de códigos para descrições
codigos_erro = {
    404: "Página não encontrada",
    500: "Erro interno do servidor",
    403: "Acesso negado",
    200: "Sucesso",
    301: "Redirecionamento permanente"
}

# Configurações de aplicação
config = {
    "database": {
        "host": "localhost",
        "port": 5432,
        "name": "app_db",
        "user": "admin"
    },
    "api": {
        "version": "v1",
        "timeout": 30,
        "rate_limit": 1000
    },
    "features": {
        "cache_enabled": True,
        "debug_mode": False,
        "ssl_required": True
    }
}

# Função para acessar configurações aninhadas
def get_config(path, default=None):
    keys = path.split('.')
    current = config
    
    for key in keys:
        if isinstance(current, dict) and key in current:
            current = current[key]
        else:
            return default
    
    return current

# Uso da função
db_host = get_config("database.host")
api_version = get_config("api.version")
feature_inexistente = get_config("features.nova_feature", False)
```


## Comparação com Outras Estruturas

### Dicionários vs Listas

A escolha entre dicionários e listas depende das necessidades específicas de acesso e organização dos dados:

```python
# Lista - acesso por índice, ordem mantida
estudantes_lista = ["João", "Maria", "Pedro", "Ana"]
primeiro_estudante = estudantes_lista[0]  # O(1)
busca_maria = "Maria" in estudantes_lista  # O(n)

# Dicionário - acesso por chave, mais flexível
estudantes_dict = {
    "001": {"nome": "João", "idade": 20, "curso": "TI"},
    "002": {"nome": "Maria", "idade": 22, "curso": "Eng"},
    "003": {"nome": "Pedro", "idade": 19, "curso": "Adm"},
    "004": {"nome": "Ana", "idade": 21, "curso": "Med"}
}
info_maria = estudantes_dict["002"]  # O(1)
busca_id = "002" in estudantes_dict  # O(1)

# Comparação de performance
import time

# Teste com lista grande
lista_grande = list(range(100000))
start = time.time()
resultado = 99999 in lista_grande
tempo_lista = time.time() - start

# Teste com dicionário grande
dict_grande = {i: i for i in range(100000)}
start = time.time()
resultado = 99999 in dict_grande
tempo_dict = time.time() - start

print(f"Busca em lista: {tempo_lista:.6f}s")
print(f"Busca em dicionário: {tempo_dict:.6f}s")
```


### Dicionários vs Tuplas Nomeadas

```python
from collections import namedtuple

# Usando dicionário - mutável, flexível
pessoa_dict = {"nome": "Carlos", "idade": 30, "profissao": "Engenheiro"}
pessoa_dict["salario"] = 8000  # Pode adicionar campos
pessoa_dict["idade"] = 31      # Pode modificar valores

# Usando namedtuple - imutável, mais eficiente em memória
Pessoa = namedtuple("Pessoa", ["nome", "idade", "profissao"])
pessoa_tuple = Pessoa("Carlos", 30, "Engenheiro")
# pessoa_tuple.idade = 31  # Erro! Imutável

# Conversão entre formatos
dict_para_tuple = Pessoa(**pessoa_dict)  # Requer campos correspondentes
tuple_para_dict = pessoa_tuple._asdict()

print("Dicionário:", pessoa_dict)
print("Tupla nomeada:", pessoa_tuple)
print("Conversão para dict:", tuple_para_dict)
```


## Boas Práticas e Armadilhas

### Práticas Recomendadas

O uso eficiente de dicionários requer atenção a alguns princípios fundamentais que garantem código limpo, eficiente e manutenível:

```python
# 1. Use chaves consistentes e descritivas
# ❌ Evite
dados = {"n": "João", "i": 25, "p": "Dev"}

# ✅ Prefira
pessoa = {"nome": "João", "idade": 25, "profissao": "Desenvolvedor"}

# 2. Utilize get() para acesso seguro
# ❌ Evite
try:
    email = usuario["email"]
except KeyError:
    email = "não informado"

# ✅ Prefira
email = usuario.get("email", "não informado")

# 3. Use setdefault() para inicialização condicional
# ❌ Evite
if "historico" not in usuario:
    usuario["historico"] = []
usuario["historico"].append("login")

# ✅ Prefira
usuario.setdefault("historico", []).append("login")

# 4. Aproveite defaultdict para casos específicos
from collections import defaultdict

# Para listas
grupos = defaultdict(list)
grupos["admin"].append("user1")
grupos["user"].append("user2")

# Para contadores
contadores = defaultdict(int)
contadores["visits"] += 1
```


### Armadilhas Comuns

```python
# 1. Mutabilidade de valores padrão
def criar_usuario(nome, historico={}):  # ❌ PERIGOSO!
    historico["nome"] = nome
    return historico

# Problema: o mesmo dicionário é reutilizado
user1 = criar_usuario("João")
user2 = criar_usuario("Maria")
print(user1)  # {'nome': 'Maria'} - Inesperado!

# ✅ Solução correta
def criar_usuario_correto(nome, historico=None):
    if historico is None:
        historico = {}
    historico["nome"] = nome
    return historico

# 2. Modificação durante iteração
dados = {"a": 1, "b": 2, "c": 3, "d": 4}

# ❌ Perigoso
for chave in dados:
    if dados[chave] % 2 == 0:
        del dados[chave]  # Pode causar erro

# ✅ Solução segura
chaves_para_remover = [k for k, v in dados.items() if v % 2 == 0]
for chave in chaves_para_remover:
    del dados[chave]

# 3. Cópia superficial vs profunda
original = {"lista": [1, 2, 3], "numero": 10}

# Cópia superficial
copia_rasa = original.copy()
copia_rasa["lista"].append(4)
print(original["lista"])  # [1, 2, 3, 4] - Modificado!

# Cópia profunda
import copy
copia_profunda = copy.deepcopy(original)
copia_profunda["lista"].append(5)
print(original["lista"])  # [1, 2, 3, 4] - Não modificado
```


## Performance e Otimização

### Análise de Complexidade

Compreender a complexidade das operações em dicionários é crucial para escrever código eficiente:

```python
import time
import sys

def testar_performance():
    tamanhos = [1000, 10000, 100000, 1000000]
    
    for tamanho in tamanhos:
        # Criação
        start = time.time()
        d = {i: i**2 for i in range(tamanho)}
        tempo_criacao = time.time() - start
        
        # Acesso
        start = time.time()
        for i in range(min(1000, tamanho)):
            valor = d[i]
        tempo_acesso = time.time() - start
        
        # Busca de chave
        start = time.time()
        existe = (tamanho - 1) in d
        tempo_busca = time.time() - start
        
        # Uso de memória
        memoria = sys.getsizeof(d)
        
        print(f"Tamanho: {tamanho}")
        print(f"  Criação: {tempo_criacao:.4f}s")
        print(f"  Acesso: {tempo_acesso:.4f}s")
        print(f"  Busca: {tempo_busca:.6f}s")
        print(f"  Memória: {memoria} bytes")
        print()

# Comparação com diferentes tipos de chaves
def comparar_tipos_chaves():
    import string
    
    # Chaves inteiras
    dict_int = {i: f"valor_{i}" for i in range(10000)}
    
    # Chaves string
    dict_str = {f"chave_{i}": f"valor_{i}" for i in range(10000)}
    
    # Chaves tupla
    dict_tuple = {(i, i+1): f"valor_{i}" for i in range(10000)}
    
    # Teste de acesso
    start = time.time()
    for i in range(1000):
        v = dict_int[i]
    tempo_int = time.time() - start
    
    start = time.time()
    for i in range(1000):
        v = dict_str[f"chave_{i}"]
    tempo_str = time.time() - start
    
    start = time.time()
    for i in range(1000):
        v = dict_tuple[(i, i+1)]
    tempo_tuple = time.time() - start
    
    print(f"Acesso com chaves int: {tempo_int:.6f}s")
    print(f"Acesso com chaves str: {tempo_str:.6f}s")
    print(f"Acesso com chaves tuple: {tempo_tuple:.6f}s")

# Executar testes
testar_performance()
comparar_tipos_chaves()
```


### Otimizações Avançadas

```python
# 1. Uso eficiente de dict comprehensions
# ❌ Menos eficiente
resultado = {}
for i in range(1000):
    if i % 2 == 0:
        resultado[i] = i ** 2

# ✅ Mais eficiente
resultado = {i: i**2 for i in range(1000) if i % 2 == 0}

# 2. Reutilização de dicionários
# ❌ Criação desnecessária
def processar_dados(items):
    for item in items:
        temp_dict = {"processed": True, "value": item * 2}
        yield temp_dict

# ✅ Reutilização eficiente
def processar_dados_otimizado(items):
    template = {"processed": True, "value": 0}
    for item in items:
        template["value"] = item * 2
        yield template.copy()

# 3. Uso de __slots__ em classes quando apropriado
class PessoaDict:
    def __init__(self, nome, idade):
        self.dados = {"nome": nome, "idade": idade}

class PessoaSlots:
    __slots__ = ['nome', 'idade']
    
    def __init__(self, nome, idade):
        self.nome = nome
        self.idade = idade

# Comparação de memória
import sys
p1 = PessoaDict("João", 25)
p2 = PessoaSlots("João", 25)

print(f"Com dict: {sys.getsizeof(p1.__dict__)} bytes")
print(f"Com slots: {sys.getsizeof(p2)} bytes")
```


## Conclusão

Os dicionários em Python representam uma das estruturas de dados mais fundamentais e versáteis da linguagem, oferecendo uma combinação única de simplicidade sintática e poder computacional. Através desta análise detalhada, observamos como os dicionários transcendem o papel de simples contêineres de dados para se tornarem ferramentas essenciais em praticamente todos os aspectos da programação Python moderna.

A eficiência temporal O(1) para operações básicas de acesso, inserção e remoção torna os dicionários ideais para aplicações que demandam alta performance, enquanto sua flexibilidade na tipagem de chaves e valores permite modelar estruturas de dados complexas de forma intuitiva. As funcionalidades avançadas como dictionary comprehensions, métodos especializados e suporte a estruturas aninhadas ampliam significativamente as possibilidades de uso.

O domínio profundo dos dicionários é fundamental para qualquer desenvolvedor Python, pois eles aparecem em praticamente todos os contextos: desde configurações de aplicação e cache de dados até estruturas complexas em frameworks web e bibliotecas de ciência de dados. A compreensão das melhores práticas, armadilhas comuns e técnicas de otimização apresentadas neste guia fornece a base sólida necessária para utilizar dicionários de forma eficiente e elegante em projetos de qualquer escala e complexidade.

