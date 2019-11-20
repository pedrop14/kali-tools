# Trabalho Kali - Binwalk e Magic Rescue
> Autor: Pedro Henrique Amado

# Binwalk
[Binwalk](https://github.com/ReFirmLabs/binwalk) é uma ferramenta open-source feita para realizar buscas em imagens. Entretanto, é uma ferramenta muito poderosa e também é utilizada para análises forenses, sendo muitas vezes utilizada por profissionais juntamente com um editor de Hexadecimal. Ela possibilita a busca em qualquer tipo de arquivo por meio de uma lista de assinaturas conhecida com `Magic Numbers`. Nesse tutorial vamos utilizar a ferramenta para extrair arquivos de dentro de um PDF.

### Instalação
```sh
# Caso esteja utilizando o Python 2.x, instale a dependência:
$ sudo apt install python-lzma ou sudo yum install pyliblzma

$ git clone https://github.com/ReFirmLabs/binwalk.git
$ cd binwalk
$ sudo python setup.py install
```

### Uso
O Binwalk pode ser usado sempre passando as opções da funcionalidade desejada e o arquivo (ou arquivos) para serem aplicados.
```sh
$ binwalk [opções] [arquivo]
```

### Funcionalidades
- Filtragem
    - A Filtragem é uma funcionalidade que permite a inclusão ou exclusão de qualquer tipo de arquivo no momento de execução de outra funcionalidade.
    Ex: `$ binwalk --include image exemplo.raw`
- Comparação de Arquivos
    - A Comparação de arquivos é utilizada para comparação hexadecimal e encontrar similaridades no bytes. As similaridades vão de tipo e formato do arquivo até conteúdos específicos.
    Ex: `$ binwalk -W arquivo01.mp3 arquivo02.mp3`
- Pesquisa RAW
    - A pesquisa consiste em buscar por arquivos ou fragmentos específicos em outros arquivos.
    Ex: `$ binwalk -R "Roberto Carlos" musica03.mp3`
- Extração de Arquivos
    - A extração possibilita a extração de arquivos de dentro do outros. É semelhante à uma desfragmentação que permite o acesso e armazenamento das partes extraídas.
    Ex: `$ binwalk -e ExerciciosDeSegurança.pdf`
    Essa opção `-e` já cria um diretório e armazena os arquivos extraídos.
- LOG
    - Essa funcionalidade permite o armazenamento de `logs` de alterações em arquivos, fazendo assim a escuta e armazenamento.
    Ex: `$ binwalk -f saída_dos_dados.log ExerciciosDeSegurança.pdf`

# Magic Rescue
O Magic Rescue é uma ferramenta que possibilita a recuperação de arquivos em mídias removíveis. Ele se assemelha à uma outra ferramenta chamada foremost. A funcionalidade básica é recuperar um arquivo que foi deletado e não sobrescrito.

### Instalação
```sh
$ sudo apt-get install magicrescue
```

### Uso
```sh
$ magicrescue -h

Usage: magicrescue [-I FILE] [-M MODE] [-O [+-=][0x]OFFSET] [-b BLOCKSIZE]
	-d OUTPUT_DIR -r RECIPE1 [-r RECIPE2 [...]] DEVICE1 [DEVICE2 [...]]

  -b  Only consider files starting at a multiple of BLOCKSIZE.
  -d  Mandatory.  Output directory for found files.
  -r  Mandatory.  Recipe name, file or directory.
  -I  Read input file names from this file ("-" for stdin)
  -M  Produce machine-readable output to stdout.
  -O  Resume from specified offset (hex or decimal) in the first device.
```

### Funcionalidade
A principal funcionalidade é a recuperação de arquivos e ele permite recuperar arquivos com extensões variadas, como:

- avi
- elf
- gpl
- jpeg-exif
- mbox
- mbox-mozilla-sent
- mp3-id3v2
- nikon-raw
- png
- sqlite
- canon-cr2
- flac
- gzip
- jpeg-jfif
- mbox-mozilla-inbox
- mp3-id3v1
- msoffice
- perl
- ppm
- zip

Comando de execução:
```sh
# Criar pasta para salvar as imagens
$ mkdir jpeg
$ magicrescue -r jpeg-exif -r jpeg-jfif -d /jpeg /dev/sdb1
```
Ao final do processamento, todos os arquivos restaurados serão salvos na pasta `/jpeg`
