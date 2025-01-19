# Introdução a Bash

<br>

## O que é Bash?

<br>

O Bash é uma ferramenta vital para o gerenciamento de computadores Linux. O nome é o acrônimo de "Bourne Again Shell".

Um shell é um programa que faz o comando executar ações no sistema operacional. Você pode inserir comandos em um console no computador e executá-los diretamente, ou pode usar scripts para executar lotes de comandos. Os shells como o PowerShell e o Bash dão aos administradores de sistema o poder e a precisão necessários para o controle preciso dos computadores pelos quais eles são responsáveis.

Há outros shells do Linux, incluindo csh e zsh, mas o Bash se tornou o padrão Linux de fato. Isso porque o Bash é compatível com o primeiro shell sério do UNIX, o shell Bourne, também conhecido como sh. 

<br>

## Conceitos básicos do Bash

<br>

A sintaxe completa de um comando Bash é:

```bash
command [options] [arguments]
```

<br>

O Bash trata a primeira cadeia de caracteres que encontra como um comando. O comando `ls`, sem opções e argumentos, exibe o conteúdo do diretório de trabalho atual

```bash
ls
```

<br>

O comando `ls` acompanhado de argumento para listar o conteúdo de outro diretório
```bash
ls /etc
```

<br>

As opções, também chamadas de *flags*, fornecem a um comando instruções mais específicas. Podemos usar a flag `-a` para mostrar todos os arquivos de um diretório, incluindo os ocultos

```bash
ls -a /etc
```

<br>

A flag `-a` acompanhada da flag `-l` para mostrar todos os arquivos de um diretório, incluindo os ocultos, em formato "longo"

```bash
ls -al /etc
```

<br>

## Obter ajuda

<br>

Verificar o manual do comando `mkdir`

```bash
man mkdir
```

<br>

Obter ajuda do comando `mkdir`

```bash
mkdir --help
```

<br>

## Use curingas

<br>

Curingas são símbolos que representam um ou mais caracteres em comandos Bash.  
O curinga usado com mais frequência é o asterisco (`*`). Ele representa zero caractere ou uma sequência de caracteres. 

Listar somente os arquivos do diretório atual que terminam com `.png`

```bash
ls *.png
```

<br>


Listar somente os arquivos do diretório atual que terminam com `.png`

```bash
ls *.png
```

<br>

Listar arquivos do diretório atual que terminam com `.jpg` e outros que terminam com `.jpeg`

```bash
ls *.jpg *.jpeg
```

<br>

Outra forma de fazer isso

```bash
ls *.jp*g
```

<br>

O curinga `?` representa um único caractere.

Listar todos os arquivos do diretório atual nomeados como `0001.jpg`, `0002.jpg` e assim por diante até ``00009.jpg`

```bash
ls 000?.jpg
```
Neste exemplo, se houver um arquivo chamado `000a.jpg` ele também será listado. Um arquivo chamado `0011.jpg` não seria listado.

<br>

Outra maneira de usar curingas para filtrar a saída é usar colchetes, que denotam grupos de caracteres.

Listar todos os arquivos do diretório atual cujos os nomes contêm um ponto imediatamente seguido por `j` ou `p`.

```bash
ls *.[jp]*
```
Neste exemplo, serão listados os arquivos `.jpg`, `.jpeg` mas não arquivos `.gif`.

<br>

Listar todos os arquivos do diretório atual cujos nomes contenham pontos seguidos por um J ou P maiúsculo ou minúsculo,

```bash
ls *.[jpJP]*
```

<br>

Listar todos os arquivos do diretório atual cujos nomes começam com letra minúscula

```bash
ls [a-z]*
```

<br>

Listar todos os arquivos do diretório atual cujos nomes começam com letra maiúscula

```bash
ls [A-Z]*
```

<br>

Listar todos os arquivos do diretório atual cujos nomes começam com letra minúscula ou maiúscula

```bash
ls [a-zA-Z]*
```

<br>

Se você precisar usar um dos caracteres curinga como um caractere comum, torne-o literal ou "escape-o" usando uma barra invertida como sufixo.

Listar todos os arquivos do diretório atual que possuem um asterisco com parte do nome

```bash
ls *\**
```

<br>

## Comandos e operados Bash

<br>

Cada linguagem de shell tem seus comandos mais usados. Vamos começar criando seu repertório Bash examinando os comandos mais usados.

<br>

### Comando `ls`

`ls` lista o conteúdo do seu diretório atual ou o diretório especificado em um argumento para o comando

```bash
ls 
```

<br>

Listar todos os arquivos de um diretório, incluindo os ocultos

```bash
ls -a /etc
```

<br>

Listar todos os arquivos de um diretório em formato "longo"

```bash
ls -l /etc
```
O formato longo oferece uma saída detalhada sobre arquivos ou diretórios correspondentes.

<br>

Exemplo da saída do comando

```
-rw-rw-r-- 1 azureuser azureuser  473774 Jun 13 15:38 0001.png
-rw-rw-r-- 1 azureuser azureuser 1557965 Jun 13 14:43 0002.jpg
-rw-rw-r-- 1 azureuser azureuser  473774 Mar 26 09:21 0003.png
-rw-rw-r-- 1 azureuser azureuser 4193680 Jun 13 09:40 0004.jpg
-rw-rw-r-- 1 azureuser azureuser  423325 Jun 10 12:53 0005.jpg
-rw-rw-r-- 1 azureuser azureuser 2278001 Jun 12 04:21 0006.jpg
-rw-rw-r-- 1 azureuser azureuser 1220517 Jun 13 14:44 0007.jpg
drwxrwxr-x 2 azureuser azureuser    4096 Jun 13 20:16 gifs
```

<br>

### Comando `cat`

O comando `cat` concatena arquivos de texto e os exibe na saída padrão do Bash. Pode ser usado para exibir o conteúdo de arquivos de texto.

Exibir o conteúdo do arquivo `/etc/os-release`

```bash
cat /etc/os-release
```

<br>

### Comando `sudo`

Executa comandos com o privilégio de administrador.

Exibir o conteúdo do arquivo `/etc/at.deny` com privilégio de administrador

```bash
sudo cat /etc/at.deny
```
Sem usar o `sudo` o conteúdo do arquivo não seria exibido.

<br>

### Comandos `cd`, `mkdir` e `rmdir`

O comando `cd` permite que você se mova de um diretório para outro.

Mudar para um subdiretório chamado `orders`

```bash
cd orders
```

<br>

Mover para um diretório acima

```bash
cd ..
```

<br>

Mudar para o diretório base, que é aquele em que você chega ao se conectar pela primeira vez:

```bash
cd ~
```

<br>

Com o comando `mkdir` você pode criar diretórios

Criar um subdiretório chamado `orders` no diretório atual

```bash
mkdir orders 
```

<br>

Criar um subdiretório e outro subdiretório sob ele

```bash
mkdir --parents orders/2019
```
A flag `--parents` pode ser substituída pela flag `-p`. O resultado será o mesmo.

<br>

O comando `rmdir` removerá um diretório vazio.

Remover o diretório `orders` que está vazio

```bash
rmdir orders
```
Para remover um diretório não vazio use o comando `rm`.

<br>

### Comando `rm`

O comando `rm` exclui arquivos.

Remover o arquivo `0001.jpg`

```bash
rm 0001.jpg
```

<br>

Excluir todos os arquivos no diretório atual

```bash
rm *
```

<br>

Exibir um aviso ao excluir um arquivo

```bash
rm -i *
```

<br>

Excluir o subdiretório `orders` que não está vazio

```bash
rm -r orders
```
Este comando exclui o subdiretório `orders` e tudo que nele contém, inclusive outros subdiretórios.

<br>

### Comando `cp`

O comando `cp` pode copiar arquivos e diretório inteiros.

Copiar o arquivo `0001.jpg` e chamá-lo de `0002.jpg`

```bash
cp 0001.jpg 0002.jpg
```
Se o arquivo `0002.jpg` já existir ele será substituído sem aviso prévio.

<br>

Copiar o arquivo `0001.jpg` e chamá-lo de `0002.jpg` e emitir um aviso caso o arquivo `0002.jpg` já exista

```bash
cp -i 0001.jpg 0002.jpg
```

<br>

Copiar todos os arquivos de um diretório atual para um subdiretório chamado `photos`

```bash
cp * photos
```

<br>

Copiar todos os arquivos de um subdiretório chamado `photos` para um subdiretório chamado `images`

```bash
cp photos/* images
```

<br>

Copiar todos os arquivos e subdiretórios do subdiretório chamado `photos` para o diretório chamado `images`

```bash
cp -r photos /images
```
A flag `-r` indica que a cópia deve ser recursiva, ou seja, todos os arquivos, subdiretórios e o conteúdo desses subdiretórios devem ser copiados.

<br>

### Comando `ps`

O comando `ps` exibe um instantâneo dos processos que estão em execução no momento. O comando `ps` sem argumentos exibe os processos do shell.

Listar todos os processos em execução além dos processos do shell

```bash
ps -e
```

<br>

Listar todos os processos em execução, seus PIDs, os PPIDs, quando eles começaram (STIME), entre outras informações

```bash
ps -ef
```
A saída do comando `ps aux` é idêntica à saída do comando `ps -ef`.

<br>

### Comando `w`

Exibe as informações sobre os usuários que estão conectados e suas atividades.

```bash
w
```

<br>

## Operadores de E/S de Bash

<br>

No Bash, os comandos podem ser combinados com operadores de E/S:

- `<`: direcionar a entrada para uma fonte que não o teclado
- `>`: direcionar a saída para um destino que não a tela 
- `>>`: direcionar a saída para um destino que não a tela, mas acrescentando, em vez de substituir
- `|`: canalizar a saída de um comando para a entrada de outro

<br>

Enviar a saída de um comando para um arquivo chamado listing.txt

```bash
ls > listing.txt
```
Se o arquivo já existir ele será substituído.

<br>

Enviar a saída de um comando para um arquivo chamado listing.txt inserindo a saída no final do arquivo sem substituí-lo

```bash
ls >> listing.txt
```
Se o arquivo já existir ele será substituído.

<br>

O `|` Redirecionar a saída de um comando para outro comando.

Redirecionar a saída do comando `ps -ef` para o comando `head` para visualizar apenas a primeiras linhas

```bash
ps -ef | head
```

<br>

Filtrar a saída do comando `ps -ef` para que mostre apenas a linhas que contenham a palavra `daemon`

```bash
ps -ef | grep daemon
```

<br>

Usar o operador `<` para classificar o texto do arquivo `file.txt` em ordem alfabética

```bash
sort < file.txt
```

<br>

Usar o operador `<` para classificar o texto do arquivo `file.txt` em ordem alfabética e salvar os dados classificados no arquivo `sorted_file.txt`

```bash
sort < file.txt > sorted_file.txt 
```

<br>

Listar os tamanhos de VM disponíveis na região `westus` 

```bash
az vm list-sizes --location westus --output table
```

<br>

Listar os tamanhos de VM disponíveis na região `westus` que contenham de "DS"

```bash
az vm list-sizes --location westus --output table | grep DS
```

<br>

Listar os tamanhos de VM disponíveis na região `westus` que contenham de "DS V2"

```bash
az vm list-sizes --location westus --output table | grep DS.*_v2
```

<br>

## Saiba mais
[MS Learn: Introduction to Bash](https://learn.microsoft.com/en-us/training/modules/bash-introduction/)   