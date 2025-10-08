# Manipulação de Arquivos e Diretórios em Python

## Índice:

- [[#Introdução|Introdução]]
- [[#Conceitos Fundamentais|Conceitos Fundamentais]]
	- [[#Conceitos Fundamentais#Sistema de Arquivos|Sistema de Arquivos]]
	- [[#Conceitos Fundamentais#Tipos de Arquivos|Tipos de Arquivos]]
	- [[#Conceitos Fundamentais#Caminhos Absolutos vs Relativos|Caminhos Absolutos vs Relativos]]
- [[#Módulos Essenciais|Módulos Essenciais]]
	- [[#Módulos Essenciais#Módulo os|Módulo os]]
	- [[#Módulos Essenciais#Módulo pathlib|Módulo pathlib]]
	- [[#Módulos Essenciais#Módulo shutil|Módulo shutil]]
- [[#Manipulação Básica de Arquivos|Manipulação Básica de Arquivos]]
	- [[#Manipulação Básica de Arquivos#Abrindo Arquivos|Abrindo Arquivos]]
	- [[#Manipulação Básica de Arquivos#Lendo Arquivos|Lendo Arquivos]]
		- [[#Lendo Arquivos#Métodos de Leitura|Métodos de Leitura]]
	- [[#Manipulação Básica de Arquivos#Escrevendo Arquivos|Escrevendo Arquivos]]
- [[#Modos de Abertura de Arquivos|Modos de Abertura de Arquivos]]
	- [[#Modos de Abertura de Arquivos#Modos Binários|Modos Binários]]
	- [[#Modos de Abertura de Arquivos#Exemplos Práticos de Modos|Exemplos Práticos de Modos]]
- [[#Context Managers e a Instrução with|Context Managers e a Instrução with]]
	- [[#Context Managers e a Instrução with#Por Que Usar Context Managers?|Por Que Usar Context Managers?]]
	- [[#Context Managers e a Instrução with#Funcionamento Interno|Funcionamento Interno]]
	- [[#Context Managers e a Instrução with#Context Managers para Múltiplos Arquivos|Context Managers para Múltiplos Arquivos]]
- [[#Tratamento de Exceções|Tratamento de Exceções]]
	- [[#Tratamento de Exceções#Exceções Comuns em Operações de Arquivo|Exceções Comuns em Operações de Arquivo]]
	- [[#Tratamento de Exceções#Tratamento Robusto com Finally|Tratamento Robusto com Finally]]
- [[#Manipulação de Diretórios|Manipulação de Diretórios]]
	- [[#Manipulação de Diretórios#Operações Básicas com os|Operações Básicas com os]]
	- [[#Manipulação de Diretórios#Listagem e Navegação|Listagem e Navegação]]
	- [[#Manipulação de Diretórios#Operações com pathlib|Operações com pathlib]]
- [[#Trabalhando com Caminhos usando pathlib|Trabalhando com Caminhos usando pathlib]]
	- [[#Trabalhando com Caminhos usando pathlib#Vantagens do pathlib|Vantagens do pathlib]]
	- [[#Trabalhando com Caminhos usando pathlib#Operações com Path|Operações com Path]]
	- [[#Trabalhando com Caminhos usando pathlib#Navegação e Resolução de Caminhos|Navegação e Resolução de Caminhos]]
	- [[#Trabalhando com Caminhos usando pathlib#Padrões de Busca|Padrões de Busca]]
- [[#Operações com o Módulo shutil|Operações com o Módulo shutil]]
	- [[#Operações com o Módulo shutil#Cópia de Arquivos|Cópia de Arquivos]]
	- [[#Operações com o Módulo shutil#Movimentação e Renomeação|Movimentação e Renomeação]]
	- [[#Operações com o Módulo shutil#Remoção de Arquivos e Diretórios|Remoção de Arquivos e Diretórios]]
	- [[#Operações com o Módulo shutil#Operações de Arquivamento|Operações de Arquivamento]]
- [[#Pattern Matching com glob|Pattern Matching com glob]]
	- [[#Pattern Matching com glob#Padrões Básicos|Padrões Básicos]]
	- [[#Pattern Matching com glob#Busca Recursiva|Busca Recursiva]]
	- [[#Pattern Matching com glob#Exemplos Práticos|Exemplos Práticos]]
- [[#Arquivos Binários|Arquivos Binários]]
	- [[#Arquivos Binários#Leitura e Escrita Básica|Leitura e Escrita Básica]]
	- [[#Arquivos Binários#Trabalhando com Estruturas Binárias|Trabalhando com Estruturas Binárias]]
	- [[#Arquivos Binários#Validação de Arquivos Binários|Validação de Arquivos Binários]]
- [[#Trabalhando com CSV|Trabalhando com CSV]]
	- [[#Trabalhando com CSV#Usando o Módulo csv|Usando o Módulo csv]]
	- [[#Trabalhando com CSV#CSV com Pandas|CSV com Pandas]]
	- [[#Trabalhando com CSV#Manipulação Avançada de CSV|Manipulação Avançada de CSV]]
- [[#Manipulação de Arquivos JSON|Manipulação de Arquivos JSON]]
	- [[#Manipulação de Arquivos JSON#Operações Básicas com JSON|Operações Básicas com JSON]]
	- [[#Manipulação de Arquivos JSON#Manipulação Avançada de JSON|Manipulação Avançada de JSON]]
	- [[#Manipulação de Arquivos JSON#Validação e Tratamento de Erros JSON|Validação e Tratamento de Erros JSON]]
- [[#Permissões de Arquivos|Permissões de Arquivos]]
	- [[#Permissões de Arquivos#Trabalhando com os.chmod()|Trabalhando com os.chmod()]]
	- [[#Permissões de Arquivos#Verificação de Acesso|Verificação de Acesso]]
	- [[#Permissões de Arquivos#Gerenciamento Seguro de Permissões|Gerenciamento Seguro de Permissões]]
- [[#Boas Práticas e Segurança|Boas Práticas e Segurança]]
	- [[#Boas Práticas e Segurança#Validação de Entrada|Validação de Entrada]]
	- [[#Boas Práticas e Segurança#Tratamento Robusto de Erros|Tratamento Robusto de Erros]]
	- [[#Boas Práticas e Segurança#Limpeza de Recursos|Limpeza de Recursos]]
	- [[#Boas Práticas e Segurança#Monitoramento de Operações|Monitoramento de Operações]]
- [[#Considerações Finais|Considerações Finais]]
	- [[#Considerações Finais#Pontos-Chave para Lembrar|Pontos-Chave para Lembrar]]
	- [[#Considerações Finais#Próximos Passos|Próximos Passos]]
- [[#Referências|Referências]]
## Introdução

A manipulação de arquivos e diretórios é uma habilidade fundamental na programação Python, essencial para desenvolvimento de aplicações que precisam interagir com o sistema de arquivos. Python oferece uma ampla gama de módulos e ferramentas integradas que facilitam essas operações, desde tarefas simples como leitura e escrita de arquivos até operações mais complexas como manipulação de permissões e navegação em estruturas de diretórios.

## Conceitos Fundamentais

### Sistema de Arquivos

O sistema de arquivos é a estrutura organizacional que um sistema operacional utiliza para controlar como os dados são armazenados e recuperados. Em Python, trabalhamos com abstrações que nos permitem interagir com arquivos e diretórios independentemente do sistema operacional subjacente.

### Tipos de Arquivos

**Arquivos de Texto**: Contêm dados legíveis por humanos, codificados em formatos como UTF-8, ASCII ou outras codificações de texto.

**Arquivos Binários**: Contêm dados em formato binário, como imagens, vídeos, executáveis ou qualquer formato não textual.

### Caminhos Absolutos vs Relativos

**Caminho Absoluto**: Especifica a localização completa de um arquivo ou diretório a partir da raiz do sistema de arquivos (ex: `/home/usuario/documento.txt` no Linux ou `C:\Users\Usuario\documento.txt` no Windows).

**Caminho Relativo**: Especifica a localização em relação ao diretório de trabalho atual (ex: `../pasta/arquivo.txt` ou `dados/config.json`).

## Módulos Essenciais

### Módulo os

O módulo `os` fornece uma interface para interagir com o sistema operacional, incluindo operações de baixo nível com arquivos e diretórios.

```python
import os

# Obter diretório de trabalho atual
diretorio_atual = os.getcwd()
print(f"Diretório atual: {diretorio_atual}")

# Listar conteúdo de um diretório
conteudo = os.listdir('.')
print(f"Conteúdo: {conteudo}")

# Verificar se um caminho existe
if os.path.exists('arquivo.txt'):
    print("Arquivo existe")
```

### Módulo pathlib

Introduzido no Python 3.4, o `pathlib` oferece uma abordagem orientada a objetos para manipulação de caminhos, sendo mais moderno e intuitivo que o `os.path`.

```python
from pathlib import Path

# Criar um objeto Path
caminho = Path('documentos/arquivo.txt')

# Verificar se é arquivo ou diretório
if caminho.is_file():
    print("É um arquivo")
elif caminho.is_dir():
    print("É um diretório")

# Obter informações do caminho
print(f"Nome: {caminho.name}")
print(f"Extensão: {caminho.suffix}")
print(f"Diretório pai: {caminho.parent}")
```

### Módulo shutil

O `shutil` (shell utilities) fornece operações de alto nível para manipulação de arquivos e coleções de arquivos.

```python
import shutil

# Copiar arquivo
shutil.copy('origem.txt', 'destino.txt')

# Copiar diretório inteiro
shutil.copytree('pasta_origem', 'pasta_destino')

# Mover arquivo ou diretório
shutil.move('arquivo.txt', 'nova_pasta/arquivo.txt')
```

## Manipulação Básica de Arquivos

### Abrindo Arquivos

A função `open()` é a principal ferramenta para trabalhar com arquivos em Python:

```python
# Abertura básica de arquivo
arquivo = open('exemplo.txt', 'r', encoding='utf-8')
conteudo = arquivo.read()
arquivo.close()

# Usando with statement (recomendado)
with open('exemplo.txt', 'r', encoding='utf-8') as arquivo:
    conteudo = arquivo.read()
    print(conteudo)
```

### Lendo Arquivos

#### Métodos de Leitura

```python
with open('arquivo.txt', 'r', encoding='utf-8') as f:
    # Ler todo o conteúdo
    conteudo_completo = f.read()
    
    # Voltar ao início do arquivo
    f.seek(0)
    
    # Ler linha por linha
    for linha in f:
        print(linha.strip())
    
    # Voltar ao início novamente
    f.seek(0)
    
    # Ler uma linha específica
    primeira_linha = f.readline()
    
    # Ler todas as linhas em uma lista
    f.seek(0)
    todas_linhas = f.readlines()
```

### Escrevendo Arquivos

```python
# Escrever texto simples
with open('saida.txt', 'w', encoding='utf-8') as f:
    f.write("Primeira linha\n")
    f.write("Segunda linha\n")

# Escrever múltiplas linhas
linhas = ["Linha 1\n", "Linha 2\n", "Linha 3\n"]
with open('multiplas.txt', 'w', encoding='utf-8') as f:
    f.writelines(linhas)

# Anexar conteúdo a um arquivo existente
with open('log.txt', 'a', encoding='utf-8') as f:
    f.write("Nova entrada no log\n")
```

## Modos de Abertura de Arquivos

O modo de abertura determina como o arquivo será utilizado:

| Modo | Descrição | Posição Inicial | Cria Arquivo |
|------|-----------|----------------|--------------|
| 'r' | Leitura apenas | Início | Não |
| 'w' | Escrita (sobrescreve) | Início | Sim |
| 'a' | Anexar | Final | Sim |
| 'x' | Criação exclusiva | Início | Sim (falha se existe) |
| 'r+' | Leitura e escrita | Início | Não |
| 'w+' | Leitura e escrita (sobrescreve) | Início | Sim |
| 'a+' | Leitura e anexar | Final | Sim |

### Modos Binários

Adicione 'b' ao modo para trabalhar com arquivos binários:

```python
# Leitura binária
with open('imagem.jpg', 'rb') as f:
    dados_binarios = f.read()

# Escrita binária
with open('copia_imagem.jpg', 'wb') as f:
    f.write(dados_binarios)
```

### Exemplos Práticos de Modos

```python
# Modo 'x' - Criação exclusiva
try:
    with open('novo_arquivo.txt', 'x') as f:
        f.write("Arquivo criado com sucesso")
except FileExistsError:
    print("Arquivo já existe!")

# Modo 'r+' - Leitura e escrita
with open('dados.txt', 'r+') as f:
    conteudo = f.read()
    f.seek(0)
    f.write("PREFIXO: " + conteudo)

# Modo 'a+' - Anexar e ler
with open('log.txt', 'a+') as f:
    f.write("Nova entrada\n")
    f.seek(0)
    print(f.read())
```

## Context Managers e a Instrução with

### Por Que Usar Context Managers?

Context managers garantem que recursos sejam adequadamente liberados, mesmo em caso de exceções:

```python
# Forma incorreta (sem garantia de fechamento)
arquivo = open('dados.txt', 'r')
dados = arquivo.read()
# Se ocorrer erro aqui, o arquivo pode não ser fechado
arquivo.close()

# Forma correta (com context manager)
with open('dados.txt', 'r') as arquivo:
    dados = arquivo.read()
    # Arquivo é automaticamente fechado, mesmo com erro
```

### Funcionamento Interno

```python
# O que acontece internamente com 'with'
class GerenciadorArquivo:
    def __init__(self, nome, modo):
        self.nome = nome
        self.modo = modo
        self.arquivo = None
    
    def __enter__(self):
        print(f"Abrindo arquivo {self.nome}")
        self.arquivo = open(self.nome, self.modo)
        return self.arquivo
    
    def __exit__(self, tipo_exc, valor_exc, traceback):
        print(f"Fechando arquivo {self.nome}")
        if self.arquivo:
            self.arquivo.close()

# Uso do context manager personalizado
with GerenciadorArquivo('teste.txt', 'w') as f:
    f.write("Teste de context manager")
```

### Context Managers para Múltiplos Arquivos

```python
# Múltiplos arquivos em um único with
with open('entrada.txt', 'r') as entrada, \
     open('saida.txt', 'w') as saida:
    dados = entrada.read()
    saida.write(dados.upper())

# Usando contextlib para múltiplos recursos
from contextlib import ExitStack

with ExitStack() as stack:
    arquivos = [
        stack.enter_context(open(f'arquivo_{i}.txt', 'w'))
        for i in range(3)
    ]
    
    for i, arquivo in enumerate(arquivos):
        arquivo.write(f"Conteúdo do arquivo {i}")
```

## Tratamento de Exceções

### Exceções Comuns em Operações de Arquivo

```python
import os

def operacao_arquivo_segura(nome_arquivo):
    try:
        with open(nome_arquivo, 'r', encoding='utf-8') as f:
            return f.read()
    
    except FileNotFoundError:
        print(f"Arquivo '{nome_arquivo}' não encontrado")
        return None
    
    except PermissionError:
        print(f"Sem permissão para acessar '{nome_arquivo}'")
        return None
    
    except IsADirectoryError:
        print(f"'{nome_arquivo}' é um diretório, não um arquivo")
        return None
    
    except UnicodeDecodeError:
        print(f"Erro de codificação ao ler '{nome_arquivo}'")
        return None
    
    except IOError as e:
        print(f"Erro de I/O: {e}")
        return None

# Exemplo de uso
conteudo = operacao_arquivo_segura('documento.txt')
if conteudo:
    print("Arquivo lido com sucesso")
```

### Tratamento Robusto com Finally

```python
def processar_arquivo_com_cleanup(nome_arquivo):
    arquivo = None
    arquivo_temp = None
    
    try:
        arquivo = open(nome_arquivo, 'r')
        arquivo_temp = open('temp.txt', 'w')
        
        # Processamento
        dados = arquivo.read()
        dados_processados = dados.upper()
        arquivo_temp.write(dados_processados)
        
        return True
        
    except Exception as e:
        print(f"Erro durante processamento: {e}")
        return False
        
    finally:
        # Garantir fechamento dos arquivos
        if arquivo:
            arquivo.close()
        if arquivo_temp:
            arquivo_temp.close()
        
        # Limpar arquivo temporário se necessário
        if os.path.exists('temp.txt'):
            os.remove('temp.txt')
```

## Manipulação de Diretórios

### Operações Básicas com os

```python
import os

# Criar diretório
os.mkdir('novo_diretorio')

# Criar diretórios aninhados
os.makedirs('pasta/subpasta/subsubpasta', exist_ok=True)

# Remover diretório vazio
os.rmdir('diretorio_vazio')

# Remover diretório e todo seu conteúdo
import shutil
shutil.rmtree('diretorio_com_conteudo')

# Navegar entre diretórios
diretorio_original = os.getcwd()
os.chdir('nova_pasta')
print(f"Agora em: {os.getcwd()}")
os.chdir(diretorio_original)  # Voltar
```

### Listagem e Navegação

```python
import os
from pathlib import Path

# Listar conteúdo do diretório atual
for item in os.listdir('.'):
    caminho_completo = os.path.join('.', item)
    if os.path.isfile(caminho_completo):
        print(f"Arquivo: {item}")
    elif os.path.isdir(caminho_completo):
        print(f"Diretório: {item}")

# Navegação recursiva
for raiz, diretorios, arquivos in os.walk('.'):
    print(f"Diretório: {raiz}")
    for arquivo in arquivos:
        print(f"  Arquivo: {arquivo}")
    for diretorio in diretorios:
        print(f"  Subdiretório: {diretorio}")
```

### Operações com pathlib

```python
from pathlib import Path

# Criar diretório
pasta = Path('nova_pasta')
pasta.mkdir(exist_ok=True)

# Criar estrutura aninhada
estrutura = Path('projeto/src/utils')
estrutura.mkdir(parents=True, exist_ok=True)

# Listar conteúdo
pasta_atual = Path('.')
for item in pasta_atual.iterdir():
    if item.is_file():
        print(f"Arquivo: {item.name}")
    elif item.is_dir():
        print(f"Diretório: {item.name}")

# Navegação recursiva com pathlib
for arquivo in pasta_atual.rglob('*.py'):
    print(f"Arquivo Python: {arquivo}")
```

## Trabalhando com Caminhos usando pathlib

### Vantagens do pathlib

O módulo `pathlib` oferece uma interface mais intuitiva e robusta para manipulação de caminhos:

```python
from pathlib import Path

# Criação de caminhos
caminho = Path('documentos') / 'projeto' / 'arquivo.txt'
print(caminho)  # documentos/projeto/arquivo.txt (ou documentos\projeto\arquivo.txt no Windows)

# Informações do caminho
arquivo = Path('/home/usuario/documento.pdf')
print(f"Nome: {arquivo.name}")                    # documento.pdf
print(f"Nome sem extensão: {arquivo.stem}")       # documento
print(f"Extensão: {arquivo.suffix}")              # .pdf
print(f"Todas extensões: {arquivo.suffixes}")     # ['.pdf']
print(f"Diretório pai: {arquivo.parent}")         # /home/usuario
print(f"Caminho absoluto: {arquivo.absolute()}")
```

### Operações com Path

```python
from pathlib import Path

# Verificações de tipo
caminho = Path('exemplo.txt')
print(f"Existe: {caminho.exists()}")
print(f"É arquivo: {caminho.is_file()}")
print(f"É diretório: {caminho.is_dir()}")
print(f"É link simbólico: {caminho.is_symlink()}")

# Operações de leitura/escrita direta
texto_path = Path('dados.txt')
texto_path.write_text('Conteúdo do arquivo', encoding='utf-8')
conteudo = texto_path.read_text(encoding='utf-8')

# Para arquivos binários
binario_path = Path('dados.bin')
binario_path.write_bytes(b'\x00\x01\x02\x03')
dados_bin = binario_path.read_bytes()
```

### Navegação e Resolução de Caminhos

```python
from pathlib import Path

# Caminho atual e home
atual = Path.cwd()
home = Path.home()
print(f"Diretório atual: {atual}")
print(f"Diretório home: {home}")

# Resolução de caminhos relativos
relativo = Path('../projeto/config.json')
absoluto = relativo.resolve()
print(f"Caminho absoluto: {absoluto}")

# Caminho relativo entre dois pontos
caminho1 = Path('/home/usuario/projeto/src')
caminho2 = Path('/home/usuario/projeto/docs/manual.pdf')
relativo = caminho2.relative_to(caminho1.parent)
print(f"Caminho relativo: {relativo}")  # docs/manual.pdf
```

### Padrões de Busca

```python
from pathlib import Path

# Buscar arquivos por padrão
projeto = Path('meu_projeto')

# Todos os arquivos .py no diretório atual
arquivos_py = list(projeto.glob('*.py'))

# Busca recursiva por arquivos .py
todos_py = list(projeto.rglob('*.py'))

# Padrões mais complexos
configs = list(projeto.glob('**/config/*.json'))
testes = list(projeto.glob('tests/**/*_test.py'))

for arquivo in todos_py:
    print(f"Arquivo Python: {arquivo}")
```

## Operações com o Módulo shutil

### Cópia de Arquivos

```python
import shutil
from pathlib import Path

# Cópia simples (apenas conteúdo)
shutil.copyfile('origem.txt', 'destino.txt')

# Cópia com metadados (timestamps, permissões)
shutil.copy2('origem.txt', 'destino_com_metadata.txt')

# Cópia para diretório
shutil.copy('arquivo.txt', 'pasta_destino/')

# Cópia de diretório inteiro
shutil.copytree('pasta_origem', 'pasta_destino')

# Cópia seletiva com função de filtro
def ignorar_temporarios(diretorio, conteudo):
    return [item for item in conteudo if item.endswith('.tmp')]

shutil.copytree('projeto', 'backup_projeto', ignore=ignorar_temporarios)
```

### Movimentação e Renomeação

```python
import shutil

# Mover arquivo
shutil.move('arquivo.txt', 'nova_pasta/arquivo.txt')

# Renomear arquivo
shutil.move('nome_antigo.txt', 'nome_novo.txt')

# Mover diretório
shutil.move('pasta_antiga', 'pasta_nova')
```

### Remoção de Arquivos e Diretórios

```python
import shutil
import os
from pathlib import Path

# Remover arquivo
os.remove('arquivo.txt')
# ou com pathlib
Path('arquivo.txt').unlink()

# Remover diretório vazio
os.rmdir('diretorio_vazio')
# ou com pathlib
Path('diretorio_vazio').rmdir()

# Remover diretório e todo conteúdo
shutil.rmtree('diretorio_com_conteudo')

# Remoção segura com verificação
def remover_seguro(caminho):
    path_obj = Path(caminho)
    if path_obj.exists():
        if path_obj.is_file():
            path_obj.unlink()
            print(f"Arquivo removido: {caminho}")
        elif path_obj.is_dir():
            shutil.rmtree(path_obj)
            print(f"Diretório removido: {caminho}")
    else:
        print(f"Caminho não existe: {caminho}")
```

### Operações de Arquivamento

```python
import shutil
import tempfile

# Criar arquivo compactado
shutil.make_archive('backup', 'zip', 'pasta_para_backup')

# Extrair arquivo
shutil.unpack_archive('backup.zip', 'pasta_destino')

# Formatos suportados
formatos = shutil.get_archive_formats()
print("Formatos de arquivo suportados:", formatos)

# Uso com diretório temporário
with tempfile.TemporaryDirectory() as temp_dir:
    # Criar backup temporário
    backup_path = shutil.make_archive(
        f'{temp_dir}/backup_temp', 'tar', 'dados_importantes'
    )
    print(f"Backup criado: {backup_path}")
    # Será automaticamente removido ao sair do contexto
```

## Pattern Matching com glob

### Padrões Básicos

```python
import glob
from pathlib import Path

# Wildcards básicos
# * - corresponde a qualquer número de caracteres
arquivos_txt = glob.glob('*.txt')
print("Arquivos .txt:", arquivos_txt)

# ? - corresponde a exatamente um caractere
arquivos_numerados = glob.glob('arquivo_?.txt')  # arquivo_1.txt, arquivo_a.txt, etc.

# [] - conjunto de caracteres
logs_numericos = glob.glob('log_[0-9].txt')  # log_1.txt, log_2.txt, etc.
logs_vowel = glob.glob('log_[aeiou].txt')    # log_a.txt, log_e.txt, etc.
```

### Busca Recursiva

```python
import glob

# Busca recursiva com **
todos_python = glob.glob('**/*.py', recursive=True)

# Padrões mais específicos
configs = glob.glob('**/config/*.json', recursive=True)
testes = glob.glob('**/test_*.py', recursive=True)

# Usar glob com pathlib (mais moderno)
from pathlib import Path

projeto = Path('.')
for arquivo_py in projeto.rglob('*.py'):
    print(f"Arquivo Python encontrado: {arquivo_py}")

# Filtros múltiplos
extensoes_imagem = ['*.jpg', '*.png', '*.gif']
imagens = []
for extensao in extensoes_imagem:
    imagens.extend(glob.glob(f'**/{extensao}', recursive=True))
```

### Exemplos Práticos

```python
import glob
import os
from datetime import datetime

def limpar_logs_antigos(diretorio, dias=30):
    """Remove arquivos de log mais antigos que X dias"""
    padrao = os.path.join(diretorio, '*.log')
    agora = datetime.now()
    
    for arquivo in glob.glob(padrao):
        estatisticas = os.stat(arquivo)
        data_modificacao = datetime.fromtimestamp(estatisticas.st_mtime)
        idade = (agora - data_modificacao).days
        
        if idade > dias:
            os.remove(arquivo)
            print(f"Removido log antigo: {arquivo}")

def organizar_por_extensao(diretorio_origem):
    """Organiza arquivos por extensão em subpastas"""
    todos_arquivos = glob.glob(os.path.join(diretorio_origem, '*'))
    
    for arquivo in todos_arquivos:
        if os.path.isfile(arquivo):
            nome, extensao = os.path.splitext(arquivo)
            if extensao:
                # Remover o ponto da extensão
                pasta_extensao = extensao[1:].lower()
                pasta_destino = os.path.join(diretorio_origem, pasta_extensao)
                
                # Criar pasta se não existir
                os.makedirs(pasta_destino, exist_ok=True)
                
                # Mover arquivo
                novo_caminho = os.path.join(pasta_destino, os.path.basename(arquivo))
                os.rename(arquivo, novo_caminho)
                print(f"Movido: {arquivo} -> {novo_caminho}")

# Buscar arquivos por tamanho
def arquivos_grandes(tamanho_mb=100):
    """Encontra arquivos maiores que o tamanho especificado"""
    arquivos_grandes = []
    
    for arquivo in glob.glob('**/*', recursive=True):
        if os.path.isfile(arquivo):
            tamanho = os.path.getsize(arquivo) / (1024 * 1024)  # MB
            if tamanho > tamanho_mb:
                arquivos_grandes.append((arquivo, tamanho))
    
    return sorted(arquivos_grandes, key=lambda x: x[1], reverse=True)
```

## Arquivos Binários

### Leitura e Escrita Básica

```python
# Leitura de arquivo binário
with open('imagem.jpg', 'rb') as f:
    dados_binarios = f.read()
    print(f"Tamanho do arquivo: {len(dados_binarios)} bytes")

# Escrita de arquivo binário
with open('copia_imagem.jpg', 'wb') as f:
    f.write(dados_binarios)

# Leitura em chunks para arquivos grandes
def copiar_arquivo_grande(origem, destino, chunk_size=8192):
    with open(origem, 'rb') as f_origem, open(destino, 'wb') as f_destino:
        while True:
            chunk = f_origem.read(chunk_size)
            if not chunk:
                break
            f_destino.write(chunk)
```

### Trabalhando com Estruturas Binárias

```python
import struct

# Ler header de arquivo BMP
def ler_header_bmp(arquivo_bmp):
    with open(arquivo_bmp, 'rb') as f:
        # Header do arquivo BMP (14 bytes)
        header = f.read(14)
        
        # Desempacotar dados usando struct
        signature = header[:2]
        tamanho_arquivo = struct.unpack('<I', header[2:6])[0]  # Little-endian
        offset_dados = struct.unpack('<I', header[10:14])[0]
        
        return {
            'assinatura': signature,
            'tamanho': tamanho_arquivo,
            'offset_dados': offset_dados
        }

# Serialização com pickle
import pickle

# Salvar objeto Python como binário
dados = {'usuarios': ['Alice', 'Bob'], 'contador': 42}
with open('dados.pkl', 'wb') as f:
    pickle.dump(dados, f)

# Carregar objeto Python de binário
with open('dados.pkl', 'rb') as f:
    dados_carregados = pickle.load(f)
    print(dados_carregados)
```

### Validação de Arquivos Binários

```python
def validar_arquivo_imagem(caminho_arquivo):
    """Valida se arquivo é uma imagem baseado no header"""
    assinaturas = {
        b'\xFF\xD8\xFF': 'JPEG',
        b'\x89PNG\r\n\x1a\n': 'PNG',
        b'GIF87a': 'GIF87a',
        b'GIF89a': 'GIF89a',
        b'BM': 'BMP'
    }
    
    try:
        with open(caminho_arquivo, 'rb') as f:
            header = f.read(10)  # Ler primeiros 10 bytes
            
            for assinatura, tipo in assinaturas.items():
                if header.startswith(assinatura):
                    return tipo
            
            return "Formato não reconhecido"
    
    except Exception as e:
        return f"Erro ao ler arquivo: {e}"

# Exemplo de uso
resultado = validar_arquivo_imagem('foto.jpg')
print(f"Tipo de arquivo: {resultado}")
```

## Trabalhando com CSV

### Usando o Módulo csv

```python
import csv

# Escrita de CSV
dados = [
    ['Nome', 'Idade', 'Cidade'],
    ['Alice', 28, 'São Paulo'],
    ['Bob', 32, 'Rio de Janeiro'],
    ['Charlie', 29, 'Belo Horizonte']
]

with open('pessoas.csv', 'w', newline='', encoding='utf-8') as f:
    writer = csv.writer(f)
    writer.writerows(dados)

# Leitura de CSV
with open('pessoas.csv', 'r', encoding='utf-8') as f:
    reader = csv.reader(f)
    for linha in reader:
        print(linha)

# Usando DictReader e DictWriter
with open('pessoas_dict.csv', 'w', newline='', encoding='utf-8') as f:
    fieldnames = ['nome', 'idade', 'cidade']
    writer = csv.DictWriter(f, fieldnames=fieldnames)
    
    writer.writeheader()
    writer.writerow({'nome': 'Alice', 'idade': 28, 'cidade': 'São Paulo'})
    writer.writerow({'nome': 'Bob', 'idade': 32, 'cidade': 'Rio de Janeiro'})

# Leitura com DictReader
with open('pessoas_dict.csv', 'r', encoding='utf-8') as f:
    reader = csv.DictReader(f)
    for linha in reader:
        print(f"Nome: {linha['nome']}, Idade: {linha['idade']}")
```

### CSV com Pandas

```python
import pandas as pd

# Criar DataFrame
dados = {
    'nome': ['Alice', 'Bob', 'Charlie'],
    'idade': [28, 32, 29],
    'salario': [75000, 82000, 68000]
}
df = pd.DataFrame(dados)

# Salvar CSV
df.to_csv('funcionarios.csv', index=False, encoding='utf-8')

# Ler CSV
df_lido = pd.read_csv('funcionarios.csv', encoding='utf-8')
print(df_lido.head())

# Operações com CSV grande
df_grande = pd.read_csv('arquivo_grande.csv', chunksize=1000)
for chunk in df_grande:
    # Processar chunk por chunk
    resultado = chunk.groupby('categoria').sum()
    print(resultado)
```

### Manipulação Avançada de CSV

```python
import csv
import json

def csv_para_json(arquivo_csv, arquivo_json):
    """Converte CSV para JSON"""
    dados = []
    
    with open(arquivo_csv, 'r', encoding='utf-8') as f:
        reader = csv.DictReader(f)
        for linha in reader:
            dados.append(linha)
    
    with open(arquivo_json, 'w', encoding='utf-8') as f:
        json.dump(dados, f, indent=2, ensure_ascii=False)

def filtrar_csv(arquivo_entrada, arquivo_saida, condicao):
    """Filtra linhas de CSV baseado em condição"""
    with open(arquivo_entrada, 'r', encoding='utf-8') as entrada, \
         open(arquivo_saida, 'w', newline='', encoding='utf-8') as saida:
        
        reader = csv.DictReader(entrada)
        writer = csv.DictWriter(saida, fieldnames=reader.fieldnames)
        
        writer.writeheader()
        for linha in reader:
            if condicao(linha):
                writer.writerow(linha)

# Exemplo de uso do filtro
def idade_maior_que_30(linha):
    return int(linha['idade']) > 30

filtrar_csv('pessoas.csv', 'pessoas_filtradas.csv', idade_maior_que_30)
```

## Manipulação de Arquivos JSON

### Operações Básicas com JSON

```python
import json

# Dados Python para JSON
dados = {
    'usuarios': [
        {'nome': 'Alice', 'idade': 28, 'ativo': True},
        {'nome': 'Bob', 'idade': 32, 'ativo': False}
    ],
    'configuracao': {
        'tema': 'escuro',
        'notificacoes': True
    }
}

# Salvar em arquivo JSON
with open('dados.json', 'w', encoding='utf-8') as f:
    json.dump(dados, f, indent=2, ensure_ascii=False)

# Ler de arquivo JSON
with open('dados.json', 'r', encoding='utf-8') as f:
    dados_carregados = json.load(f)
    print(dados_carregados)

# Conversão de/para string JSON
json_string = json.dumps(dados, indent=2, ensure_ascii=False)
dados_de_string = json.loads(json_string)
```

### Manipulação Avançada de JSON

```python
import json
from pathlib import Path

class ConfiguradorJSON:
    def __init__(self, arquivo_config):
        self.arquivo = Path(arquivo_config)
        self.config = self._carregar_config()
    
    def _carregar_config(self):
        """Carrega configuração do arquivo JSON"""
        if self.arquivo.exists():
            with open(self.arquivo, 'r', encoding='utf-8') as f:
                return json.load(f)
        return {}
    
    def salvar_config(self):
        """Salva configuração no arquivo"""
        with open(self.arquivo, 'w', encoding='utf-8') as f:
            json.dump(self.config, f, indent=2, ensure_ascii=False)
    
    def get(self, chave, padrao=None):
        """Obtém valor da configuração"""
        return self.config.get(chave, padrao)
    
    def set(self, chave, valor):
        """Define valor na configuração"""
        self.config[chave] = valor
        self.salvar_config()
    
    def update(self, novos_dados):
        """Atualiza múltiplas configurações"""
        self.config.update(novos_dados)
        self.salvar_config()

# Uso da classe
config = ConfiguradorJSON('app_config.json')
config.set('tema', 'escuro')
config.set('idioma', 'pt-br')
print(f"Tema atual: {config.get('tema')}")
```

### Validação e Tratamento de Erros JSON

```python
import json
from pathlib import Path

def ler_json_seguro(arquivo):
    """Lê arquivo JSON com tratamento de erros"""
    try:
        with open(arquivo, 'r', encoding='utf-8') as f:
            return json.load(f)
    
    except FileNotFoundError:
        print(f"Arquivo não encontrado: {arquivo}")
        return None
    
    except json.JSONDecodeError as e:
        print(f"Erro ao decodificar JSON: {e}")
        return None
    
    except Exception as e:
        print(f"Erro inesperado: {e}")
        return None

def validar_estrutura_json(dados, estrutura_esperada):
    """Valida se JSON tem a estrutura esperada"""
    try:
        for chave, tipo_esperado in estrutura_esperada.items():
            if chave not in dados:
                return False, f"Chave ausente: {chave}"
            
            if not isinstance(dados[chave], tipo_esperado):
                return False, f"Tipo incorreto para '{chave}': esperado {tipo_esperado.__name__}"
        
        return True, "Estrutura válida"
    
    except Exception as e:
        return False, f"Erro na validação: {e}"

# Exemplo de validação
estrutura = {
    'nome': str,
    'idade': int,
    'ativo': bool
}

dados_usuario = ler_json_seguro('usuario.json')
if dados_usuario:
    valido, mensagem = validar_estrutura_json(dados_usuario, estrutura)
    print(f"Validação: {mensagem}")
```

## Permissões de Arquivos

### Trabalhando com os.chmod()

```python
import os
import stat

# Definir permissões usando constantes do módulo stat
arquivo = 'documento.txt'

# Criar arquivo de exemplo
with open(arquivo, 'w') as f:
    f.write("Conteúdo confidencial")

# Permissões apenas para o proprietário (leitura e escrita)
os.chmod(arquivo, stat.S_IRUSR | stat.S_IWUSR)

# Permissões de leitura para todos
os.chmod(arquivo, stat.S_IRUSR | stat.S_IRGRP | stat.S_IROTH)

# Tornar arquivo executável
os.chmod('script.py', stat.S_IRWXU | stat.S_IRGRP | stat.S_IXGRP | stat.S_IROTH | stat.S_IXOTH)

# Verificar permissões atuais
estatisticas = os.stat(arquivo)
permissoes = stat.filemode(estatisticas.st_mode)
print(f"Permissões de {arquivo}: {permissoes}")
```

### Verificação de Acesso

```python
import os

def verificar_acesso(arquivo):
    """Verifica diferentes tipos de acesso a um arquivo"""
    if not os.path.exists(arquivo):
        return "Arquivo não existe"
    
    acessos = []
    
    if os.access(arquivo, os.R_OK):
        acessos.append("leitura")
    
    if os.access(arquivo, os.W_OK):
        acessos.append("escrita")
    
    if os.access(arquivo, os.X_OK):
        acessos.append("execução")
    
    return f"Acesso disponível: {', '.join(acessos) if acessos else 'nenhum'}"

# Exemplo de uso
print(verificar_acesso('script.py'))
print(verificar_acesso('dados.txt'))
```

### Gerenciamento Seguro de Permissões

```python
import os
import stat
from pathlib import Path

class GerenciadorPermissoes:
    @staticmethod
    def criar_arquivo_seguro(nome_arquivo, conteudo="", permissoes_proprietario_apenas=True):
        """Cria arquivo com permissões seguras"""
        # Criar arquivo
        with open(nome_arquivo, 'w') as f:
            f.write(conteudo)
        
        # Definir permissões
        if permissoes_proprietario_apenas:
            # Apenas proprietário pode ler e escrever
            os.chmod(nome_arquivo, stat.S_IRUSR | stat.S_IWUSR)
        else:
            # Permissões padrão mais abertas
            os.chmod(nome_arquivo, stat.S_IRUSR | stat.S_IWUSR | stat.S_IRGRP | stat.S_IROTH)
    
    @staticmethod
    def criar_diretorio_seguro(nome_diretorio):
        """Cria diretório com permissões seguras"""
        Path(nome_diretorio).mkdir(exist_ok=True)
        # Proprietário: rwx, Grupo: rx, Outros: rx
        os.chmod(nome_diretorio, stat.S_IRWXU | stat.S_IRGRP | stat.S_IXGRP | stat.S_IROTH | stat.S_IXOTH)
    
    @staticmethod
    def backup_com_permissoes(arquivo_origem, arquivo_backup):
        """Faz backup preservando permissões"""
        import shutil
        
        # Copiar arquivo com metadados
        shutil.copy2(arquivo_origem, arquivo_backup)
        
        # Verificar se permissões foram preservadas
        perm_origem = os.stat(arquivo_origem).st_mode
        perm_backup = os.stat(arquivo_backup).st_mode
        
        if perm_origem == perm_backup:
            print("Permissões preservadas no backup")
        else:
            print("Aviso: permissões podem ter sido alteradas")

# Exemplo de uso
GerenciadorPermissoes.criar_arquivo_seguro('config_secreta.txt', 'senha=123456', True)
GerenciadorPermissoes.criar_diretorio_seguro('dados_privados')
GerenciadorPermissoes.backup_com_permissoes('importante.txt', 'backup_importante.txt')
```

## Boas Práticas e Segurança

### Validação de Entrada

```python
import os
import re
from pathlib import Path

def validar_nome_arquivo(nome):
    """Valida nome de arquivo contra caracteres perigosos"""
    # Caracteres proibidos em nomes de arquivo
    caracteres_proibidos = r'[<>:"/\\|?*]'
    
    if re.search(caracteres_proibidos, nome):
        return False, "Nome contém caracteres proibidos"
    
    # Verificar nomes reservados (Windows)
    nomes_reservados = ['CON', 'PRN', 'AUX', 'NUL'] + \
                      [f'COM{i}' for i in range(1, 10)] + \
                      [f'LPT{i}' for i in range(1, 10)]
    
    if nome.upper() in nomes_reservados:
        return False, "Nome é reservado pelo sistema"
    
    return True, "Nome válido"

def caminho_seguro(caminho_base, caminho_usuario):
    """Verifica se caminho está dentro do diretório base (evita directory traversal)"""
    try:
        base = Path(caminho_base).resolve()
        usuario = (Path(caminho_base) / caminho_usuario).resolve()
        
        # Verificar se o caminho do usuário está dentro do base
        usuario.relative_to(base)
        return True, str(usuario)
    
    except ValueError:
        return False, "Caminho fora do diretório permitido"

# Exemplo de uso seguro
def salvar_arquivo_usuario(conteudo, nome_arquivo, diretorio_uploads):
    """Salva arquivo de usuário de forma segura"""
    # Validar nome do arquivo
    valido, mensagem = validar_nome_arquivo(nome_arquivo)
    if not valido:
        raise ValueError(f"Nome de arquivo inválido: {mensagem}")
    
    # Verificar caminho seguro
    seguro, caminho_final = caminho_seguro(diretorio_uploads, nome_arquivo)
    if not seguro:
        raise ValueError("Caminho não permitido")
    
    # Salvar arquivo
    with open(caminho_final, 'w', encoding='utf-8') as f:
        f.write(conteudo)
    
    return caminho_final
```

### Tratamento Robusto de Erros

```python
import os
import logging
from contextlib import contextmanager

# Configurar logging
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

@contextmanager
def arquivo_com_fallback(arquivo_principal, arquivo_backup=None):
    """Context manager que tenta arquivo principal, depois backup"""
    arquivo_usado = None
    
    try:
        # Tentar arquivo principal
        arquivo_usado = open(arquivo_principal, 'r', encoding='utf-8')
        logger.info(f"Usando arquivo principal: {arquivo_principal}")
        yield arquivo_usado
    
    except FileNotFoundError:
        if arquivo_backup and os.path.exists(arquivo_backup):
            try:
                arquivo_usado = open(arquivo_backup, 'r', encoding='utf-8')
                logger.warning(f"Arquivo principal não encontrado, usando backup: {arquivo_backup}")
                yield arquivo_usado
            except Exception as e:
                logger.error(f"Falha ao abrir backup: {e}")
                raise
        else:
            logger.error(f"Arquivo principal e backup não disponíveis")
            raise
    
    finally:
        if arquivo_usado:
            arquivo_usado.close()

def operacao_arquivo_com_retry(funcao, max_tentativas=3, delay=1):
    """Executa operação de arquivo com retry automático"""
    import time
    
    for tentativa in range(max_tentativas):
        try:
            return funcao()
        
        except (IOError, OSError) as e:
            if tentativa < max_tentativas - 1:
                logger.warning(f"Tentativa {tentativa + 1} falhou: {e}. Tentando novamente em {delay}s...")
                time.sleep(delay)
            else:
                logger.error(f"Todas as {max_tentativas} tentativas falharam")
                raise

# Exemplo de uso
def ler_configuracao():
    with arquivo_com_fallback('config.json', 'config_default.json') as f:
        return f.read()

# Usar com retry
config = operacao_arquivo_com_retry(ler_configuracao)
```

### Limpeza de Recursos

```python
import os
import tempfile
import atexit
from pathlib import Path

class GerenciadorRecursos:
    def __init__(self):
        self.arquivos_temporarios = []
        self.diretorios_temporarios = []
        # Registrar limpeza na saída do programa
        atexit.register(self.limpar_todos)
    
    def criar_arquivo_temporario(self, sufixo='.tmp', conteudo=''):
        """Cria arquivo temporário e registra para limpeza"""
        with tempfile.NamedTemporaryFile(mode='w', suffix=sufixo, delete=False) as f:
            f.write(conteudo)
            temp_file = f.name
        
        self.arquivos_temporarios.append(temp_file)
        return temp_file
    
    def criar_diretorio_temporario(self):
        """Cria diretório temporário e registra para limpeza"""
        temp_dir = tempfile.mkdtemp()
        self.diretorios_temporarios.append(temp_dir)
        return temp_dir
    
    def limpar_arquivo(self, arquivo):
        """Remove arquivo específico"""
        try:
            if os.path.exists(arquivo):
                os.remove(arquivo)
                if arquivo in self.arquivos_temporarios:
                    self.arquivos_temporarios.remove(arquivo)
        except Exception as e:
            print(f"Erro ao remover arquivo {arquivo}: {e}")
    
    def limpar_todos(self):
        """Remove todos os recursos temporários"""
        # Remover arquivos
        for arquivo in self.arquivos_temporarios[:]:
            self.limpar_arquivo(arquivo)
        
        # Remover diretórios
        import shutil
        for diretorio in self.diretorios_temporarios[:]:
            try:
                if os.path.exists(diretorio):
                    shutil.rmtree(diretorio)
            except Exception as e:
                print(f"Erro ao remover diretório {diretorio}: {e}")
        
        self.diretorios_temporarios.clear()

# Instância global do gerenciador
gerenciador_recursos = GerenciadorRecursos()

# Exemplo de uso
temp_file = gerenciador_recursos.criar_arquivo_temporario('.txt', 'dados temporários')
temp_dir = gerenciador_recursos.criar_diretorio_temporario()

print(f"Arquivo temporário: {temp_file}")
print(f"Diretório temporário: {temp_dir}")
# Limpeza será automática ao final do programa
```

### Monitoramento de Operações

```python
import os
import time
import hashlib
from functools import wraps

def monitorar_operacao_arquivo(func):
    """Decorator para monitorar operações de arquivo"""
    @wraps(func)
    def wrapper(*args, **kwargs):
        inicio = time.time()
        try:
            resultado = func(*args, **kwargs)
            fim = time.time()
            print(f"{func.__name__} executada com sucesso em {fim - inicio:.2f}s")
            return resultado
        except Exception as e:
            fim = time.time()
            print(f"{func.__name__} falhou após {fim - inicio:.2f}s: {e}")
            raise
    return wrapper

def calcular_hash_arquivo(arquivo, algoritmo='sha256'):
    """Calcula hash de arquivo para verificação de integridade"""
    hash_obj = hashlib.new(algoritmo)
    
    with open(arquivo, 'rb') as f:
        while chunk := f.read(8192):
            hash_obj.update(chunk)
    
    return hash_obj.hexdigest()

@monitorar_operacao_arquivo
def copiar_com_verificacao(origem, destino):
    """Copia arquivo e verifica integridade"""
    import shutil
    
    # Calcular hash do arquivo original
    hash_original = calcular_hash_arquivo(origem)
    
    # Copiar arquivo
    shutil.copy2(origem, destino)
    
    # Verificar integridade da cópia
    hash_copia = calcular_hash_arquivo(destino)
    
    if hash_original != hash_copia:
        os.remove(destino)  # Remover cópia corrompida
        raise ValueError("Cópia corrompida detectada")
    
    print(f"Arquivo copiado e verificado: {origem} -> {destino}")
    return destino

# Exemplo de uso
try:
    arquivo_copiado = copiar_com_verificacao('documento_importante.pdf', 'backup_documento.pdf')
except Exception as e:
    print(f"Falha na cópia: {e}")
```

## Considerações Finais

A manipulação eficiente de arquivos e diretórios em Python requer compreensão das ferramentas disponíveis e aplicação de boas práticas de segurança e gerenciamento de recursos. Este guia fornece uma base sólida para trabalhar com o sistema de arquivos de forma robusta e segura.

### Pontos-Chave para Lembrar

1. **Sempre use context managers** (`with` statement) para garantir fechamento adequado de arquivos
2. **Trate exceções apropriadamente** para lidar com erros de arquivo de forma elegante
3. **Prefira pathlib** para manipulação de caminhos por sua interface mais moderna e intuitiva
4. **Valide entradas de usuário** para prevenir vulnerabilidades de segurança como directory traversal
5. **Monitore permissões de arquivo** especialmente ao trabalhar com dados sensíveis
6. **Use encoding explícito** ao trabalhar com arquivos de texto para evitar problemas de codificação
7. **Implemente limpeza de recursos** para evitar vazamentos de memória e arquivos temporários órfãos

### Próximos Passos

Para aprofundar seus conhecimentos em manipulação de arquivos, considere estudar:

- Programação assíncrona com arquivos usando `aiofiles`
- Monitoramento de alterações em arquivos com `watchdog`
- Compressão e descompressão avançada com `zipfile` e `tarfile`
- Processamento de arquivos grandes com técnicas de streaming
- Integração com serviços de armazenamento em nuvem
- Implementação de sistemas de backup automatizados

A manipulação de arquivos é uma habilidade fundamental que se estende muito além dos conceitos básicos apresentados neste guia. Com prática e aplicação dos princípios aqui discutidos, você será capaz de desenvolver soluções robustas e eficientes para qualquer desafio relacionado ao sistema de arquivos.

---

## Referências

1. Real Python - Python's pathlib Module: Taming the File System
2. GeeksforGeeks - File System Manipulation in Python
3. Python Documentation - pathlib — Object-oriented filesystem paths
4. W3Schools - Python shutil Module
5. Real Python - Python Exceptions: An Introduction
6. GeeksforGeeks - Context Manager in Python
7. TutorialsPoint - File Handling with os Module
8. Python Morsels - Python's pathlib module
9. Real Python - Working With JSON Data in Python
10. GeeksforGeeks - Working With JSON Data in Python
11. Python Documentation - csv — CSV File Reading and Writing
12. Pandas Documentation - pandas.read_csv
13. GeeksforGeeks - Python | os.chmod method
14. Real Python - Python's with Statement: Manage External Resources Safely
15. Python Documentation - glob — Unix style pathname pattern expansion
16. GeeksforGeeks - glob – Filename pattern matching
17. Real Python - shutil | Python Standard Library
18. Python Documentation - shutil — High-level file operations
19. GeeksforGeeks - Create a directory in Python
20. Python Documentation - os — Miscellaneous operating system interface
21. BlackDuck - Six Python Security Best Practices for Developers
22. Qwiet AI - Preventing Directory Traversal Attacks: Best Practices for File Handling
23. IEEE - Python Security in DevOps: Best Practices for Secure Coding
24. Programming Historian - Trabalhando com ficheiros de texto em Python
25. Hub Asimov - Aprenda a manipular diretórios e arquivos em Python
26. FreeCodeCamp - Creating a Directory in Python – How to Create a Folder
27. Accuweb Cloud - How to Read Binary File in Python?
28. Better Stack - Python Pandas: Working with CSV Files
29. Learn Data Sci - Context Managers in Python: Using the "with" statement
30. GitHub MCP Direct - Python file manipulation and directory operations best practices