# Funções em Python

- [[#Conceitos Fundamentais|Conceitos Fundamentais]]
	- [[#Conceitos Fundamentais#Definição e Propósito|Definição e Propósito]]
	- [[#Conceitos Fundamentais#Anatomia de uma Função|Anatomia de uma Função]]
- [[#Parâmetros e Argumentos|Parâmetros e Argumentos]]
	- [[#Parâmetros e Argumentos#Parâmetros Posicionais|Parâmetros Posicionais]]
	- [[#Parâmetros e Argumentos#Parâmetros com Valores Padrão|Parâmetros com Valores Padrão]]
	- [[#Parâmetros e Argumentos#Argumentos Nomeados (Keywords)|Argumentos Nomeados (Keywords)]]
	- [[#Parâmetros e Argumentos#Parâmetros Variáveis|Parâmetros Variáveis]]
		- [[#Parâmetros Variáveis#*args (Argumentos Posicionais Variáveis)|*args (Argumentos Posicionais Variáveis)]]
		- [[#Parâmetros Variáveis#**kwargs (Argumentos Nomeados Variáveis)|**kwargs (Argumentos Nomeados Variáveis)]]
		- [[#Parâmetros Variáveis#Combinando Diferentes Tipos de Parâmetros|Combinando Diferentes Tipos de Parâmetros]]
- [[#Valores de Retorno|Valores de Retorno]]
	- [[#Valores de Retorno#Return Básico|Return Básico]]
	- [[#Valores de Retorno#Múltiplos Valores de Retorno|Múltiplos Valores de Retorno]]
	- [[#Valores de Retorno#Retorno Implícito|Retorno Implícito]]
- [[#Escopo de Variáveis|Escopo de Variáveis]]
	- [[#Escopo de Variáveis#Escopo Local|Escopo Local]]
	- [[#Escopo de Variáveis#Escopo Global|Escopo Global]]
	- [[#Escopo de Variáveis#Escopo Enclosing (LEGB Rule)|Escopo Enclosing (LEGB Rule)]]
- [[#Funções Lambda|Funções Lambda]]
	- [[#Funções Lambda#Sintaxe e Uso Básico|Sintaxe e Uso Básico]]
	- [[#Funções Lambda#Aplicações Práticas|Aplicações Práticas]]
	- [[#Funções Lambda#Limitações das Funções Lambda|Limitações das Funções Lambda]]
- [[#Decoradores|Decoradores]]
	- [[#Decoradores#Conceito Básico|Conceito Básico]]
	- [[#Decoradores#Decoradores com Parâmetros|Decoradores com Parâmetros]]
- [[#Funções Avançadas|Funções Avançadas]]
	- [[#Funções Avançadas#Funções de Primeira Classe|Funções de Primeira Classe]]
	- [[#Funções Avançadas#Closures|Closures]]
	- [[#Funções Avançadas#Geradores (Generator Functions)|Geradores (Generator Functions)]]
- [[#Documentação de Funções|Documentação de Funções]]
	- [[#Documentação de Funções#Docstrings|Docstrings]]
	- [[#Documentação de Funções#Type Hints|Type Hints]]
- [[#Tratamento de Erros em Funções|Tratamento de Erros em Funções]]
	- [[#Tratamento de Erros em Funções#Exceções Personalizadas|Exceções Personalizadas]]
	- [[#Tratamento de Erros em Funções#Tratamento Robusto de Erros|Tratamento Robusto de Erros]]
- [[#Exercícios Práticos|Exercícios Práticos]]
	- [[#Exercícios Práticos#Exercício 1: Calculadora de Juros Compostos|Exercício 1: Calculadora de Juros Compostos]]
	- [[#Exercícios Práticos#Exercício 2: Analisador de Texto|Exercício 2: Analisador de Texto]]
	- [[#Exercícios Práticos#Exercício 3: Sistema de Cache com Decorador|Exercício 3: Sistema de Cache com Decorador]]
- [[#Boas Práticas e Convenções|Boas Práticas e Convenções]]
	- [[#Boas Práticas e Convenções#Nomenclatura de Funções|Nomenclatura de Funções]]
	- [[#Boas Práticas e Convenções#Princípio da Responsabilidade Única|Princípio da Responsabilidade Única]]
	- [[#Boas Práticas e Convenções#Testabilidade|Testabilidade]]
- [[#Conclusão|Conclusão]]
## Conceitos Fundamentais

### Definição e Propósito

Uma função em Python é um bloco de código organizado e reutilizável que executa uma tarefa específica. As funções promovem a modularidade do código, facilitam a manutenção e evitam repetições desnecessárias. Elas recebem dados de entrada (parâmetros), processam esses dados e podem retornar um resultado.

A estrutura básica de uma função segue o paradigma de entrada-processamento-saída, onde os parâmetros representam a entrada, o corpo da função contém o processamento, e a instrução `return` fornece a saída. Este modelo permite a decomposição de problemas complexos em subproblemas menores e mais gerenciáveis.

### Anatomia de uma Função

```python
def nome_da_funcao(parametro1, parametro2):
    """
    Docstring - documentação da função
    """
    # Corpo da função
    resultado = parametro1 + parametro2
    return resultado
```

A palavra-chave `def` inicia a definição da função, seguida pelo nome da função e uma lista de parâmetros entre parênteses. O dois-pontos marca o início do bloco de código da função, que deve estar indentado. A docstring (opcional, mas recomendada) fornece documentação sobre o propósito e uso da função.

## Parâmetros e Argumentos

### Parâmetros Posicionais

Os parâmetros posicionais são definidos na ordem em que aparecem na declaração da função e devem ser fornecidos na mesma ordem durante a chamada. Esta é a forma mais básica de passagem de argumentos.

```python
def calcular_area_retangulo(largura, altura):
    """Calcula a área de um retângulo"""
    return largura * altura

# Chamada da função
area = calcular_area_retangulo(5, 3)  # largura=5, altura=3
```


### Parâmetros com Valores Padrão

Python permite definir valores padrão para parâmetros, tornando-os opcionais durante a chamada da função. Os parâmetros com valores padrão devem sempre aparecer após os parâmetros obrigatórios na definição.

```python
def cumprimentar(nome, saudacao="Olá", pontuacao="!"):
    """Cria uma mensagem de cumprimento personalizada"""
    return f"{saudacao}, {nome}{pontuacao}"

# Diferentes formas de chamada
print(cumprimentar("Ana"))  # Usa valores padrão
print(cumprimentar("Carlos", "Bom dia"))  # Personaliza saudação
print(cumprimentar("Maria", "Oi", "."))  # Personaliza tudo
```


### Argumentos Nomeados (Keywords)

Os argumentos podem ser passados explicitamente pelo nome do parâmetro, permitindo alterar a ordem dos argumentos e tornando o código mais legível e menos propenso a erros.

```python
def criar_perfil(nome, idade, cidade, profissao):
    return f"{nome}, {idade} anos, {profissao} em {cidade}"

# Usando argumentos nomeados
perfil = criar_perfil(cidade="São Paulo", nome="João", 
                      profissao="Engenheiro", idade=30)
```


### Parâmetros Variáveis

#### *args (Argumentos Posicionais Variáveis)

O parâmetro `*args` permite que uma função aceite qualquer número de argumentos posicionais, que são recebidos como uma tupla.

```python
def somar_todos(*numeros):
    """Soma qualquer quantidade de números"""
    return sum(numeros)

# Exemplos de uso
print(somar_todos(1, 2, 3))        # 6
print(somar_todos(10, 20, 30, 40)) # 100
print(somar_todos())               # 0
```


#### **kwargs (Argumentos Nomeados Variáveis)

O parâmetro `**kwargs` permite que uma função aceite qualquer número de argumentos nomeados, que são recebidos como um dicionário.

```python
def criar_configuracao(**opcoes):
    """Cria um dicionário de configurações"""
    config = {"versao": "1.0"}
    config.update(opcoes)
    return config

# Exemplo de uso
config = criar_configuracao(debug=True, porta=8080, host="localhost")
```


#### Combinando Diferentes Tipos de Parâmetros

A ordem correta para definir parâmetros é: posicionais obrigatórios, posicionais com padrão, `*args`, parâmetros nomeados, `**kwargs`.

```python
def funcao_completa(pos1, pos2, padrao="valor", *args, kwonly, **kwargs):
    """Demonstra todos os tipos de parâmetros"""
    print(f"Posicionais: {pos1}, {pos2}")
    print(f"Padrão: {padrao}")
    print(f"Args extras: {args}")
    print(f"Keyword only: {kwonly}")
    print(f"Kwargs: {kwargs}")
```


## Valores de Retorno

### Return Básico

A instrução `return` especifica o valor que a função deve retornar ao código que a chamou. Uma função pode ter múltiplas instruções `return`, mas apenas uma será executada.

```python
def classificar_numero(numero):
    """Classifica um número como positivo, negativo ou zero"""
    if numero > 0:
        return "positivo"
    elif numero < 0:
        return "negativo"
    else:
        return "zero"
```


### Múltiplos Valores de Retorno

Python permite retornar múltiplos valores empacotando-os em uma tupla. Essa tupla pode ser desempacotada durante a atribuição.

```python
def calcular_estatisticas(numeros):
    """Calcula média, máximo e mínimo de uma lista"""
    if not numeros:
        return None, None, None
    
    media = sum(numeros) / len(numeros)
    maximo = max(numeros)
    minimo = min(numeros)
    
    return media, maximo, minimo

# Desempacotamento dos valores retornados
media, max_val, min_val = calcular_estatisticas([1, 2, 3, 4, 5])
```


### Retorno Implícito

Se uma função não contém uma instrução `return` explícita, ela retorna `None` implicitamente. Isso é útil para funções que executam ações sem produzir um valor específico.

```python
def imprimir_relatorio(dados):
    """Imprime um relatório - não retorna valor"""
    for item in dados:
        print(f"Item: {item}")
    # Retorna None implicitamente
```


## Escopo de Variáveis

### Escopo Local

Variáveis definidas dentro de uma função possuem escopo local, sendo acessíveis apenas dentro dessa função. Elas são criadas quando a função é chamada e destruídas quando a função termina.

```python
def funcao_exemplo():
    variavel_local = "Só existe aqui"
    print(variavel_local)

funcao_exemplo()
# print(variavel_local)  # Erro: variável não existe fora da função
```


### Escopo Global

Variáveis definidas no nível do módulo possuem escopo global e podem ser acessadas por qualquer função no mesmo módulo. Para modificar uma variável global dentro de uma função, usa-se a palavra-chave `global`.

```python
contador_global = 0

def incrementar_contador():
    global contador_global
    contador_global += 1

incrementar_contador()
print(contador_global)  # 1
```


### Escopo Enclosing (LEGB Rule)

Python segue a regra LEGB para resolução de escopo: Local, Enclosing, Global, Built-in. Variáveis são procuradas nessa ordem hierárquica.

```python
x = "global"

def externa():
    x = "enclosing"
    
    def interna():
        x = "local"
        print(f"Interna: {x}")
    
    interna()
    print(f"Externa: {x}")

externa()
print(f"Global: {x}")
```


## Funções Lambda

### Sintaxe e Uso Básico

Funções lambda são funções anônimas de uma linha, úteis para operações simples que podem ser definidas inline. Elas são frequentemente usadas com funções como `map()`, `filter()` e `sorted()`.

```python
# Função lambda básica
quadrado = lambda x: x ** 2
print(quadrado(5))  # 25

# Equivalente usando def
def quadrado_tradicional(x):
    return x ** 2
```


### Aplicações Práticas

```python
# Com map() - aplicar função a cada elemento
numeros = [1, 2, 3, 4, 5]
quadrados = list(map(lambda x: x ** 2, numeros))

# Com filter() - filtrar elementos
pares = list(filter(lambda x: x % 2 == 0, numeros))

# Com sorted() - ordenação personalizada
pessoas = [("Ana", 25), ("Carlos", 30), ("Beatriz", 22)]
por_idade = sorted(pessoas, key=lambda pessoa: pessoa[1])
```


### Limitações das Funções Lambda

Funções lambda são limitadas a expressões simples e não podem conter instruções como `print()`, `return` ou estruturas de controle complexas. Para lógica mais complexa, funções tradicionais são preferíveis.

## Decoradores

### Conceito Básico

Decoradores são uma funcionalidade avançada que permite modificar ou estender o comportamento de funções sem alterar seu código. Eles implementam o padrão de design Decorator usando a sintaxe `@decorator`.

```python
def meu_decorador(func):
    def wrapper(*args, **kwargs):
        print(f"Executando {func.__name__}")
        resultado = func(*args, **kwargs)
        print(f"Finalizando {func.__name__}")
        return resultado
    return wrapper

@meu_decorador
def saudacao(nome):
    return f"Olá, {nome}!"

print(saudacao("Maria"))
```


### Decoradores com Parâmetros

```python
def repetir(vezes):
    def decorador(func):
        def wrapper(*args, **kwargs):
            for _ in range(vezes):
                resultado = func(*args, **kwargs)
            return resultado
        return wrapper
    return decorador

@repetir(3)
def dizer_ola():
    print("Olá!")

dizer_ola()  # Imprime "Olá!" três vezes
```


## Funções Avançadas

### Funções de Primeira Classe

Em Python, funções são objetos de primeira classe, significando que podem ser atribuídas a variáveis, passadas como argumentos e retornadas por outras funções.

```python
def operacao_matematica(func, a, b):
    """Executa uma operação matemática usando a função fornecida"""
    return func(a, b)

def somar(x, y):
    return x + y

def multiplicar(x, y):
    return x * y

# Passando funções como argumentos
resultado1 = operacao_matematica(somar, 5, 3)
resultado2 = operacao_matematica(multiplicar, 5, 3)
```


### Closures

Closures são funções aninhadas que capturam variáveis do escopo da função externa, mantendo acesso a essas variáveis mesmo após a função externa ter terminado.

```python
def criar_multiplicador(fator):
    """Cria uma função que multiplica por um fator específico"""
    def multiplicador(numero):
        return numero * fator
    return multiplicador

# Criando closures
dobrar = criar_multiplicador(2)
triplicar = criar_multiplicador(3)

print(dobrar(5))    # 10
print(triplicar(4)) # 12
```


### Geradores (Generator Functions)

Funções geradoras usam `yield` ao invés de `return` para produzir uma sequência de valores sob demanda, sendo eficientes em memória para grandes conjuntos de dados.

```python
def fibonacci(n):
    """Gera os primeiros n números da sequência Fibonacci"""
    a, b = 0, 1
    for _ in range(n):
        yield a
        a, b = b, a + b

# Usando o gerador
for numero in fibonacci(10):
    print(numero, end=" ")
```


## Documentação de Funções

### Docstrings

Docstrings são strings de documentação que descrevem o propósito, parâmetros e valor de retorno de uma função. Elas são acessíveis através do atributo `__doc__`.

```python
def calcular_imc(peso, altura):
    """
    Calcula o Índice de Massa Corporal (IMC).
    
    Args:
        peso (float): Peso da pessoa em quilogramas
        altura (float): Altura da pessoa em metros
    
    Returns:
        float: O IMC calculado
    
    Raises:
        ValueError: Se peso ou altura forem negativos ou zero
    
    Example:
        >>> calcular_imc(70, 1.75)
        22.857142857142858
    """
    if peso <= 0 or altura <= 0:
        raise ValueError("Peso e altura devem ser positivos")
    
    return peso / (altura ** 2)
```


### Type Hints

Type hints fornecem informações sobre os tipos de parâmetros e retorno, melhorando a legibilidade e permitindo verificação estática de tipos.

```python
from typing import List, Dict, Optional

def processar_dados(numeros: List[float], 
                   config: Dict[str, str]) -> Optional[float]:
    """
    Processa uma lista de números baseado na configuração.
    
    Args:
        numeros: Lista de números para processar
        config: Dicionário de configurações
    
    Returns:
        Resultado processado ou None se a lista estiver vazia
    """
    if not numeros:
        return None
    
    if config.get("operacao") == "media":
        return sum(numeros) / len(numeros)
    elif config.get("operacao") == "soma":
        return sum(numeros)
    else:
        return max(numeros)
```


## Tratamento de Erros em Funções

### Exceções Personalizadas

```python
class IdadeInvalidaError(Exception):
    """Exceção levantada quando uma idade inválida é fornecida"""
    pass

def validar_idade(idade: int) -> bool:
    """
    Valida se a idade está dentro de um range aceitável.
    
    Args:
        idade: A idade a ser validada
    
    Returns:
        True se a idade for válida
    
    Raises:
        IdadeInvalidaError: Se a idade for negativa ou maior que 150
    """
    if idade < 0:
        raise IdadeInvalidaError("Idade não pode ser negativa")
    elif idade > 150:
        raise IdadeInvalidaError("Idade não pode ser maior que 150")
    
    return True
```


### Tratamento Robusto de Erros

```python
def dividir_com_seguranca(a: float, b: float) -> Optional[float]:
    """
    Realiza divisão com tratamento seguro de erros.
    
    Args:
        a: Dividendo
        b: Divisor
    
    Returns:
        Resultado da divisão ou None em caso de erro
    """
    try:
        if b == 0:
            print("Erro: Divisão por zero")
            return None
        
        resultado = a / b
        return resultado
    
    except TypeError:
        print("Erro: Tipos inválidos para divisão")
        return None
    except Exception as e:
        print(f"Erro inesperado: {e}")
        return None
```


## Exercícios Práticos

### Exercício 1: Calculadora de Juros Compostos

```python
def calcular_juros_compostos(principal: float, taxa: float, 
                           tempo: int, composicao: int = 1) -> dict:
    """
    Calcula juros compostos e retorna informações detalhadas.
    
    Args:
        principal: Valor inicial do investimento
        taxa: Taxa de juros anual (como decimal, ex: 0.05 para 5%)
        tempo: Período em anos
        composicao: Frequência de composição por ano
    
    Returns:
        Dicionário com montante final, juros ganhos e evolução anual
    """
    montante = principal * (1 + taxa/composicao) ** (composicao * tempo)
    juros_ganhos = montante - principal
    
    # Calcular evolução ano a ano
    evolucao = []
    for ano in range(1, tempo + 1):
        valor_ano = principal * (1 + taxa/composicao) ** (composicao * ano)
        evolucao.append({"ano": ano, "valor": round(valor_ano, 2)})
    
    return {
        "valor_inicial": principal,
        "montante_final": round(montante, 2),
        "juros_ganhos": round(juros_ganhos, 2),
        "evolucao_anual": evolucao
    }

# Teste da função
resultado = calcular_juros_compostos(1000, 0.08, 5, 12)
print(resultado)
```


### Exercício 2: Analisador de Texto

```python
def analisar_texto(texto: str) -> dict:
    """
    Analisa um texto e retorna estatísticas detalhadas.
    
    Args:
        texto: O texto a ser analisado
    
    Returns:
        Dicionário com estatísticas do texto
    """
    import re
    from collections import Counter
    
    # Limpeza básica
    texto_limpo = texto.strip()
    
    # Contagens básicas
    caracteres = len(texto_limpo)
    caracteres_sem_espacos = len(texto_limpo.replace(" ", ""))
    palavras = len(texto_limpo.split())
    frases = len(re.split(r'[.!?]+', texto_limpo)) - 1
    
    # Análise de palavras
    palavras_lista = re.findall(r'\b\w+\b', texto_limpo.lower())
    palavras_unicas = len(set(palavras_lista))
    palavras_frequentes = Counter(palavras_lista).most_common(5)
    
    # Média de caracteres por palavra
    media_chars_palavra = sum(len(palavra) for palavra in palavras_lista) / len(palavras_lista) if palavras_lista else 0
    
    return {
        "caracteres_total": caracteres,
        "caracteres_sem_espacos": caracteres_sem_espacos,
        "palavras_total": palavras,
        "palavras_unicas": palavras_unicas,
        "frases": frases,
        "media_chars_palavra": round(media_chars_palavra, 2),
        "palavras_mais_frequentes": palavras_frequentes
    }

# Teste da função
texto_exemplo = """Python é uma linguagem de programação. 
                   É fácil de aprender e muito poderosa. 
                   Python é usado em muitas áreas!"""

analise = analisar_texto(texto_exemplo)
print(analise)
```


### Exercício 3: Sistema de Cache com Decorador

```python
from functools import wraps
import time

def cache_com_tempo(tempo_expiracao=60):
    """
    Decorador que implementa cache com expiração por tempo.
    
    Args:
        tempo_expiracao: Tempo em segundos para expiração do cache
    """
    def decorador(func):
        cache = {}
        
        @wraps(func)
        def wrapper(*args, **kwargs):
            # Criar chave do cache
            chave = str(args) + str(sorted(kwargs.items()))
            tempo_atual = time.time()
            
            # Verificar se está no cache e não expirou
            if (chave in cache and 
                tempo_atual - cache[chave]["timestamp"] < tempo_expiracao):
                print(f"Cache hit para {func.__name__}")
                return cache[chave]["valor"]
            
            # Executar função e cachear resultado
            print(f"Cache miss para {func.__name__}")
            resultado = func(*args, **kwargs)
            cache[chave] = {
                "valor": resultado,
                "timestamp": tempo_atual
            }
            
            return resultado
        
        return wrapper
    return decorador

@cache_com_tempo(30)  # Cache expira em 30 segundos
def operacao_custosa(n):
    """Simula uma operação que demora para executar"""
    time.sleep(2)  # Simula processamento
    return sum(range(n))

# Teste do cache
print(operacao_custosa(1000))  # Cache miss
print(operacao_custosa(1000))  # Cache hit
```


## Boas Práticas e Convenções

### Nomenclatura de Funções

- Use nomes descritivos e em snake_case
- Verbos para funções que executam ações: `calcular_total()`, `enviar_email()`
- Predicados (retornam bool) começam com `is_`, `has_`, `can_`: `is_valid()`, `has_permission()`


### Princípio da Responsabilidade Única

Cada função deve ter uma única responsabilidade bem definida. Funções grandes e complexas devem ser decompostas em funções menores.

```python
# Ruim: muitas responsabilidades
def processar_usuario_ruim(dados):
    # Validação
    if not dados.get("email"):
        raise ValueError("Email necessário")
    
    # Processamento
    usuario = criar_usuario(dados)
    
    # Envio de email
    enviar_email_boas_vindas(usuario.email)
    
    # Logging
    log_usuario_criado(usuario.id)
    
    return usuario

# Melhor: responsabilidades separadas
def validar_dados_usuario(dados):
    """Valida dados do usuário"""
    if not dados.get("email"):
        raise ValueError("Email necessário")

def processar_novo_usuario(dados):
    """Processa criação de novo usuário"""
    validar_dados_usuario(dados)
    usuario = criar_usuario(dados)
    enviar_email_boas_vindas(usuario.email)
    log_usuario_criado(usuario.id)
    return usuario
```


### Testabilidade

Funções devem ser projetadas para facilitar testes unitários. Evite efeitos colaterais desnecessários e dependências externas quando possível.

```python
def calcular_desconto_testavel(preco, percentual_desconto, cliente_vip=False):
    """
    Calcula desconto aplicável a um preço.
    Função pura, fácil de testar.
    """
    if not isinstance(preco, (int, float)) or preco < 0:
        raise ValueError("Preço deve ser um número não negativo")
    
    if not 0 <= percentual_desconto <= 1:
        raise ValueError("Percentual deve estar entre 0 e 1")
    
    desconto_base = preco * percentual_desconto
    
    if cliente_vip:
        desconto_base *= 1.1  # 10% extra para VIP
    
    return min(desconto_base, preco)  # Desconto não pode ser maior que o preço
```


## Conclusão

As funções são elementos fundamentais da programação Python, oferecendo mecanismos poderosos para estruturar código de forma modular, reutilizável e maintível. O domínio dos conceitos apresentados neste guia - desde a sintaxe básica até técnicas avançadas como decoradores e closures - é essencial para o desenvolvimento de programas Python eficientes e elegantes.

A prática regular com os exercícios propostos e a aplicação dos princípios de boas práticas contribuirão significativamente para o desenvolvimento de habilidades sólidas em programação Python. Continue explorando e experimentando com diferentes padrões e técnicas para aprofundar sua compreensão sobre este tópico fundamental.

