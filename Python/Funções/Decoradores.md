

# Decoradores em Python

- [[#Essência dos decoradores|Essência dos decoradores]]
- [[#Anatomia de um decorador de função|Anatomia de um decorador de função]]
- [[#Decoradores com argumentos (fábricas de decoradores)|Decoradores com argumentos (fábricas de decoradores)]]
- [[#Ordem e composição de múltiplos decoradores|Ordem e composição de múltiplos decoradores]]
- [[#Métodos de instância, classmethod e staticmethod|Métodos de instância, classmethod e staticmethod]]
- [[#Decoradores baseados em classe (stateful)|Decoradores baseados em classe (stateful)]]
- [[#Padrões de uso comuns (idioms)|Padrões de uso comuns (idioms)]]
- [[#Decoradores da biblioteca padrão úteis|Decoradores da biblioteca padrão úteis]]
- [[#Boas práticas|Boas práticas]]
- [[#Armadilhas comuns e mitigação|Armadilhas comuns e mitigação]]
- [[#Integração em frameworks|Integração em frameworks]]
- [[#Tipagem e transformação de classes|Tipagem e transformação de classes]]
- [[#Desempenho e medições|Desempenho e medições]]
- [[#Exemplos práticos recorrentes|Exemplos práticos recorrentes]]
- [[#Quando não usar decoradores|Quando não usar decoradores]]
- [[#Relação com o padrão de projeto Decorator|Relação com o padrão de projeto Decorator]]


## Essência dos decoradores

Um decorador é um callable que recebe outro callable e retorna um novo callable, adicionando comportamento sem alterar o código-fonte original. Em Python, isso funciona porque funções e classes são objetos de primeira classe. A sintaxe @decorator equivale a func = decorator(func).
Benefícios principais:

- Separação de interesses e reuso sem duplicação de código.
- Composição por empilhamento de decoradores (ordem importa).
- Transparência e introspecção preservadas com functools.wraps.


## Anatomia de um decorador de função

Um esqueleto robusto de decorador segue este padrão:

```python
import functools

def my_decorator(func):
    @functools.wraps(func)  # preserva metadados e __wrapped__
    def wrapper(*args, **kwargs):
        # código antes
        result = func(*args, **kwargs)
        # código depois
        return result
    return wrapper
```

Pontos-chave:

- Use *args, **kwargs para aceitar qualquer assinatura.
- wraps copia __name__, __doc__, __qualname__, __module__, __annotations__ e define __wrapped__ para melhor debug, help(), ferramentas e type checkers.


## Decoradores com argumentos (fábricas de decoradores)

Quando o decorador precisa de parâmetros, crie uma fábrica que retorna o decorador:

```python
import functools

def retry(times=3):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            last_exc = None
            for _ in range(times):
                try:
                    return func(*args, **kwargs)
                except Exception as exc:
                    last_exc = exc
            raise last_exc
        return wrapper
    return decorator
```

Uso: @retry(times=5). Esse padrão é descrito como decorator factory e é a forma idiomática para aceitar parâmetros.

Padrão opcional-duplo (usar como @dec e @dec(...)):

```python
import functools

def dec(_func=None, *, enabled=True):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            if not enabled:
                return func(*args, **kwargs)
            # comportamento
            return func(*args, **kwargs)
        return wrapper
    return decorator if _func is None else decorator(_func)
```


## Ordem e composição de múltiplos decoradores

Decoradores são aplicados de baixo para cima (o mais próximo da função é aplicado primeiro). A ordem altera o comportamento final pois cada decorador envolve a saída do anterior. Documente composições sensíveis e teste a ordem esperada.

## Métodos de instância, classmethod e staticmethod

- Métodos de instância decorados continuam recebendo self normalmente.
- classmethod altera o primeiro parâmetro para cls; staticmethod não recebe self/cls. A aplicação de decoradores é idêntica, mas atente ao contexto e assinatura.
- property é um decorador especial para acesso como atributo (com .setter/.deleter). Interações com classmethod/staticmethod têm nuances e limitações (ex.: encadeamento de @classmethod com @property).

Exemplo:

```python
class Svc:
    @staticmethod
    @my_decorator
    def util(x):
        return x * 2

    @classmethod
    @my_decorator
    def make(cls, x):
        return cls()
```


## Decoradores baseados em classe (stateful)

Qualquer objeto chamável pode ser um decorador. Classes com __call__ permitem estado interno e exposição de atributos de controle:

```python
import functools, time

class Timer:
    def __init__(self, func):
        functools.update_wrapper(self, func)
        self.func = func
    def __call__(self, *args, **kwargs):
        t0 = time.perf_counter()
        try:
            return self.func(*args, **kwargs)
        finally:
            dt = time.perf_counter() - t0
            print(f"{self.func.__name__} took {dt:.6f}s")
```

Uso: @Timer. update_wrapper fornece efeito equivalente a wraps ao decorar callables não-função.

## Padrões de uso comuns (idioms)

- Logging/auditoria: registrar entradas/saídas/exceções.
- Autenticação/autorização: checagens de permissão antes de executar.
- Caching/memoization: reduzir recomputações caras com @lru_cache.
- Medição de desempenho: temporização com time.perf_counter.
- Validação de argumentos/retornos; retry/backoff em IO.


## Decoradores da biblioteca padrão úteis

- functools.wraps: preserve metadados e __wrapped__.
- functools.lru_cache(maxsize=128): cache LRU para funções puras com argumentos hashable. Exibe cache_info() e cache_clear().
- functools.cache (3.9+): cache sem limite (equivale a lru_cache(None)).
- functools.singledispatch/singledispatchmethod: despacho por tipo do primeiro argumento.
- property com .setter/.deleter; classmethod; staticmethod.

Extensão idiomática de lru_cache, expondo controles:

```python
from functools import lru_cache, wraps

def cached(maxsize=128):
    def deco(func):
        cached_func = lru_cache(maxsize=maxsize)(func)
        @wraps(func)
        def wrapper(*args, **kwargs):
            return cached_func(*args, **kwargs)
        wrapper.cache_clear = cached_func.cache_clear
        wrapper.cache_info = cached_func.cache_info
        return wrapper
    return deco
```


## Boas práticas

- Sempre use @wraps ou update_wrapper para preservar introspecção, docstrings, annotations e __wrapped__.
- Evite capturar estado mutável implícito; prefira parâmetros claros.
- Documente expectativas: pureza, thread-safety, ordem com outros decoradores.
- Exponha controles: atributos enabled, métodos como cache_clear/cache_info para caches.
- Teste com e sem decorador. __wrapped__ permite chamar a função original ao testar ou medir.


## Armadilhas comuns e mitigação

- Perda de metadados/assinatura: use wraps; melhora help(), IDE, ferramentas e depuração.
- Overhead: todo decorador adiciona ao menos uma chamada. Em hot paths muito curtos, o custo relativo pode ser significativo; meça e reduza lógica de wrapper.
- Ordem de aplicação: altera semântica. Especifique/valide a ordem em composições (ex.: validações antes de cache, IO-retry ao redor de chamadas).
- Caches e métodos: atente a hashabilidade de argumentos e ao binding self/cls; exponha limpeza (cache_clear) quando necessário.
- Interação com propriedades e métodos especiais: encadeamentos com property/classmethod têm limitações.


## Integração em frameworks

- Flask: “view decorators” para autenticação, rate limit, headers e caching de resposta.[^21]
- Testes e infraestrutura: marcações, parametrização e skips via decoradores; despacho com singledispatch para algoritmos.


## Tipagem e transformação de classes

Decoradores podem transformar classes (como dataclasses). typing.dataclass_transform instrui type checkers sobre decoradores que geram construtores/eq/order, garantindo boa experiência de tipos e lint.
## Desempenho e medições

- Meça com time.perf_counter; para microbenchmarks, use timeit e testes controlados.
- Em cenários reais, ganhos de cache/memoization tendem a suplantar o custo do wrapper.


## Exemplos práticos recorrentes

Temporização simples:

```python
import time, functools

def timed(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        t0 = time.perf_counter()
        try:
            return func(*args, **kwargs)
        finally:
            dt = time.perf_counter() - t0
            print(f"{func.__name__}: {dt:.3f}s")
    return wrapper
```

Autorização (conceitual):

```python
import functools

def require(role):
    def deco(func):
        @functools.wraps(func)
        def wrapper(user, *args, **kwargs):
            if role not in user.roles:
                raise PermissionError("forbidden")
            return func(user, *args, **kwargs)
        return wrapper
    return deco
```


## Quando não usar decoradores

- Lógica altamente específica e não reutilizável: prefira chamadas explícitas ou helpers.
- Depuração/manutenção prejudicadas por opacidade: considere context managers/funções auxiliares.
- Hot paths extremamente sensíveis a latência: inline pode ser mais apropriado.


## Relação com o padrão de projeto Decorator

O recurso de linguagem “decorator” em Python reflete o padrão estrutural Decorator: empilhar wrappers que preservam a interface para adicionar capacidades incrementalmente. Em Python, a técnica é leve (açúcar sintático), mas a ideia de composição e transparência permanece.

***


