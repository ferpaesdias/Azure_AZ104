# Introdução ao PowerShell

<br>

O PowerShell, é um shell de linha de comando multiplataforma e uma linguagem de script criada para automação de tarefas e gerenciamento de configuração.   
O PowerShell consiste em duas partes: um shell de linha de comando e uma linguagem de script. Ele começou como uma estrutura para automatizar tarefas administrativas no Windows. O PowerShell cresceu e se tornou uma ferramenta multiplataforma que é usada para muitos tipos de tarefas.

<br>

## Recursos

<br>

O PowerShell compartilha alguns recursos com shells tradicionais:

- **Sistema de ajuda interno**: O sistema de ajuda do PowerShell fornece informações sobre comandos e se integra a artigos de ajuda online.
- **Pipeline**: Shells tradicionais usam um pipeline para executar muitos comandos sequencialmente. O PowerShell implementa esse conceito como shells tradicionais, mais é diferente deles porque opera em objetas por texto.
- **Aliases**: Aliases são nomes alternativos que podem ser usados para executar comandos.

<br>

O PowerShell é diferente de um shell de linha de comando tradicional de algumas maneiras:

- **Opera em objetos por texto**: No PowerShell você usa objetos como entrada e saída. Isso significa que você gasta menos tempo na formatação e na extração.
- **Tem cmdlets**:  Os comandos no PowerShell são chamados de cmdlets (pronunciados como commandlets). Ao contrário de muitos outros ambientes de shell, no PowerShell, os cmdlets são criados em um runtime comum em vez de executáveis separados. Essa característica fornece uma experiência consistente na análise de parâmetros e no comportamento do pipeline. Normalmente, os cmdlets usam a entrada do objeto e retornam objetos. Os cmdlets básicos do PowerShell foram criados no .NET Core e são software livre. Você pode estender o PowerShell usando mais cmdlets, scripts e funções da comunidade e de outras fontes, ou pode criar seus próprios cmdlets no .NET Core ou no PowerShell.
- **Tem muitos tipos de comandos**: Os comandos do PowerShell podem ser executáveis, cmdlets, funções, scripts ou aliases nativos. Cada comando executado pertence a um desses tipos. As palavras comando e cmdlet geralmente são usadas de modo intercambiável, porque um cmdlet é um tipo de comando.

<br>

## Comandos

<br>

### Verificar a instalação do PowerShell

```powershell
$PSVersionTable
```

<br>

Verificar a instalação do PowerShell e restringir a saída a somente a sua versão

```powershell
$PSVersionTable.PSVersion
```
A execução de `$PSVersionTable` resulta em uma saída que se parece com uma tabela, mas é, na verdade, um objeto. Por esse motivo, você pode usar um ponto final (`.`) para acessar uma propriedade específica, como `PSVersion`.

<br>

### Localizar comandos

Um cmdlet (pronuncia-se "command-let") é um comando compilado. Os cmdlets são nomeados de acordo com um padrão de nomenclatura de verbo-substantivo. 

<br>

Listar os verbos aprovados para cmdlets
```powershell
Get-Verb
```

<br>

Três cmdlets principais permitem que você se aprofunde nos cmdlets existentes e no que eles fazem:

- `Get-Command`: Listar todos os cmdlets disponíveis no sistema.
- `Get-Help`: Invocar um sistema de ajuda interno.
- `Get-Member`: Fazer uma busca detalhada das propriedades de um objeto.

<br>

### Localizar comandos usando o `Get-Command`

Ao executar o cmdlet Get-Command no Cloud Shell, você obtém uma lista de todos os comandos instalados no PowerShell.  Como milhares de comandos são instalados, você precisa encontrar uma forma de filtrar a resposta para localizar rapidamente o comando de que precisa.   
Use flags para obter o verbo ou o substantivo no comando desejado. O sinalizador especificado espera um valor que seja uma cadeia de caracteres.

<br>

Exemplos de como usar flags para filtrar uma lista de comandos:

- `-Noun`: Obtém a parte do nome do comando que está relacionado ao substantivo. Pesquisa de um nome de comando usando `alias` como o substantivo.

```powershell
Get-Command -Noun alias*
```

<br>

- `-Verb`: Obtém a parte do nome do comando que está relacionado ao verbo. A combinação da flag `-Noun` e da flag `-Verb`
permite criar uma consulta de pesquisa e um tipo ainda mais detalhado.
```powershell
Get-Command -Verb Get -Noun alias*
```
A pesquisa para especificar que a parte do verbo precisa corresponder a `Get` e a parte do substantivo precisa corresponder a `alias`.

<br>

## Saiba mais
[MS Learn: Introduction to PowerShell](https://learn.microsoft.com/en-us/training/modules/introduction-to-powershell/)   