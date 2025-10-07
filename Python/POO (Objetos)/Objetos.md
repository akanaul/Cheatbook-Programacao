
# Objetos em Python

Python é uma linguagem fundamentalmente orientada a objetos, onde praticamente tudo é um objeto.

- [[#Conceitos Fundamentais de Objetos|Conceitos Fundamentais de Objetos]]
	- [[#Conceitos Fundamentais de Objetos#O que são Objetos|O que são Objetos]]
	- [[#Conceitos Fundamentais de Objetos#Classes como Modelos de Objetos|Classes como Modelos de Objetos]]
	- [[#Conceitos Fundamentais de Objetos#Instanciação e Manipulação de Objetos|Instanciação e Manipulação de Objetos]]
- [[#Atributos e Métodos|Atributos e Métodos]]
	- [[#Atributos e Métodos#Tipos de Atributos|Tipos de Atributos]]
	- [[#Atributos e Métodos#Métodos de Instância, Classe e Estáticos|Métodos de Instância, Classe e Estáticos]]
	- [[#Atributos e Métodos#Propriedades e Getters/Setters|Propriedades e Getters/Setters]]
- [[#Herança e Relacionamentos Entre Classes|Herança e Relacionamentos Entre Classes]]
	- [[#Herança e Relacionamentos Entre Classes#Herança Simples|Herança Simples]]
	- [[#Herança e Relacionamentos Entre Classes#Herança Múltipla|Herança Múltipla]]
	- [[#Herança e Relacionamentos Entre Classes#Polimorfismo|Polimorfismo]]
- [[#Encapsulamento e Modificadores de Acesso|Encapsulamento e Modificadores de Acesso]]
	- [[#Encapsulamento e Modificadores de Acesso#Convenções de Visibilidade|Convenções de Visibilidade]]
	- [[#Encapsulamento e Modificadores de Acesso#Validação e Controle de Acesso|Validação e Controle de Acesso]]
- [[#Métodos Especiais e Protocolo de Objetos|Métodos Especiais e Protocolo de Objetos]]
	- [[#Métodos Especiais e Protocolo de Objetos#Métodos Dunder (Magic Methods)|Métodos Dunder (Magic Methods)]]
	- [[#Métodos Especiais e Protocolo de Objetos#Protocolo de Iteração|Protocolo de Iteração]]
	- [[#Métodos Especiais e Protocolo de Objetos#Context Managers (Gerenciadores de Contexto)|Context Managers (Gerenciadores de Contexto)]]
- [[#Conceitos Avançados|Conceitos Avançados]]
	- [[#Conceitos Avançados#Metaclasses|Metaclasses]]
	- [[#Conceitos Avançados#Descritores|Descritores]]
	- [[#Conceitos Avançados#Slots|Slots]]
- [[#Conclusão|Conclusão]]

## Conceitos Fundamentais de Objetos

### O que são Objetos

Em Python, um **objeto** é uma entidade que combina dados (atributos) e comportamentos (métodos) em uma única unidade. Todo valor em Python é um objeto, desde números inteiros até funções complexas. Esta característica torna Python uma linguagem consistente e poderosa para programação orientada a objetos.

Um objeto possui três características essenciais: identidade (um identificador único na memória), tipo (que determina as operações possíveis) e valor (os dados armazenados). A função `id()` retorna a identidade de um objeto, `type()` retorna seu tipo, e o valor é acessado diretamente através do nome do objeto. Compreender essas características é fundamental para trabalhar efetivamente com objetos em Python.

```python
# Exemplo básico de objeto
numero = 42
texto = "Python"
lista = [1, 2, 3]

print(f"ID do número: {id(numero)}")
print(f"Tipo do texto: {type(texto)}")
print(f"Valor da lista: {lista}")
```


### Classes como Modelos de Objetos

Uma **classe** é um modelo ou template que define a estrutura e comportamento de objetos. É como um blueprint que especifica quais atributos (dados) e métodos (funções) os objetos criados a partir dela terão. As classes permitem criar múltiplas instâncias com características similares mas valores diferentes.

A definição de uma classe utiliza a palavra-chave `class`, seguida pelo nome da classe (por convenção, utilizando CamelCase). Dentro da classe, definimos métodos e atributos que serão compartilhados por todas as instâncias. O método especial `__init__` é o construtor da classe, executado automaticamente quando uma nova instância é criada.

```python
class Pessoa:
    # Atributo de classe (compartilhado por todas as instâncias)
    especie = "Homo sapiens"
    
    def __init__(self, nome, idade):
        # Atributos de instância (únicos para cada objeto)
        self.nome = nome
        self.idade = idade
    
    def apresentar(self):
        return f"Olá, eu sou {self.nome} e tenho {self.idade} anos"
    
    def fazer_aniversario(self):
        self.idade += 1
        return f"{self.nome} agora tem {self.idade} anos"
```


### Instanciação e Manipulação de Objetos

A **instanciação** é o processo de criar um objeto específico a partir de uma classe. Cada instância é um objeto independente com seus próprios valores de atributos, embora compartilhem a mesma estrutura definida pela classe. A instanciação é realizada chamando a classe como se fosse uma função.

Após a criação, podemos acessar e modificar atributos dos objetos usando a notação de ponto. É possível adicionar novos atributos dinamicamente a instâncias específicas, uma característica única do Python que oferece grande flexibilidade. Métodos são chamados da mesma forma, utilizando a notação de ponto seguida pelos parênteses com argumentos quando necessário.

```python
# Criando instâncias da classe Pessoa
pessoa1 = Pessoa("Ana", 25)
pessoa2 = Pessoa("Carlos", 30)

# Acessando atributos
print(pessoa1.nome)  # Ana
print(pessoa2.idade)  # 30

# Chamando métodos
print(pessoa1.apresentar())  # Olá, eu sou Ana e tenho 25 anos
print(pessoa2.fazer_aniversario())  # Carlos agora tem 31 anos

# Adicionando atributo dinamicamente
pessoa1.profissao = "Engenheira"
print(pessoa1.profissao)  # Engenheira
```


## Atributos e Métodos

### Tipos de Atributos

Python distingue entre **atributos de classe** e **atributos de instância**. Atributos de classe são compartilhados por todas as instâncias da classe e são definidos diretamente no corpo da classe. Eles representam características comuns a todos os objetos daquela classe e ocupam apenas uma posição na memória, independentemente do número de instâncias criadas.

Atributos de instância são únicos para cada objeto e são geralmente definidos no método `__init__`. Cada instância mantém sua própria cópia desses atributos, permitindo que objetos da mesma classe tenham valores diferentes. Esta distinção é crucial para o design eficiente de classes e o gerenciamento adequado da memória.

```python
class Veiculo:
    # Atributo de classe
    rodas = 4
    combustivel = "Gasolina"
    
    def __init__(self, marca, modelo, ano):
        # Atributos de instância
        self.marca = marca
        self.modelo = modelo
        self.ano = ano
        self.km = 0
    
    def acelerar(self, distancia):
        self.km += distancia
        return f"{self.marca} {self.modelo} percorreu {distancia}km"

# Acessando atributos de classe e instância
carro1 = Veiculo("Toyota", "Corolla", 2020)
carro2 = Veiculo("Honda", "Civic", 2021)

print(carro1.rodas)  # 4 (atributo de classe)
print(carro1.marca)  # Toyota (atributo de instância)
print(carro2.modelo)  # Civic (atributo de instância)

# Modificando atributo de classe afeta todas as instâncias
Veiculo.rodas = 6
print(carro1.rodas)  # 6
print(carro2.rodas)  # 6
```


### Métodos de Instância, Classe e Estáticos

Os **métodos de instância** são os mais comuns e operam sobre uma instância específica da classe. Eles sempre recebem `self` como primeiro parâmetro, que é uma referência à própria instância. Através de `self`, esses métodos podem acessar e modificar tanto atributos de instância quanto atributos de classe do objeto específico.

**Métodos de classe** são definidos com o decorador `@classmethod` e recebem `cls` como primeiro parâmetro, representando a própria classe. Eles são úteis para operações que dizem respeito à classe como um todo, como métodos construtores alternativos ou operações sobre atributos de classe. **Métodos estáticos**, definidos com `@staticmethod`, não recebem referência automática nem para a instância nem para a classe, funcionando como funções normais agrupadas logicamente dentro da classe.

```python
class Contador:
    total_objetos = 0
    
    def __init__(self, valor=0):
        self.valor = valor
        Contador.total_objetos += 1
    
    def incrementar(self):
        """Método de instância"""
        self.valor += 1
    
    @classmethod
    def obter_total_objetos(cls):
        """Método de classe"""
        return cls.total_objetos
    
    @classmethod
    def criar_com_valor_inicial(cls, valor):
        """Construtor alternativo"""
        return cls(valor)
    
    @staticmethod
    def validar_numero(numero):
        """Método estático"""
        return isinstance(numero, (int, float)) and numero >= 0

# Usando diferentes tipos de métodos
c1 = Contador()
c2 = Contador.criar_com_valor_inicial(10)  # Método de classe

c1.incrementar()  # Método de instância
print(f"Valor de c1: {c1.valor}")

print(f"Total de objetos: {Contador.obter_total_objetos()}")  # Método de classe
print(f"Número válido: {Contador.validar_numero(5)}")  # Método estático
```


### Propriedades e Getters/Setters

As **propriedades** em Python permitem criar atributos que se comportam como variáveis simples mas executam código específico quando acessados ou modificados. Isso é implementado através do decorador `@property` para getters e `@atributo.setter` para setters. Esta funcionalidade oferece controle sobre o acesso aos dados sem quebrar a interface externa da classe.

As propriedades são essenciais para implementar **encapsulamento**, um dos princípios fundamentais da programação orientada a objetos. Elas permitem validação de dados, computação de valores derivados e manutenção da consistência interna do objeto. O uso de propriedades torna o código mais robusto e facilita a manutenção futura sem afetar o código cliente.

```python
class TemperaturaMonitor:
    def __init__(self):
        self._celsius = 0  # Atributo "privado" por convenção
    
    @property
    def celsius(self):
        """Getter para temperatura em Celsius"""
        return self._celsius
    
    @celsius.setter
    def celsius(self, valor):
        """Setter com validação"""
        if valor < -273.15:
            raise ValueError("Temperatura não pode ser menor que zero absoluto")
        self._celsius = valor
    
    @property
    def fahrenheit(self):
        """Propriedade computada (somente leitura)"""
        return (self._celsius * 9/5) + 32
    
    @property
    def kelvin(self):
        """Outra propriedade computada"""
        return self._celsius + 273.15

# Usando propriedades
temp = TemperaturaMonitor()
temp.celsius = 25  # Usa o setter
print(f"Celsius: {temp.celsius}")  # Usa o getter
print(f"Fahrenheit: {temp.fahrenheit}")  # Propriedade computada
print(f"Kelvin: {temp.kelvin}")  # Propriedade computada

# temp.celsius = -300  # Levantaria ValueError
```


## Herança e Relacionamentos Entre Classes

### Herança Simples

A **herança** é um mecanismo que permite criar uma nova classe baseada em uma classe existente, herdando seus atributos e métodos. A classe existente é chamada de classe pai, base ou superclasse, enquanto a nova classe é chamada de classe filha, derivada ou subclasse. Este conceito promove reutilização de código e estabelece relacionamentos hierárquicos entre classes.

A herança é implementada especificando a classe pai entre parênteses na definição da classe filha. A subclasse herda automaticamente todos os métodos e atributos públicos da superclasse, podendo também adicionar novos membros ou sobrescrever os existentes. O método `super()` permite acessar membros da classe pai, facilitando a extensão de funcionalidades sem duplicação de código.

```python
class Animal:
    def __init__(self, nome, especie):
        self.nome = nome
        self.especie = especie
        self.energia = 100
    
    def dormir(self):
        self.energia = 100
        return f"{self.nome} dormiu e recuperou energia"
    
    def mover(self):
        self.energia -= 10
        return f"{self.nome} se moveu"

class Mamifero(Animal):  # Herança simples
    def __init__(self, nome, especie, pelos=True):
        super().__init__(nome, especie)  # Chama o construtor da classe pai
        self.pelos = pelos
        self.temperatura_corporal = 37.0
    
    def amamentar(self):
        self.energia -= 20
        return f"{self.nome} está amamentando"

class Cachorro(Mamifero):
    def __init__(self, nome, raca):
        super().__init__(nome, "Canis lupus")
        self.raca = raca
    
    def latir(self):
        self.energia -= 5
        return f"{self.nome} está latindo: Au au!"
    
    def mover(self):  # Sobrescreve o método da classe pai
        resultado = super().mover()  # Chama o método original
        return resultado + " correndo alegremente"

# Usando herança
rex = Cachorro("Rex", "Pastor Alemão")
print(rex.latir())  # Método próprio da classe Cachorro
print(rex.amamentar())  # Método herdado de Mamifero
print(rex.dormir())  # Método herdado de Animal
print(rex.mover())  # Método sobrescrito
```


### Herança Múltipla

Python suporta **herança múltipla**, permitindo que uma classe herde de várias classes pai simultaneamente. Esta funcionalidade oferece grande flexibilidade para combinar comportamentos de diferentes classes, mas requer cuidado para evitar conflitos e ambiguidades. O Python utiliza o algoritmo C3 linearization (Method Resolution Order - MRO) para determinar a ordem de resolução de métodos.

A herança múltipla é útil para implementar padrões como mixins, onde pequenas classes fornecem funcionalidades específicas que podem ser combinadas. É importante compreender o MRO para prever qual implementação de um método será chamada quando há conflitos. O método `mro()` ou o atributo `__mro__` podem ser utilizados para examinar a ordem de resolução.

```python
class Voador:
    def __init__(self):
        self.altitude = 0
    
    def voar(self):
        self.altitude += 100
        return f"Voando a {self.altitude}m de altitude"
    
    def pousar(self):
        self.altitude = 0
        return "Pousou no solo"

class Nadador:
    def __init__(self):
        self.profundidade = 0
    
    def nadar(self):
        self.profundidade += 10
        return f"Nadando a {self.profundidade}m de profundidade"
    
    def emergir(self):
        self.profundidade = 0
        return "Emergiu à superfície"

class Pato(Animal, Voador, Nadador):  # Herança múltipla
    def __init__(self, nome):
        Animal.__init__(self, nome, "Anas platyrhynchos")
        Voador.__init__(self)
        Nadador.__init__(self)
    
    def grasnar(self):
        return f"{self.nome} faz: Quack!"

# Usando herança múltipla
donald = Pato("Donald")
print(donald.grasnar())  # Método próprio
print(donald.voar())     # Método de Voador
print(donald.nadar())    # Método de Nadador
print(donald.dormir())   # Método de Animal

# Examinando o MRO
print(Pato.__mro__)
```


### Polimorfismo

O **polimorfismo** permite que objetos de diferentes classes sejam tratados de forma uniforme através de uma interface comum. Em Python, o polimorfismo é naturalmente suportado através do duck typing: "se anda como um pato e grasna como um pato, então é um pato". Isso significa que o tipo específico do objeto é menos importante que os métodos que ele implementa.

O polimorfismo facilita a escrita de código genérico que pode trabalhar com diferentes tipos de objetos, desde que implementem os métodos necessários. Esta flexibilidade é uma das grandes forças do Python e permite criar sistemas extensíveis onde novos tipos podem ser adicionados sem modificar código existente.

```python
class Forma:
    def calcular_area(self):
        raise NotImplementedError("Método deve ser implementado pela subclasse")
    
    def calcular_perimetro(self):
        raise NotImplementedError("Método deve ser implementado pela subclasse")

class Retangulo(Forma):
    def __init__(self, largura, altura):
        self.largura = largura
        self.altura = altura
    
    def calcular_area(self):
        return self.largura * self.altura
    
    def calcular_perimetro(self):
        return 2 * (self.largura + self.altura)

class Circulo(Forma):
    def __init__(self, raio):
        self.raio = raio
    
    def calcular_area(self):
        return 3.14159 * self.raio ** 2
    
    def calcular_perimetro(self):
        return 2 * 3.14159 * self.raio

# Função polimórfica
def processar_formas(formas):
    for forma in formas:
        print(f"Área: {forma.calcular_area():.2f}")
        print(f"Perímetro: {forma.calcular_perimetro():.2f}")
        print("-" * 30)

# Usando polimorfismo
formas = [
    Retangulo(5, 3),
    Circulo(4),
    Retangulo(2, 8)
]

processar_formas(formas)  # Funciona com qualquer objeto que implemente os métodos
```


## Encapsulamento e Modificadores de Acesso

### Convenções de Visibilidade

O **encapsulamento** é o princípio de ocultar detalhes internos de implementação e expor apenas interfaces controladas para interação externa. Python não possui modificadores de acesso tradicionais (como private ou protected de outras linguagens), mas utiliza convenções de nomenclatura para indicar o nível de visibilidade pretendido dos membros da classe.

Atributos e métodos que começam com um sublinhado (`_`) são considerados **protegidos** por convenção, indicando uso interno à classe e suas subclasses. Aqueles que começam com dois sublinhados (`__`) sofrem name mangling, tornando-se mais difíceis de acessar externamente. Embora tecnicamente ainda sejam acessíveis, esta convenção sinaliza que são detalhes internos que não devem ser utilizados por código externo.

```python
class ContaBancaria:
    def __init__(self, titular, saldo_inicial=0):
        self.titular = titular           # Público
        self._numero_conta = self._gerar_numero()  # Protegido
        self.__saldo = saldo_inicial     # "Privado" (name mangling)
        self._historico = []            # Protegido
    
    def _gerar_numero(self):
        """Método protegido para uso interno"""
        import random
        return random.randint(10000, 99999)
    
    def __validar_valor(self, valor):
        """Método privado para validação"""
        return valor > 0
    
    def depositar(self, valor):
        """Método público"""
        if self.__validar_valor(valor):
            self.__saldo += valor
            self._historico.append(f"Depósito: +{valor}")
            return True
        return False
    
    def sacar(self, valor):
        """Método público"""
        if self.__validar_valor(valor) and self.__saldo >= valor:
            self.__saldo -= valor
            self._historico.append(f"Saque: -{valor}")
            return True
        return False
    
    @property
    def saldo(self):
        """Acesso controlado ao saldo"""
        return self.__saldo
    
    def extrato(self):
        """Método público"""
        return self._historico.copy()

# Usando encapsulamento
conta = ContaBancaria("João Silva", 1000)
print(f"Titular: {conta.titular}")  # Acesso público OK
print(f"Saldo: {conta.saldo}")      # Acesso via property OK

# Tentativas de acesso direto (não recomendadas)
print(f"Número protegido: {conta._numero_conta}")  # Funciona mas não é recomendado
# print(conta.__saldo)  # Geraria AttributeError

# Acesso ao atributo com name mangling (possível mas desencorajado)
print(f"Saldo via name mangling: {conta._ContaBancaria__saldo}")
```


### Validação e Controle de Acesso

O uso de propriedades e métodos permite implementar **validação de dados** e **controle de acesso** refinados. Isso garante que o estado interno dos objetos permaneça consistente e válido, prevenindo bugs e comportamentos inesperados. A validação pode incluir verificação de tipos, rangos de valores, formatação e regras de negócio específicas.

O controle de acesso através de métodos também facilita a implementação de logging, auditoria e outras funcionalidades transversais. Mudanças na implementação interna podem ser realizadas sem afetar o código cliente, desde que a interface pública seja mantida. Esta abordagem promove manutenibilidade e evolução segura do software.

```python
class Produto:
    def __init__(self, nome, preco, categoria):
        self._nome = None
        self._preco = None
        self._categoria = None
        self._desconto = 0
        
        # Usar setters para validação inicial
        self.nome = nome
        self.preco = preco
        self.categoria = categoria
    
    @property
    def nome(self):
        return self._nome
    
    @nome.setter
    def nome(self, valor):
        if not isinstance(valor, str) or len(valor.strip()) == 0:
            raise ValueError("Nome deve ser uma string não vazia")
        self._nome = valor.strip().title()
    
    @property
    def preco(self):
        return self._preco
    
    @preco.setter
    def preco(self, valor):
        if not isinstance(valor, (int, float)) or valor <= 0:
            raise ValueError("Preço deve ser um número positivo")
        self._preco = float(valor)
    
    @property
    def categoria(self):
        return self._categoria
    
    @categoria.setter
    def categoria(self, valor):
        categorias_validas = ["eletrônicos", "roupas", "livros", "casa", "esportes"]
        if valor.lower() not in categorias_validas:
            raise ValueError(f"Categoria deve ser uma de: {categorias_validas}")
        self._categoria = valor.lower()
    
    @property
    def desconto(self):
        return self._desconto
    
    @desconto.setter
    def desconto(self, valor):
        if not isinstance(valor, (int, float)) or not (0 <= valor <= 100):
            raise ValueError("Desconto deve estar entre 0 e 100")
        self._desconto = valor
    
    @property
    def preco_final(self):
        """Propriedade computada somente leitura"""
        return self._preco * (1 - self._desconto / 100)
    
    def aplicar_promocao(self, percentual):
        """Método para aplicar desconto com validação adicional"""
        if percentual < 0:
            raise ValueError("Promoção não pode ser negativa")
        
        desconto_atual = min(self._desconto + percentual, 90)  # Máximo 90% desconto
        self.desconto = desconto_atual
        return f"Desconto aplicado: {self._desconto}%"

# Usando validação e controle
try:
    produto = Produto("  smartphone samsung  ", 899.99, "eletrônicos")
    print(f"Produto: {produto.nome}")  # Nome formatado automaticamente
    print(f"Preço original: R$ {produto.preco:.2f}")
    
    produto.desconto = 15
    print(f"Preço com desconto: R$ {produto.preco_final:.2f}")
    
    produto.aplicar_promocao(10)
    print(f"Preço após promoção: R$ {produto.preco_final:.2f}")
    
    # produto.preco = -100  # Levantaria ValueError
    # produto.categoria = "inválida"  # Levantaria ValueError
    
except ValueError as e:
    print(f"Erro de validação: {e}")
```


## Métodos Especiais e Protocolo de Objetos

### Métodos Dunder (Magic Methods)

Os **métodos especiais** ou **dunder methods** (double underscore) são métodos com nomes que começam e terminam com dois sublinhados. Eles definem como objetos se comportam em situações específicas, como operações aritméticas, comparações, conversões de tipo e representações. Implementar esses métodos permite que objetos customizados se integrem naturalmente com as funcionalidades built-in do Python.

Estes métodos são chamados automaticamente pelo interpretador Python em resposta a operações específicas. Por exemplo, `__add__` é chamado quando o operador `+` é usado, `__len__` quando `len()` é aplicado ao objeto, e `__str__` quando `str()` ou `print()` são utilizados. Dominar esses métodos permite criar classes que se comportam como tipos nativos do Python.

```python
class Vetor2D:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __str__(self):
        """Representação legível para usuários"""
        return f"Vetor({self.x}, {self.y})"
    
    def __repr__(self):
        """Representação técnica para desenvolvedores"""
        return f"Vetor2D({self.x!r}, {self.y!r})"
    
    def __add__(self, outro):
        """Soma de vetores usando operador +"""
        if isinstance(outro, Vetor2D):
            return Vetor2D(self.x + outro.x, self.y + outro.y)
        raise TypeError("Só pode somar com outro Vetor2D")
    
    def __sub__(self, outro):
        """Subtração de vetores usando operador -"""
        if isinstance(outro, Vetor2D):
            return Vetor2D(self.x - outro.x, self.y - outro.y)
        raise TypeError("Só pode subtrair outro Vetor2D")
    
    def __mul__(self, escalar):
        """Multiplicação por escalar usando operador *"""
        if isinstance(escalar, (int, float)):
            return Vetor2D(self.x * escalar, self.y * escalar)
        raise TypeError("Só pode multiplicar por número")
    
    def __eq__(self, outro):
        """Igualdade usando operador =="""
        if isinstance(outro, Vetor2D):
            return self.x == outro.x and self.y == outro.y
        return False
    
    def __abs__(self):
        """Magnitude do vetor usando abs()"""
        return (self.x ** 2 + self.y ** 2) ** 0.5
    
    def __bool__(self):
        """Valor booleano do vetor"""
        return self.x != 0 or self.y != 0

# Usando métodos especiais
v1 = Vetor2D(3, 4)
v2 = Vetor2D(1, 2)

print(v1)  # Usa __str__
print(repr(v2))  # Usa __repr__

v3 = v1 + v2  # Usa __add__
print(f"Soma: {v3}")

v4 = v1 * 2  # Usa __mul__
print(f"Multiplicação: {v4}")

print(f"Igualdade: {v1 == v2}")  # Usa __eq__
print(f"Magnitude de v1: {abs(v1)}")  # Usa __abs__
print(f"v1 é verdadeiro: {bool(v1)}")  # Usa __bool__
```


### Protocolo de Iteração

O **protocolo de iteração** permite que objetos customizados sejam utilizados em loops `for`, compreensões de lista e outras situações que requerem iteração. Para implementar este protocolo, uma classe deve definir os métodos `__iter__` (que retorna um iterador) e `__next__` (que retorna o próximo item da sequência).

Um objeto iterável implementa `__iter__`, enquanto um iterador implementa tanto `__iter__` quanto `__next__`. Frequentemente, uma classe pode ser tanto iterável quanto iterador, retornando `self` em `__iter__`. O protocolo de iteração é fundamental para integração com as estruturas de controle do Python e permite criar objetos que se comportam como sequências ou geradores.

```python
class Fibonacci:
    """Iterador que gera números da sequência de Fibonacci"""
    
    def __init__(self, max_count=10):
        self.max_count = max_count
        self.count = 0
        self.current = 0
        self.next_val = 1
    
    def __iter__(self):
        """Retorna o próprio objeto (é um iterador)"""
        return self
    
    def __next__(self):
        """Retorna o próximo número de Fibonacci"""
        if self.count >= self.max_count:
            raise StopIteration
        
        if self.count == 0:
            self.count += 1
            return 0
        elif self.count == 1:
            self.count += 1
            return 1
        else:
            result = self.current + self.next_val
            self.current = self.next_val
            self.next_val = result
            self.count += 1
            return result

class MinhaLista:
    """Exemplo de classe iterável que não é iterador"""
    
    def __init__(self):
        self._items = []
    
    def adicionar(self, item):
        self._items.append(item)
    
    def __iter__(self):
        """Retorna um novo iterador"""
        return MinhaListaIterator(self._items)
    
    def __len__(self):
        return len(self._items)
    
    def __getitem__(self, index):
        return self._items[index]

class MinhaListaIterator:
    """Iterador separado para MinhaLista"""
    
    def __init__(self, items):
        self._items = items
        self._index = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self._index >= len(self._items):
            raise StopIteration
        item = self._items[self._index]
        self._index += 1
        return item

# Usando protocolo de iteração
fib = Fibonacci(8)
print("Sequência de Fibonacci:")
for numero in fib:
    print(numero, end=" ")
print()

# Usando lista customizada
minha_lista = MinhaLista()
minha_lista.adicionar("Python")
minha_lista.adicionar("é")
minha_lista.adicionar("incrível")

print("\nIterando sobre MinhaLista:")
for item in minha_lista:
    print(item)

# Múltiplas iterações são possíveis porque __iter__ retorna novo iterador
print("\nSegunda iteração:")
for item in minha_lista:
    print(f"-> {item}")
```


### Context Managers (Gerenciadores de Contexto)

**Context managers** implementam o protocolo de contexto através dos métodos `__enter__` e `__exit__`, permitindo uso com a declaração `with`. Este padrão garante que recursos sejam adequadamente inicializados e liberados, mesmo quando exceções ocorrem. É amplamente utilizado para gerenciamento de arquivos, conexões de banco de dados e outros recursos que precisam de limpeza.

O método `__enter__` é chamado no início do bloco `with` e pode retornar um valor que será atribuído à variável após `as`. O método `__exit__` é sempre chamado ao final do bloco, mesmo se uma exceção ocorrer, recebendo informações sobre qualquer exceção que tenha sido levantada. Implementar este protocolo torna objetos mais robustos e seguros para uso.

```python
class GerenciadorArquivo:
    """Context manager customizado para arquivos"""
    
    def __init__(self, nome_arquivo, modo='r'):
        self.nome_arquivo = nome_arquivo
        self.modo = modo
        self.arquivo = None
    
    def __enter__(self):
        """Chamado no início do bloco with"""
        print(f"Abrindo arquivo: {self.nome_arquivo}")
        self.arquivo = open(self.nome_arquivo, self.modo)
        return self.arquivo
    
    def __exit__(self, exc_type, exc_value, traceback):
        """Chamado no final do bloco with (mesmo com exceção)"""
        print(f"Fechando arquivo: {self.nome_arquivo}")
        if self.arquivo:
            self.arquivo.close()
        
        # Se retornar True, suprime a exceção
        if exc_type is not None:
            print(f"Exceção capturada: {exc_type.__name__}: {exc_value}")
        
        return False  # Não suprime exceções

class Cronometro:
    """Context manager para medir tempo de execução"""
    
    def __init__(self, nome="Operação"):
        self.nome = nome
        self.tempo_inicio = None
    
    def __enter__(self):
        import time
        self.tempo_inicio = time.time()
        print(f"Iniciando: {self.nome}")
        return self
    
    def __exit__(self, exc_type, exc_value, traceback):
        import time
        tempo_total = time.time() - self.tempo_inicio
        print(f"{self.nome} completada em {tempo_total:.4f} segundos")
        return False

class ConexaoDB:
    """Simulador de conexão com banco de dados"""
    
    def __init__(self, host, banco):
        self.host = host
        self.banco = banco
        self.conectado = False
    
    def __enter__(self):
        print(f"Conectando a {self.host}/{self.banco}")
        self.conectado = True
        return self
    
    def __exit__(self, exc_type, exc_value, traceback):
        if self.conectado:
            print(f"Desconectando de {self.host}/{self.banco}")
            self.conectado = False
        return False
    
    def executar_query(self, sql):
        if not self.conectado:
            raise RuntimeError("Não conectado ao banco")
        return f"Executando: {sql}"

# Usando context managers
# Exemplo 1: Gerenciador de arquivo
try:
    with GerenciadorArquivo("exemplo.txt", "w") as arquivo:
        arquivo.write("Olá, mundo!")
        # Arquivo é automaticamente fechado
except FileNotFoundError as e:
    print(f"Arquivo não encontrado: {e}")

# Exemplo 2: Cronômetro
with Cronometro("Processamento de dados"):
    import time
    time.sleep(1)  # Simula processamento
    total = sum(range(1000000))

# Exemplo 3: Conexão de banco
with ConexaoDB("localhost", "meu_banco") as db:
    resultado = db.executar_query("SELECT * FROM usuarios")
    print(resultado)
    # Conexão é automaticamente fechada
```


## Conceitos Avançados

### Metaclasses

**Metaclasses** são "classes de classes" - elas definem como as classes são criadas. Assim como uma classe é um template para criar instâncias, uma metaclasse é um template para criar classes. Em Python, o tipo padrão de metaclasse é `type`, que é usada implicitamente para criar todas as classes. Compreender metaclasses permite controle profundo sobre a criação e comportamento de classes.

Metaclasses são um conceito avançado raramente necessário no dia a dia, mas extremamente poderoso para frameworks e bibliotecas. Elas permitem interceptar a criação de classes, modificar atributos, adicionar métodos dinamicamente e implementar padrões como Singleton automaticamente. O uso de metaclasses deve ser considerado apenas quando decoradores ou outras técnicas não são suficientes.

```python
class SingletonMeta(type):
    """Metaclasse que implementa o padrão Singleton"""
    
    _instances = {}
    
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
            print(f"Criando nova instância de {cls.__name__}")
        else:
            print(f"Retornando instância existente de {cls.__name__}")
        return cls._instances[cls]

class LoggerMeta(type):
    """Metaclasse que adiciona logging a todos os métodos"""
    
    def __new__(mcs, name, bases, attrs):
        for attr_name, attr_value in attrs.items():
            if callable(attr_value) and not attr_name.startswith('_'):
                attrs[attr_name] = mcs.add_logging(attr_value, attr_name)
        
        return super().__new__(mcs, name, bases, attrs)
    
    @staticmethod
    def add_logging(func, name):
        def wrapper(*args, **kwargs):
            print(f"Chamando método: {name}")
            result = func(*args, **kwargs)
            print(f"Método {name} finalizado")
            return result
        return wrapper

# Usando metaclasses
class DatabaseConnection(metaclass=SingletonMeta):
    def __init__(self, host="localhost"):
        self.host = host
        self.conectado = False
    
    def conectar(self):
        self.conectado = True
        return f"Conectado a {self.host}"

class Calculadora(metaclass=LoggerMeta):
    def somar(self, a, b):
        return a + b
    
    def multiplicar(self, a, b):
        return a * b

# Testando Singleton
db1 = DatabaseConnection("servidor1")
db2 = DatabaseConnection("servidor2")  # Ignora o novo host
print(f"db1 é db2: {db1 is db2}")  # True

# Testando logging automático
calc = Calculadora()
resultado1 = calc.somar(5, 3)
resultado2 = calc.multiplicar(4, 6)
```


### Descritores

**Descritores** são objetos que definem como acessar atributos de outros objetos através dos métodos `__get__`, `__set__` e `__delete__`. Eles são o mecanismo subjacente que implementa propriedades, métodos e funções em Python. Compreender descritores oferece controle granular sobre acesso a atributos e permite criar abstrações poderosas.

Descritores podem ser de dados (implementam `__set__` ou `__delete__`) ou não-dados (apenas `__get__`). Python consulta descritores de dados antes de verificar o dicionário da instância, enquanto descritores não-dados são consultados apenas se o atributo não for encontrado no dicionário da instância. Esta distinção afeta a precedência de resolução de atributos.

```python
class ValidadorTipo:
    """Descritor para validação de tipo"""
    
    def __init__(self, tipo_esperado, nome=None):
        self.tipo_esperado = tipo_esperado
        self.nome = nome
    
    def __set_name__(self, owner, name):
        """Chamado automaticamente quando o descritor é atribuído a uma classe"""
        self.nome = name
    
    def __get__(self, instance, owner):
        if instance is None:
            return self
        return instance.__dict__.get(self.nome)
    
    def __set__(self, instance, value):
        if not isinstance(value, self.tipo_esperado):
            raise TypeError(f"{self.nome} deve ser do tipo {self.tipo_esperado.__name__}")
        instance.__dict__[self.nome] = value
    
    def __delete__(self, instance):
        if self.nome in instance.__dict__:
            del instance.__dict__[self.nome]

class ValidadorRange:
    """Descritor para validação de intervalo numérico"""
    
    def __init__(self, minimo, maximo):
        self.minimo = minimo
        self.maximo = maximo
    
    def __set_name__(self, owner, name):
        self.nome = name
    
    def __get__(self, instance, owner):
        if instance is None:
            return self
        return instance.__dict__.get(self.nome)
    
    def __set__(self, instance, value):
        if not isinstance(value, (int, float)):
            raise TypeError(f"{self.nome} deve ser numérico")
        if not (self.minimo <= value <= self.maximo):
            raise ValueError(f"{self.nome} deve estar entre {self.minimo} e {self.maximo}")
        instance.__dict__[self.nome] = value

class Historico:
    """Descritor que mantém histórico de mudanças"""
    
    def __set_name__(self, owner, name):
        self.nome = name
        self.private_name = f"_{name}"
        self.history_name = f"_{name}_history"
    
    def __get__(self, instance, owner):
        if instance is None:
            return self
        return getattr(instance, self.private_name, None)
    
    def __set__(self, instance, value):
        # Inicializa histórico se necessário
        if not hasattr(instance, self.history_name):
            setattr(instance, self.history_name, [])
        
        # Adiciona valor anterior ao histórico
        valor_anterior = getattr(instance, self.private_name, None)
        if valor_anterior is not None:
            getattr(instance, self.history_name).append(valor_anterior)
        
        # Define novo valor
        setattr(instance, self.private_name, value)
    
    def get_history(self, instance):
        return getattr(instance, self.history_name, [])

# Usando descritores
class Pessoa:
    nome = ValidadorTipo(str)
    idade = ValidadorRange(0, 150)
    salario = Historico()
    
    def __init__(self, nome, idade, salario):
        self.nome = nome
        self.idade = idade
        self.salario = salario
    
    def obter_historico_salario(self):
        return self.salario.get_history(self)

# Testando descritores
try:
    pessoa = Pessoa("João", 30, 5000)
    print(f"Nome: {pessoa.nome}, Idade: {pessoa.idade}, Salário: {pessoa.salario}")
    
    # Alterando salário para testar histórico
    pessoa.salario = 5500
    pessoa.salario = 6000
    
    print(f"Histórico salarial: {pessoa.obter_historico_salario()}")
    
    # Teste de validação
    # pessoa.nome = 123  # Levantaria TypeError
    # pessoa.idade = -5  # Levantaria ValueError
    
except (TypeError, ValueError) as e:
    print(f"Erro de validação: {e}")
```


### Slots

O mecanismo `__slots__` permite definir explicitamente quais atributos uma classe pode ter, oferecendo otimização de memória e prevenção de criação dinâmica de atributos. Quando `__slots__` é definido, Python não cria um dicionário `__dict__` para cada instância, resultando em uso mais eficiente de memória, especialmente para classes com muitas instâncias.

Slots impõem restrições: apenas os atributos listados podem existir, herança múltipla com classes que têm slots pode ser problemática, e funcionalidades como `__dict__` e weak references podem não estar disponíveis. Slots são úteis para classes que representam estruturas de dados simples onde performance e uso de memória são críticos.

```python
import sys
from collections import namedtuple

class PontoNormal:
    """Classe tradicional sem slots"""
    
    def __init__(self, x, y, z):
        self.x = x
        self.y = y
        self.z = z
    
    def distancia_origem(self):
        return (self.x ** 2 + self.y ** 2 + self.z ** 2) ** 0.5

class PontoComSlots:
    """Classe otimizada com slots"""
    
    __slots__ = ['x', 'y', 'z']
    
    def __init__(self, x, y, z):
        self.x = x
        self.y = y
        self.z = z
    
    def distancia_origem(self):
        return (self.x ** 2 + self.y ** 2 + self.z ** 2) ** 0.5

class SlotsComPropriedades:
    """Slots com propriedades e validação"""
    
    __slots__ = ['_x', '_y', '_nome']
    
    def __init__(self, x, y, nome):
        self._x = x
        self._y = y
        self._nome = nome
    
    @property
    def x(self):
        return self._x
    
    @x.setter
    def x(self, value):
        if not isinstance(value, (int, float)):
            raise TypeError("x deve ser numérico")
        self._x = value
    
    @property
    def y(self):
        return self._y
    
    @y.setter
    def y(self, value):
        if not isinstance(value, (int, float)):
            raise TypeError("y deve ser numérico")
        self._y = value
    
    @property
    def nome(self):
        return self._nome

# Comparando uso de memória
def comparar_memoria():
    # Criando instâncias
    ponto_normal = PontoNormal(1, 2, 3)
    ponto_slots = PontoComSlots(1, 2, 3)
    
    # Medindo uso de memória
    tamanho_normal = sys.getsizeof(ponto_normal) + sys.getsizeof(ponto_normal.__dict__)
    tamanho_slots = sys.getsizeof(ponto_slots)
    
    print(f"Ponto normal: {tamanho_normal} bytes")
    print(f"Ponto com slots: {tamanho_slots} bytes")
    print(f"Economia: {tamanho_normal - tamanho_slots} bytes ({((tamanho_normal - tamanho_slots) / tamanho_normal * 100):.1f}%)")

# Testando funcionalidades
comparar_memoria()

# Testando restrições de slots
ponto_slots = PontoComSlots(1, 2, 3)
print(f"Distância: {ponto_slots.distancia_origem():.2f}")

# Tentar adicionar atributo dinâmico falhará
try:
    ponto_slots.novo_atributo = "teste"  # Levantará AttributeError
except AttributeError as e:
    print(f"Erro esperado com slots: {e}")

# Testando slots com propriedades
ponto_prop = SlotsComPropriedades(5, 10, "Ponto A")
print(f"Ponto {ponto_prop.nome}: ({ponto_prop.x}, {ponto_prop.y})")

try:
    ponto_prop.x = "inválido"  # Levantará TypeError
except TypeError as e:
    print(f"Validação funcionou: {e}")

# Comparando com namedtuple
PontoNamedTuple = namedtuple('PontoNamedTuple', ['x', 'y', 'z'])
ponto_nt = PontoNamedTuple(1, 2, 3)

print(f"\nComparação de tamanhos:")
print(f"Classe normal: {sys.getsizeof(PontoNormal(1, 2, 3)) + sys.getsizeof(PontoNormal(1, 2, 3).__dict__)} bytes")
print(f"Classe com slots: {sys.getsizeof(PontoComSlots(1, 2, 3))} bytes")
print(f"NamedTuple: {sys.getsizeof(ponto_nt)} bytes")
```


## Conclusão

O domínio de objetos em Python representa um marco fundamental na jornada de qualquer desenvolvedor que busca criar código robusto, maintível e escalável. Este material abordou desde conceitos básicos como classes e instâncias até tópicos avançados como metaclasses, descritores e slots, fornecendo uma base sólida para aplicação prática da programação orientada a objetos.

A programação orientada a objetos em Python oferece ferramentas poderosas para modelar problemas do mundo real de forma natural e intuitiva. Através do encapsulamento, desenvolvemos código mais seguro e organizados; pela herança, reutilizamos funcionalidades e estabelecemos hierarquias lógicas; com polimorfismo, criamos interfaces flexíveis que facilitam extensibilidade e manutenção. Estes princípios, combinados com as características únicas do Python como duck typing e introspecção dinâmica, permitem desenvolvimento ágil sem sacrificar qualidade ou performance.

Os conceitos avançados apresentados, embora não necessários para programação cotidiana, abrem possibilidades para criação de frameworks, bibliotecas e soluções elegantes para problemas complexos. Metaclasses permitem controle profundo sobre criação de classes, descritores oferecem mecanismos sofisticados de controle de acesso a atributos, e slots proporcionam otimizações importantes quando performance é crítica. A compreensão destes mecanismos internos eleva significativamente a capacidade de um desenvolvedor para criar soluções pythônicas e eficientes.

A jornada de aprendizado em programação orientada a objetos é contínua e recompensadora. Os conceitos aqui apresentados devem ser praticados através de projetos reais, experimentação constante e estudo de código de bibliotecas populares. Python oferece um ambiente excepcional para explorar estes conceitos devido à sua sintaxe clara, filosofia pragmática e comunidade ativa que constantemente desenvolve exemplos e padrões exemplares de código orientado a objetos.

