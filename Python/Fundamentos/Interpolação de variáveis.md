

# Interpolação de Variáveis em Python

A interpolação de variáveis em Python é uma técnica fundamental que permite incorporar valores de variáveis diretamente em strings, facilitando a criação de textos dinâmicos e a formatação de saídas. Este conceito é essencial para qualquer desenvolvedor Python, desde iniciantes até profissionais experientes, pois oferece múltiplas abordagens com diferentes níveis de complexidade e funcionalidade.

A evolução dos métodos de interpolação em Python reflete a constante busca por maior legibilidade, performance e flexibilidade no desenvolvimento de aplicações. Compreender essas técnicas não apenas melhora a qualidade do código, mas também permite escolher a abordagem mais adequada para cada situação específica.

- [[#Conceitos Fundamentais da Interpolação|Conceitos Fundamentais da Interpolação]]
	- [[#Conceitos Fundamentais da Interpolação#Definição e Importância|Definição e Importância]]
	- [[#Conceitos Fundamentais da Interpolação#Evolução Histórica dos Métodos|Evolução Histórica dos Métodos]]
- [[#Método de Formatação com Operador %|Método de Formatação com Operador %]]
	- [[#Método de Formatação com Operador %#Sintaxe Básica e Especificadores|Sintaxe Básica e Especificadores]]
	- [[#Método de Formatação com Operador %#Formatação Avançada e Modificadores|Formatação Avançada e Modificadores]]
	- [[#Método de Formatação com Operador %#Limitações e Casos Problemáticos|Limitações e Casos Problemáticos]]
- [[#Método .format() e Formatação Moderna|Método .format() e Formatação Moderna]]
	- [[#Método .format() e Formatação Moderna#Introdução ao Método .format()|Introdução ao Método .format()]]
	- [[#Método .format() e Formatação Moderna#Especificadores de Formato Avançados|Especificadores de Formato Avançados]]
	- [[#Método .format() e Formatação Moderna#Formatação com Objetos e Atributos|Formatação com Objetos e Atributos]]
- [[#F-Strings: A Revolução na Interpolação|F-Strings: A Revolução na Interpolação]]
	- [[#F-Strings: A Revolução na Interpolação#Introdução às Formatted String Literals|Introdução às Formatted String Literals]]
	- [[#F-Strings: A Revolução na Interpolação#Expressões Complexas e Chamadas de Função|Expressões Complexas e Chamadas de Função]]
	- [[#F-Strings: A Revolução na Interpolação#Especificadores de Formato em F-Strings|Especificadores de Formato em F-Strings]]
- [[#Template Strings para Casos Especiais|Template Strings para Casos Especiais]]
	- [[#Template Strings para Casos Especiais#Introdução ao Módulo string.Template|Introdução ao Módulo string.Template]]
	- [[#Template Strings para Casos Especiais#Casos de Uso e Vantagens de Segurança|Casos de Uso e Vantagens de Segurança]]
- [[#Comparação de Performance e Melhores Práticas|Comparação de Performance e Melhores Práticas]]
	- [[#Comparação de Performance e Melhores Práticas#Análise de Performance entre Métodos|Análise de Performance entre Métodos]]
	- [[#Comparação de Performance e Melhores Práticas#Diretrizes para Escolha do Método Adequado|Diretrizes para Escolha do Método Adequado]]
	- [[#Comparação de Performance e Melhores Práticas#Padrões de Código e Legibilidade|Padrões de Código e Legibilidade]]
- [[#Casos de Uso Avançados e Aplicações Práticas|Casos de Uso Avançados e Aplicações Práticas]]
	- [[#Casos de Uso Avançados e Aplicações Práticas#Formatação de Logs e Debugging|Formatação de Logs e Debugging]]
	- [[#Casos de Uso Avançados e Aplicações Práticas#Geração de Relatórios e Templates|Geração de Relatórios e Templates]]
	- [[#Casos de Uso Avançados e Aplicações Práticas#Internacionalização e Localização|Internacionalização e Localização]]
- [[#Técnicas Avançadas e Otimizações|Técnicas Avançadas e Otimizações]]
	- [[#Técnicas Avançadas e Otimizações#Formatação Condicional e Dinâmica|Formatação Condicional e Dinâmica]]
	- [[#Técnicas Avançadas e Otimizações#Formatação de Estruturas de Dados Complexas|Formatação de Estruturas de Dados Complexas]]
- [[#Conclusão|Conclusão]]

## Conceitos Fundamentais da Interpolação

### Definição e Importância

A interpolação de variáveis, também conhecida como formatação de strings, é o processo de inserir valores de variáveis dentro de strings de texto. Em Python, esta funcionalidade é crucial para criar mensagens dinâmicas, relatórios, logs e interfaces de usuário. O conceito surgiu da necessidade de combinar texto estático com dados variáveis de forma eficiente e legível.

A importância da interpolação vai além da simples concatenação de strings. Ela oferece controle preciso sobre a formatação, permite a reutilização de templates e melhora significativamente a manutenibilidade do código. Quando bem aplicada, a interpolação torna o código mais expressivo e facilita a internacionalização de aplicações.

### Evolução Histórica dos Métodos

Python evoluiu consideravelmente em relação aos métodos de interpolação ao longo de suas versões. Inicialmente, o método principal era baseado no operador de módulo (%), inspirado na linguagem C. Com o tempo, surgiram métodos mais sofisticados como o método `.format()` no Python 2.6 e as f-strings (formatted string literals) no Python 3.6, cada um oferecendo vantagens específicas em termos de performance e legibilidade.

Esta evolução reflete a filosofia Python de priorizar a legibilidade e a facilidade de uso. Cada novo método introduzido não apenas oferecia melhor performance, mas também sintaxe mais intuitiva e recursos mais avançados para formatação complexa.

## Método de Formatação com Operador %

### Sintaxe Básica e Especificadores

O método mais antigo de interpolação em Python utiliza o operador de módulo (%) seguido de especificadores de formato. A sintaxe básica segue o padrão `"string com %especificador" % valor`. Os especificadores mais comuns incluem `%s` para strings, `%d` para inteiros, `%f` para números de ponto flutuante e `%x` para hexadecimais.

```python
nome = "João"
idade = 25
altura = 1.75

# Formatação básica
mensagem = "Olá, %s! Você tem %d anos e %.2f metros de altura." % (nome, idade, altura)
print(mensagem)  # Olá, João! Você tem 25 anos e 1.75 metros de altura.

# Formatação com diferentes tipos
numero = 42
hexadecimal = "O número %d em hexadecimal é %x" % (numero, numero)
print(hexadecimal)  # O número 42 em hexadecimal é 2a
```


### Formatação Avançada e Modificadores

O operador % oferece diversos modificadores para controle preciso da formatação. É possível especificar largura mínima, alinhamento, preenchimento com zeros e precisão decimal. Os modificadores são colocados entre o % e o especificador de tipo, seguindo a sintaxe `%[flags][width][.precision]type`.

```python
# Controle de largura e alinhamento
valor = 123.456
print("Valor: %10.2f" % valor)      # "Valor:     123.46" (alinhado à direita)
print("Valor: %-10.2f" % valor)     # "Valor: 123.46    " (alinhado à esquerda)
print("Valor: %010.2f" % valor)     # "Valor: 0000123.46" (preenchido com zeros)

# Formatação de percentuais
percentual = 0.1234
print("Taxa: %.2%" % (percentual * 100))  # Taxa: 12.34%
```


### Limitações e Casos Problemáticos

Embora funcional, o método % apresenta várias limitações significativas. A principal dificuldade surge ao trabalhar com múltiplas variáveis, exigindo que sejam passadas como tupla na ordem exata. Além disso, não oferece suporte nativo para formatação por nome de variável, tornando o código menos legível em casos complexos. A mistura de tipos pode causar erros difíceis de debugar, especialmente quando os especificadores não correspondem aos tipos das variáveis fornecidas.

## Método .format() e Formatação Moderna

### Introdução ao Método .format()

O método `.format()` foi introduzido no Python 2.6 como uma alternativa mais flexível e poderosa ao operador %. Este método permite formatação por posição, por nome e oferece recursos avançados de formatação que não estavam disponíveis no método anterior. A sintaxe utiliza chaves `{}` como placeholders dentro da string, que são substituídos pelos argumentos passados ao método.

```python
# Formatação por posição
nome = "Maria"
idade = 30
mensagem = "Olá, {}! Você tem {} anos.".format(nome, idade)
print(mensagem)  # Olá, Maria! Você tem 30 anos.

# Formatação por índice
mensagem = "Olá, {0}! Você tem {1} anos. {0} é um belo nome.".format(nome, idade)
print(mensagem)  # Olá, Maria! Você tem 30 anos. Maria é um belo nome.

# Formatação por nome
mensagem = "Olá, {nome}! Você tem {idade} anos.".format(nome=nome, idade=idade)
print(mensagem)  # Olá, Maria! Você tem 30 anos.
```


### Especificadores de Formato Avançados

O método `.format()` oferece um sistema robusto de especificadores que permite controle detalhado sobre a apresentação dos dados. A sintaxe completa é `{[field_name][!conversion][:format_spec]}`, onde cada componente oferece diferentes níveis de customização.

```python
import datetime

# Formatação numérica avançada
numero = 1234567.89
print("Número: {:,.2f}".format(numero))           # Número: 1,234,567.89
print("Científica: {:e}".format(numero))          # Científica: 1.234568e+06
print("Percentual: {:.2%}".format(0.1234))        # Percentual: 12.34%

# Formatação de datas
agora = datetime.datetime.now()
print("Data: {:%d/%m/%Y %H:%M}".format(agora))    # Data: 02/10/2025 08:00

# Alinhamento e preenchimento
texto = "Python"
print("'{:>20}'".format(texto))    # '              Python'
print("'{:<20}'".format(texto))    # 'Python              '
print("'{:^20}'".format(texto))    # '       Python       '
print("'{:*^20}'".format(texto))   # '*******Python*******'
```


### Formatação com Objetos e Atributos

Uma das funcionalidades mais poderosas do método `.format()` é a capacidade de acessar atributos de objetos e elementos de estruturas de dados diretamente na string de formatação. Isto permite criar templates complexos sem a necessidade de extrair cada valor individualmente.

```python
# Formatação com dicionários
pessoa = {"nome": "Carlos", "idade": 28, "profissao": "desenvolvedor"}
mensagem = "Nome: {nome}, Idade: {idade}, Profissão: {profissao}".format(**pessoa)
print(mensagem)  # Nome: Carlos, Idade: 28, Profissão: desenvolvedor

# Formatação com listas
dados = ["Ana", 25, "designer"]
mensagem = "Nome: {0[0]}, Idade: {0[1]}, Profissão: {0[2]}".format(dados)
print(mensagem)  # Nome: Ana, Idade: 25, Profissão: designer

# Formatação com atributos de objetos
class Pessoa:
    def __init__(self, nome, idade):
        self.nome = nome
        self.idade = idade

p = Pessoa("Pedro", 35)
mensagem = "Nome: {.nome}, Idade: {.idade}".format(p, p)
print(mensagem)  # Nome: Pedro, Idade: 35
```


## F-Strings: A Revolução na Interpolação

### Introdução às Formatted String Literals

As f-strings, introduzidas no Python 3.6, representam a evolução mais significativa na formatação de strings em Python. Elas combinam a simplicidade de uso com performance superior e legibilidade excepcional. A sintaxe utiliza o prefixo `f` antes da string e permite que expressões Python sejam incorporadas diretamente entre chaves, sendo avaliadas em tempo de execução.

```python
nome = "Alice"
idade = 32
salario = 5500.50

# F-string básica
mensagem = f"Olá, {nome}! Você tem {idade} anos."
print(mensagem)  # Olá, Alice! Você tem 32 anos.

# F-string com expressões
print(f"Salário anual: R$ {salario * 12:,.2f}")    # Salário anual: R$ 66,006.00
print(f"Em 5 anos, {nome} terá {idade + 5} anos")  # Em 5 anos, Alice terá 37 anos

# F-string multiline
relatorio = f"""
Relatório do Funcionário:
Nome: {nome}
Idade: {idade}
Salário Mensal: R$ {salario:,.2f}
Salário Anual: R$ {salario * 12:,.2f}
"""
print(relatorio)
```


### Expressões Complexas e Chamadas de Função

Uma das características mais poderosas das f-strings é a capacidade de incluir expressões Python arbitrárias, incluindo chamadas de função, operações matemáticas complexas e acesso a métodos de objetos. Esta funcionalidade elimina a necessidade de variáveis temporárias em muitos casos.

```python
import math

# Expressões matemáticas
x, y = 3, 4
print(f"A hipotenusa é {math.sqrt(x**2 + y**2):.2f}")  # A hipotenusa é 5.00

# Chamadas de método
texto = "python programming"
print(f"Capitalizado: {texto.title()}")               # Capitalizado: Python Programming
print(f"Palavras: {len(texto.split())}")              # Palavras: 2

# Expressões condicionais
nota = 8.5
resultado = f"Status: {'Aprovado' if nota >= 7 else 'Reprovado'}"
print(resultado)  # Status: Aprovado

# Formatação de estruturas de dados
numeros = [1, 2, 3, 4, 5]
print(f"Soma: {sum(numeros)}, Média: {sum(numeros)/len(numeros):.2f}")
# Soma: 15, Média: 3.00
```


### Especificadores de Formato em F-Strings

As f-strings mantêm compatibilidade com os especificadores de formato do método `.format()`, permitindo controle preciso sobre a apresentação dos dados. A sintaxe combina a expressão Python com os especificadores usando dois pontos.

```python
from datetime import datetime

# Formatação numérica
pi = 3.14159265359
print(f"Pi: {pi:.3f}")              # Pi: 3.142
print(f"Pi científico: {pi:e}")     # Pi científico: 3.141593e+00

# Formatação de data e hora
agora = datetime.now()
print(f"Agora: {agora:%d/%m/%Y às %H:%M:%S}")  # Agora: 02/10/2025 às 08:00:00

# Alinhamento em f-strings
nome = "Python"
largura = 15
print(f"'{nome:>{largura}}'")       # '         Python'
print(f"'{nome:^{largura}}'")       # '    Python     '
print(f"'{nome:*^{largura}}'")      # '****Python*****'

# Formatação condicional
valor = 1500
moeda = "USD" if valor > 1000 else "BRL"
print(f"Valor: {valor:,.2f} {moeda}")  # Valor: 1,500.00 USD
```


## Template Strings para Casos Especiais

### Introdução ao Módulo string.Template

O módulo `string.Template` oferece uma abordagem alternativa para interpolação, especialmente útil quando se trabalha com templates criados por usuários ou quando é necessário maior segurança na formatação. Este método utiliza o símbolo `$` para marcar variáveis e oferece proteção contra execução de código malicioso, uma vez que não permite expressões Python arbitrárias.

```python
from string import Template

# Template básico
template = Template("Olá, $nome! Você tem $idade anos.")
resultado = template.substitute(nome="Roberto", idade=40)
print(resultado)  # Olá, Roberto! Você tem 40 anos.

# Template com dicionário
dados = {"produto": "Notebook", "preco": 2500.00, "desconto": 10}
template = Template("Produto: $produto, Preço: R$ $preco, Desconto: $desconto%")
resultado = template.substitute(dados)
print(resultado)  # Produto: Notebook, Preço: R$ 2500.0, Desconto: 10%

# Template seguro com safe_substitute
template = Template("Nome: $nome, Cargo: $cargo, Salário: $salario")
dados_incompletos = {"nome": "João", "cargo": "Analista"}
resultado = template.safe_substitute(dados_incompletos)
print(resultado)  # Nome: João, Cargo: Analista, Salário: $salario
```


### Casos de Uso e Vantagens de Segurança

O Template oferece vantagens significativas em cenários onde a segurança é prioritária. Diferentemente das f-strings e do método `.format()`, os Templates não executam código Python, tornando-os ideais para processar entrada de usuários não confiáveis. Esta característica é particularmente importante em aplicações web, sistemas de configuração e ferramentas de geração de relatórios.

```python
from string import Template

# Exemplo de uso seguro em aplicação web
def gerar_email_template(nome_usuario, acao):
    template = Template("""
    Olá $nome,
    
    Sua ação '$acao' foi processada com sucesso.
    
    Atenciosamente,
    Equipe de Suporte
    """)
    
    # Mesmo que nome_usuario contenha código malicioso, não será executado
    return template.safe_substitute(nome=nome_usuario, acao=acao)

# Simulação de entrada potencialmente perigosa
entrada_usuario = "${os.system('rm -rf /')}"  # Tentativa de código malicioso
email = gerar_email_template(entrada_usuario, "atualização de perfil")
print(email)  # O código malicioso é tratado como texto literal
```


## Comparação de Performance e Melhores Práticas

### Análise de Performance entre Métodos

A performance dos diferentes métodos de interpolação varia significativamente, sendo as f-strings geralmente as mais rápidas, seguidas pelo método `.format()` e depois pelo operador %. Esta diferença torna-se mais pronunciada com o aumento da complexidade das operações de formatação e do volume de dados processados.

```python
import timeit

# Configuração para teste de performance
nome = "Teste"
idade = 25
valor = 1234.56

# Teste com operador %
tempo_percent = timeit.timeit(
    lambda: "Nome: %s, Idade: %d, Valor: %.2f" % (nome, idade, valor),
    number=100000
)

# Teste com .format()
tempo_format = timeit.timeit(
    lambda: "Nome: {}, Idade: {}, Valor: {:.2f}".format(nome, idade, valor),
    number=100000
)

# Teste com f-string
tempo_fstring = timeit.timeit(
    lambda: f"Nome: {nome}, Idade: {idade}, Valor: {valor:.2f}",
    number=100000
)

print(f"Operador %: {tempo_percent:.4f}s")
print(f"Método .format(): {tempo_format:.4f}s")  
print(f"F-string: {tempo_fstring:.4f}s")
```

As f-strings demonstram superioridade em performance porque são avaliadas em tempo de compilação quando possível, resultando em bytecode mais eficiente. O método `.format()` oferece boa performance com flexibilidade superior, enquanto o operador % apresenta a menor performance devido ao overhead de parsing dos especificadores.

### Diretrizes para Escolha do Método Adequado

A escolha do método de interpolação deve considerar diversos fatores: versão do Python, requisitos de performance, necessidades de segurança e complexidade da formatação. Para código novo em Python 3.6+, f-strings são geralmente a melhor escolha devido à combinação de performance, legibilidade e funcionalidade. O método `.format()` permanece valioso para templates complexos e quando compatibilidade com versões antigas é necessária.

Em aplicações que processam entrada de usuários não confiáveis, Template strings oferecem segurança superior. Para código legado ou quando trabalhando com bases de código antigas, o operador % pode ser mantido, mas deve-se considerar migração gradual para métodos mais modernos.

### Padrões de Código e Legibilidade

A legibilidade é um aspecto fundamental na escolha do método de interpolação. F-strings promovem código mais limpo e expressivo, especialmente quando combinadas com expressões simples. Para casos complexos com múltiplas condicionais ou cálculos, pode ser preferível extrair a lógica para variáveis intermediárias antes da formatação.

```python
# Exemplo de código legível com f-strings
def formatar_relatorio_vendas(vendedor, vendas_mes, meta_mes):
    percentual_meta = (vendas_mes / meta_mes) * 100
    status = "Superou" if vendas_mes > meta_mes else "Não atingiu"
    
    return f"""
    Relatório de Vendas - {vendedor}
    {'='*40}
    Vendas do mês: R$ {vendas_mes:,.2f}
    Meta do mês: R$ {meta_mes:,.2f}
    Percentual da meta: {percentual_meta:.1f}%
    Status: {status} a meta
    """

# Uso do template
relatorio = formatar_relatorio_vendas("Ana Silva", 15000.00, 12000.00)
print(relatorio)
```


## Casos de Uso Avançados e Aplicações Práticas

### Formatação de Logs e Debugging

A interpolação de variáveis é fundamental para sistemas de logging eficazes. A capacidade de incluir informações contextuais em mensagens de log facilita significativamente o debugging e monitoramento de aplicações. F-strings são particularmente úteis neste contexto devido à sua simplicidade e performance.

```python
import logging
import datetime

# Configuração de logging com formatação avançada
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s'
)

def processar_pedido(pedido_id, usuario_id, valor_total):
    inicio = datetime.datetime.now()
    
    logging.info(f"Iniciando processamento do pedido {pedido_id} para usuário {usuario_id}")
    
    # Simulação de processamento
    import time
    time.sleep(0.1)
    
    fim = datetime.datetime.now()
    duracao = (fim - inicio).total_seconds()
    
    logging.info(f"Pedido {pedido_id} processado com sucesso em {duracao:.3f}s - Valor: R$ {valor_total:,.2f}")
    
    return {"status": "sucesso", "duracao": duracao}

# Exemplo de uso
resultado = processar_pedido("PED-001", "USR-123", 299.90)
```


### Geração de Relatórios e Templates

A interpolação é essencial para geração automática de relatórios, especialmente quando os dados provêm de fontes dinâmicas como bancos de dados ou APIs. A combinação de diferentes métodos permite criar sistemas flexíveis de templating.

```python
def gerar_relatorio_financeiro(dados_empresa, periodo):
    template = f"""
    RELATÓRIO FINANCEIRO - {dados_empresa['nome'].upper()}
    {'='*60}
    
    Período: {periodo['inicio']:%d/%m/%Y} a {periodo['fim']:%d/%m/%Y}
    
    RECEITAS:
    --------
    Vendas de Produtos: R$ {dados_empresa['receitas']['produtos']:>12,.2f}
    Prestação de Serviços: R$ {dados_empresa['receitas']['servicos']:>8,.2f}
    Outras Receitas: R$ {dados_empresa['receitas']['outras']:>15,.2f}
    {'-'*50}
    Total de Receitas: R$ {sum(dados_empresa['receitas'].values()):>13,.2f}
    
    DESPESAS:
    ---------
    Salários e Encargos: R$ {dados_empresa['despesas']['salarios']:>11,.2f}
    Aluguel e Condomínio: R$ {dados_empresa['despesas']['aluguel']:>10,.2f}
    Outras Despesas: R$ {dados_empresa['despesas']['outras']:>15,.2f}
    {'-'*50}
    Total de Despesas: R$ {sum(dados_empresa['despesas'].values()):>14,.2f}
    
    {'='*60}
    RESULTADO DO PERÍODO: R$ {sum(dados_empresa['receitas'].values()) - sum(dados_empresa['despesas'].values()):>10,.2f}
    """
    
    return template

# Dados de exemplo
dados = {
    'nome': 'TechSolutions Ltda',
    'receitas': {
        'produtos': 150000.00,
        'servicos': 75000.00,
        'outras': 5000.00
    },
    'despesas': {
        'salarios': 80000.00,
        'aluguel': 15000.00,
        'outras': 25000.00
    }
}

periodo = {
    'inicio': datetime.date(2025, 1, 1),
    'fim': datetime.date(2025, 3, 31)
}

relatorio = gerar_relatorio_financeiro(dados, periodo)
print(relatorio)
```


### Internacionalização e Localização

A interpolação desempenha papel crucial em sistemas de internacionalização, permitindo que templates de mensagens sejam traduzidos mantendo a posição das variáveis. O uso adequado de formatação nomeada facilita a tradução e adaptação cultural.

```python
# Sistema de internacionalização simples
mensagens = {
    'pt_BR': {
        'boas_vindas': 'Bem-vindo, {nome}! Você tem {quantidade} {item}.',
        'data_formato': '{data:%d de %B de %Y}',
        'moeda_formato': 'R$ {valor:,.2f}'
    },
    'en_US': {
        'boas_vindas': 'Welcome, {nome}! You have {quantidade} {item}.',
        'data_formato': '{data:%B %d, %Y}',
        'moeda_formato': '${valor:,.2f}'
    }
}

def obter_mensagem(idioma, chave, **kwargs):
    template = mensagens[idioma][chave]
    return template.format(**kwargs)

# Exemplos de uso
print(obter_mensagem('pt_BR', 'boas_vindas', nome='João', quantidade=5, item='mensagens'))
print(obter_mensagem('en_US', 'boas_vindas', nome='John', quantidade=5, item='messages'))

data_atual = datetime.date.today()
print(obter_mensagem('pt_BR', 'data_formato', data=data_atual))
print(obter_mensagem('en_US', 'data_formato', data=data_atual))
```


## Técnicas Avançadas e Otimizações

### Formatação Condicional e Dinâmica

A interpolação permite implementar lógica de formatação sofisticada, adaptando a apresentação com base no contexto dos dados. Esta flexibilidade é especialmente valiosa em aplicações que precisam apresentar informações de forma contextual.

```python
def formatar_status_conta(conta):
    # Formatação condicional baseada no saldo
    cor_saldo = "verde" if conta['saldo'] >= 0 else "vermelho"
    simbolo_saldo = "+" if conta['saldo'] > 0 else ""
    
    # Formatação de limites
    limite_info = f"Limite disponível: R$ {conta['limite']:,.2f}" if conta['limite'] > 0 else "Sem limite especial"
    
    # Status da conta
    if conta['saldo'] >= conta['limite']:
        status = "✅ Conta em excelente situação"
    elif conta['saldo'] >= 0:
        status = "⚠️  Saldo baixo"
    else:
        status = "❌ Conta em débito"
    
    return f"""
    EXTRATO DA CONTA - {conta['numero']}
    Titular: {conta['titular']}
    Saldo atual: {simbolo_saldo}R$ {abs(conta['saldo']):,.2f} ({cor_saldo})
    {limite_info}
    Status: {status}
    
    Última movimentação: {conta['ultima_movimentacao']:%d/%m/%Y às %H:%M}
    """

# Exemplo de uso
conta_exemplo = {
    'numero': '12345-6',
    'titular': 'Maria Oliveira',
    'saldo': -150.75,
    'limite': 1000.00,
    'ultima_movimentacao': datetime.datetime.now()
}

print(formatar_status_conta(conta_exemplo))
```


### Formatação de Estruturas de Dados Complexas

Para estruturas de dados complexas como listas aninhadas, dicionários e objetos customizados, a interpolação pode ser combinada com técnicas de processamento para criar apresentações organizadas e informativas.

```python
def formatar_estrutura_empresa(empresa):
    # Formatação de departamentos
    departamentos_info = []
    for dept in empresa['departamentos']:
        funcionarios_lista = ', '.join([f['nome'] for f in dept['funcionarios']])
        dept_info = f"  {dept['nome']} ({len(dept['funcionarios'])} funcionários): {funcionarios_lista}"
        departamentos_info.append(dept_info)
    
    # Cálculo de estatísticas
    total_funcionarios = sum(len(d['funcionarios']) for d in empresa['departamentos'])
    media_salario = sum(f['salario'] for d in empresa['departamentos'] for f in d['funcionarios']) / total_funcionarios
    
    return f"""
    RELATÓRIO ORGANIZACIONAL
    {'='*50}
    
    Empresa: {empresa['nome']}
    Fundada em: {empresa['fundacao']}
    Sede: {empresa['endereco']['cidade']}, {empresa['endereco']['estado']}
    
    ESTRUTURA ORGANIZACIONAL:
    {'-'*30}
{chr(10).join(departamentos_info)}
    
    ESTATÍSTICAS:
    {'-'*15}
    Total de funcionários: {total_funcionarios}
    Salário médio: R$ {media_salario:,.2f}
    Número de departamentos: {len(empresa['departamentos'])}
    """

# Dados complexos de exemplo
empresa_dados = {
    'nome': 'Inovação Tech',
    'fundacao': 2015,
    'endereco': {'cidade': 'São Paulo', 'estado': 'SP'},
    'departamentos': [
        {
            'nome': 'Desenvolvimento',
            'funcionarios': [
                {'nome': 'Ana Costa', 'salario': 8000},
                {'nome': 'Bruno Silva', 'salario': 7500},
                {'nome': 'Carla Mendes', 'salario': 9000}
            ]
        },
        {
            'nome': 'Marketing',
            'funcionarios': [
                {'nome': 'Diana Rocha', 'salario': 6000},
                {'nome': 'Eduardo Lima', 'salario': 5500}
            ]
        }
    ]
}

print(formatar_estrutura_empresa(empresa_dados))
```


## Conclusão

A interpolação de variáveis em Python evoluiu significativamente ao longo das versões da linguagem, oferecendo hoje múltiplas abordagens para diferentes necessidades e contextos. As f-strings representam o estado da arte em termos de performance e legibilidade, sendo a escolha recomendada para a maioria dos casos em Python 3.6+. O método `.format()` continua sendo valioso para situações que exigem compatibilidade com versões anteriores ou templates mais complexos, enquanto o operador % mantém relevância em código legado. Por fim, as Template strings oferecem uma alternativa segura para cenários onde a entrada de dados não é confiável.

A escolha adequada do método de interpolação deve considerar fatores como performance, legibilidade, segurança e compatibilidade. O domínio dessas técnicas é essencial para qualquer desenvolvedor Python, pois elas são fundamentais para a criação de aplicações robustas, manuteníveis e eficientes. A prática consistente com diferentes métodos e cenários permitirá identificar rapidamente a abordagem mais adequada para cada situação específica.

As técnicas avançadas de formatação, incluindo formatação condicional, processamento de estruturas complexas e sistemas de internacionalização, demonstram o poder e flexibilidade da interpolação em Python. Essas habilidades são particularmente valiosas no desenvolvimento de aplicações profissionais que requerem apresentação sofisticada de dados e adaptabilidade a diferentes contextos e culturas. O investimento no aprendizado aprofundado dessas técnicas resultará em código mais elegante, eficiente e profissional.

