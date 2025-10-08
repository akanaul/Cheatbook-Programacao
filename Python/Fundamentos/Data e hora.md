# Data e Hora em Python: Guia Completo para Estudo de Longo Prazo

- [[#Introdução|Introdução]]
- [[#Conceitos Fundamentais|Conceitos Fundamentais]]
	- [[#Conceitos Fundamentais#Epoch e Timestamp|Epoch e Timestamp]]
	- [[#Conceitos Fundamentais#Objetos Naive vs Aware|Objetos Naive vs Aware]]
- [[#Classes Principais do Módulo datetime|Classes Principais do Módulo datetime]]
	- [[#Classes Principais do Módulo datetime#1. datetime.date|1. datetime.date]]
	- [[#Classes Principais do Módulo datetime#2. datetime.time|2. datetime.time]]
	- [[#Classes Principais do Módulo datetime#3. datetime.datetime|3. datetime.datetime]]
	- [[#Classes Principais do Módulo datetime#4. datetime.timedelta|4. datetime.timedelta]]
- [[#Formatação e Parsing de Datas|Formatação e Parsing de Datas]]
	- [[#Formatação e Parsing de Datas#Método strftime() - Datetime para String|Método strftime() - Datetime para String]]
	- [[#Formatação e Parsing de Datas#Principais Códigos de Formato|Principais Códigos de Formato]]
	- [[#Formatação e Parsing de Datas#Método strptime() - String para Datetime|Método strptime() - String para Datetime]]
	- [[#Formatação e Parsing de Datas#Métodos fromisoformat() e isoformat()|Métodos fromisoformat() e isoformat()]]
- [[#Trabalhando com Timestamps|Trabalhando com Timestamps]]
	- [[#Trabalhando com Timestamps#Conversão para Timestamp|Conversão para Timestamp]]
	- [[#Trabalhando com Timestamps#Conversão de Timestamp|Conversão de Timestamp]]
- [[#Manipulação de Microssegundos e Precisão|Manipulação de Microssegundos e Precisão]]
	- [[#Manipulação de Microssegundos e Precisão#Removendo Componentes de Precisão|Removendo Componentes de Precisão]]
	- [[#Manipulação de Microssegundos e Precisão#Método replace()|Método replace()]]
- [[#Operações Aritméticas e Comparações|Operações Aritméticas e Comparações]]
	- [[#Operações Aritméticas e Comparações#Aritmética com Datetime|Aritmética com Datetime]]
	- [[#Operações Aritméticas e Comparações#Comparações|Comparações]]
- [[#Trabalhando com Fusos Horários|Trabalhando com Fusos Horários]]
	- [[#Trabalhando com Fusos Horários#Introdução ao pytz|Introdução ao pytz]]
	- [[#Trabalhando com Fusos Horários#Criando Datetime Timezone-Aware|Criando Datetime Timezone-Aware]]
	- [[#Trabalhando com Fusos Horários#Conversões entre Fusos Horários|Conversões entre Fusos Horários]]
- [[#Módulo time - Complemento ao datetime|Módulo time - Complemento ao datetime]]
	- [[#Módulo time - Complemento ao datetime#Principais Funções|Principais Funções]]
	- [[#Módulo time - Complemento ao datetime#Estrutura struct_time|Estrutura struct_time]]
- [[#Módulo calendar - Operações Calendáricas|Módulo calendar - Operações Calendáricas]]
	- [[#Módulo calendar - Operações Calendáricas#Funcionalidades Principais|Funcionalidades Principais]]
	- [[#Módulo calendar - Operações Calendáricas#Trabalhando com Semanas|Trabalhando com Semanas]]
- [[#Casos de Uso Práticos|Casos de Uso Práticos]]
	- [[#Casos de Uso Práticos#1. Calculadora de Idade|1. Calculadora de Idade]]
	- [[#Casos de Uso Práticos#2. Contador de Days até Evento|2. Contador de Days até Evento]]
	- [[#Casos de Uso Práticos#3. Gerador de Horários de Trabalho|3. Gerador de Horários de Trabalho]]
	- [[#Casos de Uso Práticos#4. Validador de Formato de Data|4. Validador de Formato de Data]]
- [[#Boas Práticas e Dicas Importantes|Boas Práticas e Dicas Importantes]]
	- [[#Boas Práticas e Dicas Importantes#1. Sempre Use Timezone-Aware para Aplicações Produção|1. Sempre Use Timezone-Aware para Aplicações Produção]]
	- [[#Boas Práticas e Dicas Importantes#2. Armazene Sempre em UTC|2. Armazene Sempre em UTC]]
	- [[#Boas Práticas e Dicas Importantes#3. Validação e Tratamento de Erros|3. Validação e Tratamento de Erros]]
	- [[#Boas Práticas e Dicas Importantes#4. Escolha da Classe Apropriada|4. Escolha da Classe Apropriada]]
	- [[#Boas Práticas e Dicas Importantes#5. Cuidado com Horário de Verão|5. Cuidado com Horário de Verão]]
- [[#Limitações e Considerações|Limitações e Considerações]]
	- [[#Limitações e Considerações#1. Precisão dos Timestamps|1. Precisão dos Timestamps]]
	- [[#Limitações e Considerações#2. Fusos Horários e Mudanças Políticas|2. Fusos Horários e Mudanças Políticas]]
	- [[#Limitações e Considerações#3. Performance com Muitas Operações|3. Performance com Muitas Operações]]
- [[#Debugging e Troubleshooting|Debugging e Troubleshooting]]
	- [[#Debugging e Troubleshooting#Problemas Comuns e Soluções|Problemas Comuns e Soluções]]
	- [[#Debugging e Troubleshooting#Ferramentas de Debug|Ferramentas de Debug]]
- [[#Conclusão|Conclusão]]
- [[#Referências|Referências]]

## Introdução

A manipulação de data e hora é uma das tarefas fundamentais em programação Python. O módulo `datetime` fornece classes para trabalhar com datas, horários, diferenças temporais e fusos horários de forma precisa e eficiente. Este guia abrangente cobre todos os aspectos essenciais para o domínio completo desta importante área da linguagem Python.

## Conceitos Fundamentais

### Epoch e Timestamp

O conceito de **epoch** refere-se ao ponto de referência temporal padrão: 1º de janeiro de 1970, 00:00:00 UTC. O **timestamp Unix** é o número de segundos transcorridos desde este momento, representando qualquer data e hora como um único número decimal. Esta representação padronizada facilita cálculos temporais e comparações entre diferentes sistemas.

### Objetos Naive vs Aware

Em Python, objetos de data e hora podem ser classificados em duas categorias:

- **Naive (Ingênuos)**: Não possuem informações sobre fuso horário, assumindo o horário local do sistema
- **Aware (Conscientes)**: Incluem informações explícitas sobre fuso horário, permitindo conversões precisas entre diferentes regiões

## Classes Principais do Módulo datetime

### 1. datetime.date

A classe `date` representa uma data específica (ano, mês, dia) sem componente temporal.

```python
from datetime import date

# Criando objetos date
hoje = date.today()  # Data atual
data_especifica = date(2025, 10, 8)  # 8 de outubro de 2025

# Propriedades principais
print(hoje.year)    # Ano
print(hoje.month)   # Mês (1-12)  
print(hoje.day)     # Dia (1-31)
print(hoje.weekday())     # Dia da semana (0=segunda, 6=domingo)
print(hoje.isoweekday())  # Dia da semana ISO (1=segunda, 7=domingo)
```

### 2. datetime.time

A classe `time` representa um horário específico (hora, minuto, segundo, microssegundo) independente de data.

```python
from datetime import time

# Criando objetos time
horario_atual = time(14, 30, 45, 123456)  # 14:30:45.123456
meio_dia = time(12, 0)  # 12:00:00

# Propriedades principais
print(horario_atual.hour)        # Hora (0-23)
print(horario_atual.minute)      # Minuto (0-59)
print(horario_atual.second)      # Segundo (0-59)
print(horario_atual.microsecond) # Microssegundo (0-999999)
```

### 3. datetime.datetime

A classe `datetime` combina data e hora em um único objeto, sendo a mais versátil para manipulação temporal completa.

```python
from datetime import datetime

# Obtendo datetime atual
agora = datetime.now()      # Horário local atual
agora_utc = datetime.utcnow()  # Horário UTC atual (descontinuado em Python 3.12+)

# Criando datetime específico
dt = datetime(2025, 10, 8, 14, 30, 45, 123456)

# Combinando date e time
from datetime import date, time
data = date(2025, 10, 8)
horario = time(14, 30, 45)
dt_combinado = datetime.combine(data, horario)
```

### 4. datetime.timedelta

A classe `timedelta` representa uma duração temporal - a diferença entre duas datas ou horários.

```python
from datetime import datetime, timedelta

# Criando objetos timedelta
uma_semana = timedelta(weeks=1)
cinco_dias = timedelta(days=5)
duas_horas = timedelta(hours=2)
duracao_complexa = timedelta(days=7, hours=3, minutes=30, seconds=45)

# Operações aritméticas
agora = datetime.now()
futuro = agora + uma_semana
passado = agora - cinco_dias

# Calculando diferenças
diferenca = futuro - agora
print(diferenca.days)         # Número de dias
print(diferenca.seconds)      # Segundos (dentro do último dia)
print(diferenca.total_seconds())  # Total em segundos
```

## Formatação e Parsing de Datas

### Método strftime() - Datetime para String

O método `strftime()` converte objetos datetime em strings formatadas usando códigos de formato específicos.

```python
from datetime import datetime

agora = datetime.now()

# Exemplos de formatação
print(agora.strftime("%Y-%m-%d"))          # 2025-10-08
print(agora.strftime("%d/%m/%Y %H:%M:%S")) # 08/10/2025 14:30:45
print(agora.strftime("%A, %B %d, %Y"))     # Terça-feira, Outubro 08, 2025
print(agora.strftime("%Y-%m-%d %H:%M"))    # 2025-10-08 14:30
```

### Principais Códigos de Formato

| Código | Significado | Exemplo |
|--------|-------------|---------|
| %Y | Ano com 4 dígitos | 2025 |
| %y | Ano com 2 dígitos | 25 |
| %m | Mês (01-12) | 10 |
| %B | Nome do mês completo | Outubro |
| %b | Nome do mês abreviado | Out |
| %d | Dia do mês (01-31) | 08 |
| %A | Nome do dia da semana | Terça-feira |
| %a | Nome do dia abreviado | Ter |
| %H | Hora (00-23) | 14 |
| %I | Hora (01-12) | 02 |
| %M | Minuto (00-59) | 30 |
| %S | Segundo (00-59) | 45 |
| %f | Microssegundo | 123456 |
| %p | AM/PM | PM |

### Método strptime() - String para Datetime

O método `strptime()` converte strings formatadas em objetos datetime.

```python
from datetime import datetime

# Parsing de diferentes formatos
dt1 = datetime.strptime("2025-10-08", "%Y-%m-%d")
dt2 = datetime.strptime("08/10/2025 14:30", "%d/%m/%Y %H:%M")
dt3 = datetime.strptime("October 8, 2025", "%B %d, %Y")

# Exemplo prático
data_string = "2025-10-08 14:30:45"
dt_objeto = datetime.strptime(data_string, "%Y-%m-%d %H:%M:%S")
```

### Métodos fromisoformat() e isoformat()

Para trabalhar com formato ISO 8601, Python oferece métodos especializados.

```python
from datetime import datetime

# Convertendo de ISO format para datetime
dt = datetime.fromisoformat("2025-10-08T14:30:45")
dt_com_tz = datetime.fromisoformat("2025-10-08T14:30:45+03:00")

# Convertendo datetime para ISO format
agora = datetime.now()
iso_string = agora.isoformat()  # "2025-10-08T14:30:45.123456"
iso_sem_micro = agora.isoformat(timespec='seconds')  # "2025-10-08T14:30:45"
```

## Trabalhando com Timestamps

### Conversão para Timestamp

```python
from datetime import datetime
import time

# Datetime para timestamp
dt = datetime(2025, 10, 8, 14, 30, 45)
timestamp = dt.timestamp()  # Retorna float com segundos desde epoch

# Timestamp atual
timestamp_atual = time.time()
```

### Conversão de Timestamp

```python
from datetime import datetime

# Timestamp para datetime
timestamp = 1728394245.123456
dt = datetime.fromtimestamp(timestamp)    # Horário local
dt_utc = datetime.utcfromtimestamp(timestamp)  # Horário UTC
```

## Manipulação de Microssegundos e Precisão

### Removendo Componentes de Precisão

```python
from datetime import datetime

agora = datetime.now()

# Removendo microssegundos
sem_micro = agora.replace(microsecond=0)

# Removendo segundos e microssegundos
sem_seg = agora.replace(second=0, microsecond=0)

# Usando isoformat com timespec
iso_segundos = agora.isoformat(timespec='seconds')
```

### Método replace()

O método `replace()` permite modificar componentes específicos de objetos datetime.

```python
from datetime import datetime

dt = datetime(2025, 10, 8, 14, 30, 45)

# Modificando componentes específicos
novo_ano = dt.replace(year=2026)
nova_hora = dt.replace(hour=16, minute=45)
sem_micro = dt.replace(microsecond=0)
```

## Operações Aritméticas e Comparações

### Aritmética com Datetime

```python
from datetime import datetime, timedelta

dt1 = datetime(2025, 10, 8, 14, 30)
dt2 = datetime(2025, 10, 15, 16, 45)

# Diferença entre datas
diferenca = dt2 - dt1
print(diferenca.days)          # 7
print(diferenca.seconds)       # 8100 (2 horas e 15 minutos em segundos)
print(diferenca.total_seconds())  # Total em segundos

# Adição e subtração
futuro = dt1 + timedelta(days=30, hours=5)
passado = dt1 - timedelta(weeks=2)
```

### Comparações

```python
from datetime import datetime

dt1 = datetime(2025, 10, 8)
dt2 = datetime(2025, 10, 15)

# Operadores de comparação
print(dt1 < dt2)   # True
print(dt1 == dt2)  # False
print(dt1 > dt2)   # False

# Encontrando min/max
datas = [dt1, dt2, datetime(2025, 9, 1)]
mais_antiga = min(datas)
mais_recente = max(datas)
```

## Trabalhando com Fusos Horários

### Introdução ao pytz

A biblioteca `pytz` fornece suporte abrangente para fusos horários.

```python
import pytz
from datetime import datetime

# Criando objetos timezone
utc = pytz.UTC
sao_paulo = pytz.timezone('America/Sao_Paulo')
nova_york = pytz.timezone('America/New_York')
toquio = pytz.timezone('Asia/Tokyo')

# Listando fusos horários disponíveis
fusos_brasil = [tz for tz in pytz.all_timezones if 'Brazil' in tz]
```

### Criando Datetime Timezone-Aware

```python
import pytz
from datetime import datetime

# Criando datetime com timezone
agora_utc = datetime.now(pytz.UTC)
agora_sp = datetime.now(pytz.timezone('America/Sao_Paulo'))

# Localizando datetime naive
dt_naive = datetime(2025, 10, 8, 14, 30)
dt_aware = pytz.timezone('America/Sao_Paulo').localize(dt_naive)

# Alternativa usando replace para UTC
dt_utc = dt_naive.replace(tzinfo=pytz.UTC)
```

### Conversões entre Fusos Horários

```python
import pytz
from datetime import datetime

# Criando datetime em um fuso
dt_sp = pytz.timezone('America/Sao_Paulo').localize(datetime(2025, 10, 8, 14, 30))

# Convertendo para outros fusos
dt_utc = dt_sp.astimezone(pytz.UTC)
dt_ny = dt_sp.astimezone(pytz.timezone('America/New_York'))
dt_toquio = dt_sp.astimezone(pytz.timezone('Asia/Tokyo'))

print(f"São Paulo: {dt_sp}")
print(f"UTC: {dt_utc}")  
print(f"Nova York: {dt_ny}")
print(f"Tóquio: {dt_toquio}")
```

## Módulo time - Complemento ao datetime

### Principais Funções

```python
import time

# Timestamp atual
timestamp = time.time()

# Formatação usando time
tempo_formatado = time.strftime("%Y-%m-%d %H:%M:%S")

# Pausar execução
time.sleep(2)  # Pausa por 2 segundos

# Conversões
time_tuple = time.localtime(timestamp)  # Tupla de tempo local
utc_tuple = time.gmtime(timestamp)      # Tupla de tempo UTC
timestamp_from_tuple = time.mktime(time_tuple)  # Tupla para timestamp
```

### Estrutura struct_time

```python
import time

# Obtendo struct_time
st = time.localtime()

# Acessando componentes
print(st.tm_year)   # Ano
print(st.tm_mon)    # Mês (1-12)
print(st.tm_mday)   # Dia do mês
print(st.tm_hour)   # Hora
print(st.tm_min)    # Minuto
print(st.tm_sec)    # Segundo
print(st.tm_wday)   # Dia da semana (0=segunda)
print(st.tm_yday)   # Dia do ano (1-366)
print(st.tm_isdst)  # Horário de verão
```

## Módulo calendar - Operações Calendáricas

### Funcionalidades Principais

```python
import calendar

# Verificações
print(calendar.isleap(2024))        # True - ano bissexto
print(calendar.weekday(2025, 10, 8)) # 2 - quarta-feira (0=segunda)
print(calendar.monthrange(2025, 10)) # (1, 31) - primeiro dia é terça, 31 dias

# Gerando calendários
print(calendar.month(2025, 10))     # Calendário do mês
print(calendar.calendar(2025))      # Calendário do ano completo

# Nomes localizados
print(calendar.month_name[10])      # October
print(calendar.day_name[2])         # Wednesday
```

### Trabalhando com Semanas

```python
import calendar

# Matriz de dias do mês
matriz_mes = calendar.monthcalendar(2025, 10)
for semana in matriz_mes:
    print(semana)  # [0, 0, 0, 1, 2, 3, 4], [5, 6, 7, 8, 9, 10, 11], ...

# Configurando primeiro dia da semana
calendar.setfirstweekday(calendar.SUNDAY)  # Domingo como primeiro dia
```

## Casos de Uso Práticos

### 1. Calculadora de Idade

```python
from datetime import date

def calcular_idade(data_nascimento):
    hoje = date.today()
    idade = hoje.year - data_nascimento.year
    
    # Verificar se já fez aniversário este ano
    if (hoje.month, hoje.day) < (data_nascimento.month, data_nascimento.day):
        idade -= 1
    
    return idade

nascimento = date(1990, 5, 15)
idade = calcular_idade(nascimento)
print(f"Idade: {idade} anos")
```

### 2. Contador de Days até Evento

```python
from datetime import datetime, timedelta

def dias_ate_evento(data_evento):
    agora = datetime.now()
    diferenca = data_evento - agora
    
    if diferenca.total_seconds() > 0:
        return diferenca.days
    else:
        return 0  # Evento já passou

evento = datetime(2025, 12, 25, 0, 0)  # Natal
dias = dias_ate_evento(evento)
print(f"Faltam {dias} dias para o Natal")
```

### 3. Gerador de Horários de Trabalho

```python
from datetime import datetime, timedelta

def gerar_horarios_trabalho(inicio, fim, intervalo_minutos):
    horarios = []
    atual = inicio
    
    while atual <= fim:
        horarios.append(atual.strftime("%H:%M"))
        atual += timedelta(minutes=intervalo_minutos)
    
    return horarios

inicio = datetime.now().replace(hour=9, minute=0, second=0, microsecond=0)
fim = datetime.now().replace(hour=17, minute=0, second=0, microsecond=0)
horarios = gerar_horarios_trabalho(inicio, fim, 30)
print(horarios)  # ['09:00', '09:30', '10:00', ..., '17:00']
```

### 4. Validador de Formato de Data

```python
from datetime import datetime

def validar_data(data_string, formato):
    try:
        datetime.strptime(data_string, formato)
        return True
    except ValueError:
        return False

# Testando diferentes formatos
formatos = [
    ("%Y-%m-%d", "2025-10-08"),
    ("%d/%m/%Y", "08/10/2025"),  
    ("%B %d, %Y", "October 8, 2025")
]

for formato, exemplo in formatos:
    valido = validar_data(exemplo, formato)
    print(f"{exemplo} com formato {formato}: {'Válido' if valido else 'Inválido'}")
```

## Boas Práticas e Dicas Importantes

### 1. Sempre Use Timezone-Aware para Aplicações Produção

```python
import pytz
from datetime import datetime

# ❌ Evitar - datetime naive
dt_naive = datetime.now()

# ✅ Recomendado - datetime aware
dt_aware = datetime.now(pytz.UTC)
```

### 2. Armazene Sempre em UTC

```python
import pytz
from datetime import datetime

# Para armazenamento em banco de dados
def salvar_evento(dt_local, timezone_usuario):
    # Converter para UTC antes de salvar
    dt_utc = dt_local.astimezone(pytz.UTC)
    # Salvar dt_utc no banco
    return dt_utc

def recuperar_evento(dt_utc, timezone_usuario):
    # Converter de UTC para fuso do usuário
    return dt_utc.astimezone(timezone_usuario)
```

### 3. Validação e Tratamento de Erros

```python
from datetime import datetime

def parse_data_segura(data_string, formato):
    try:
        return datetime.strptime(data_string, formato)
    except ValueError as e:
        print(f"Erro ao converter '{data_string}': {e}")
        return None

# Uso seguro
resultado = parse_data_segura("2025-13-08", "%Y-%m-%d")  # Retorna None
```

### 4. Escolha da Classe Apropriada

```python
from datetime import date, time, datetime

# Para apenas datas (aniversários, feriados)
aniversario = date(1990, 5, 15)

# Para apenas horários (horário de funcionamento)
abertura = time(9, 0)

# Para combinação completa (timestamps, logs)
log_entry = datetime.now()
```

### 5. Cuidado com Horário de Verão

```python
import pytz
from datetime import datetime

# Zona com horário de verão
tz_sp = pytz.timezone('America/Sao_Paulo')

# Use localize para datas no passado/futuro
dt = datetime(2025, 10, 8, 14, 30)
dt_aware = tz_sp.localize(dt)

# Use datetime.now(tz) para horário atual
agora = datetime.now(tz_sp)
```

## Limitações e Considerações

### 1. Precisão dos Timestamps

- Timestamps têm precisão limitada pela arquitetura do sistema
- Em sistemas de 32 bits, o "Problema do Ano 2038" pode afetar timestamps
- Para aplicações que requerem alta precisão, considere bibliotecas especializadas

### 2. Fusos Horários e Mudanças Políticas

- Fusos horários podem mudar devido a decisões políticas
- Mantenha a biblioteca `pytz` sempre atualizada
- Para aplicações críticas, considere usar `zoneinfo` (Python 3.9+)

### 3. Performance com Muitas Operações

- Para processamento de grandes volumes de dados temporais, considere:
  - `pandas` com `DatetimeIndex`
  - `numpy.datetime64` para arrays
  - Bibliotecas especializadas como `arrow` ou `pendulum`

## Debugging e Troubleshooting

### Problemas Comuns e Soluções

```python
from datetime import datetime
import pytz

# Problema: Comparação entre naive e aware
dt_naive = datetime(2025, 10, 8, 14, 30)
dt_aware = datetime.now(pytz.UTC)

# ❌ Isso causará TypeError
# resultado = dt_naive < dt_aware

# ✅ Solução: Tornar ambos aware ou ambos naive
dt_naive_aware = pytz.UTC.localize(dt_naive)
resultado = dt_naive_aware < dt_aware
```

### Ferramentas de Debug

```python
from datetime import datetime
import pytz

def debug_datetime(dt):
    """Função helper para debug de objetos datetime"""
    print(f"Valor: {dt}")
    print(f"Tipo: {type(dt)}")
    print(f"Timezone: {dt.tzinfo}")
    print(f"Naive: {dt.tzinfo is None}")
    print(f"ISO Format: {dt.isoformat()}")
    if dt.tzinfo:
        print(f"UTC Offset: {dt.utcoffset()}")
    print("-" * 30)

# Exemplo de uso
dt1 = datetime.now()
dt2 = datetime.now(pytz.UTC)
debug_datetime(dt1)
debug_datetime(dt2)
```

## Conclusão

O domínio completo da manipulação de data e hora em Python requer compreensão sólida dos conceitos fundamentais, prática com as diferentes classes e métodos, e atenção às melhores práticas de timezone e formatação. Este conhecimento é essencial para desenvolvimento de aplicações robustas que lidem com dados temporais de forma precisa e confiável.

A combinação dos módulos `datetime`, `time`, `calendar` e bibliotecas como `pytz` oferece um conjunto completo de ferramentas para qualquer necessidade relacionada ao tempo em Python. Com este guia como referência, você estará preparado para enfrentar os desafios mais complexos de manipulação temporal em seus projetos.

## Referências

[Documentação Oficial Python - datetime](https://docs.python.org/3/library/datetime.html)

[Python Datetime Tutorial: Manipulate Times, Dates, and Time Spans](https://www.dataquest.io/blog/python-datetime-tutorial/)

[Python Datetime Guide | Timezone & Format Handling](https://inventivehq.com/working-with-datetime-in-python/)

[Using Python datetime to Work With Dates and Times](https://realpython.com/python-datetime/)

[Python datetime (With Examples)](https://www.programiz.com/python-programming/datetime)

[Python strftime() - datetime to string](https://www.programiz.com/python-programming/datetime/strftime)

[Python strptime() - string to datetime object](https://www.programiz.com/python-programming/datetime/strptime)

[Manipulate Date and Time with the Datetime Module in Python](https://www.geeksforgeeks.org/python/manipulate-date-and-time-with-the-datetime-module-in-python/)

[A Guide to Python's datetime Module: Use Cases and Examples](https://dev.to/usooldatascience/a-guide-to-pythons-datetime-module-use-cases-and-examples-1odc)

[How to use timedelta in Python? (with Examples)](https://favtutor.com/blogs/timedelta-python)

[Python 3: Unix Timestamp](https://csatlas.com/python-unix-timestamp/)

[How to Convert DateTime to UNIX Timestamp in Python ?](https://www.geeksforgeeks.org/python/how-to-convert-datetime-to-unix-timestamp-in-python/)

[fromisoformat() method](https://www.geeksforgeeks.org/python/fromisoformat-function-of-datetime-date-class-in-python/)

[Isoformat to datetime - Python](https://www.geeksforgeeks.org/python/isoformat-to-datetime-python/)

[Python time Module (with Examples)](https://www.programiz.com/python-programming/time)

[Python pytz](https://www.geeksforgeeks.org/python/python-pytz/)

[pytz utc conversion - python](https://stackoverflow.com/questions/1357711/pytz-utc-conversion)

[Python calendar Module](https://www.w3schools.com/Python/ref_module_calendar.asp)

[Python calendar module - Python Geeks](https://pythongeeks.org/python-calendar-module/)

[The Python calendar Module: Create Calendars With Python](https://realpython.com/python-calendar-module/)

[Python time mktime() Method](https://www.tutorialspoint.com/python/time_mktime.htm)

[Python time.mktime Function - Complete Guide](https://zetcode.com/python/time-mktime/)

[Get current date using Python](https://www.geeksforgeeks.org/python/get-current-date-using-python/)

[How to get current date and time in Python? (With Examples)](https://www.programiz.com/python-programming/datetime/current-datetime)

[Python: Drop microseconds from datetime](https://www.w3resource.com/python-exercises/date-time-exercise/python-date-time-exercise-17.php)

[Remove Seconds from the Datetime in Python](https://www.geeksforgeeks.org/python/remove-seconds-from-the-datetime-in-python/)

[isoweekday function in Python](https://pythontic.com/datetime/date/isoweekday)

[Isoweekday() Method Of Datetime Class In Python](https://www.geeksforgeeks.org/python/isoweekday-method-of-datetime-class-in-python/)

[How to Use Python's datetime](https://www.kdnuggets.com/2019/06/how-use-datetime.html)

[Understanding Python DateTime astimezone()](https://www.browserstack.com/guide/python-datetime-astimezone)

[Python datetime to string without microsecond component](https://stackoverflow.com/questions/7999935/python-datetime-to-string-without-microsecond-component)

[How to make a datetime object aware (not naive)?](https://stackoverflow.com/questions/7065164/how-to-make-a-datetime-object-aware-not-naive)

[Easiest way to combine date and time strings to single datetime object using Python?](https://stackoverflow.com/questions/9578906/easiest-way-to-combine-date-and-time-strings-to-single-datetime-object-using-pyt)