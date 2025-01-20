# Implantar a infraestrutura do Azure usando modelos JSON do ARM

<br>

Os modelos JSON do ARM (modelos do Azure Resource Manager) permitem especificar a infraestrutura de seu projeto de modo declarativo e reutilizável. 

<br>

## Explorar a estrutura do modelo do Azure Resource Manager

<br>

Você pode usar modelos do ARM para implementar a infraestrutura como código (IaC)

<br>

### O que é a infraestrutura como código?

A infraestrutura como código permite que você descreva, por meio de código, a infraestrutura de que você precisa para seu aplicativo.

Com a infraestrutura como código, você pode manter o código do aplicativo e tudo de que precisa para implantar seu aplicativo em um repositório de código central. As vantagens da infraestrutura como código são:

- Configurações consistentes
- Escalabilidade aprimorada
- Implantações mais rápidas
- Melhor capacidade de rastreamento

<br>

## O que é um modelo ARM?

Os modelos de ARM são arquivos JSON (JavaScript Object Notation) que definem a infraestrutura e a configuração de sua implantação.   
Os modelos de ARM usam uma sintaxe declarativa.

Os modelos do ARM permitem declarar o que você pretende implantar sem a necessidade de escrever a sequência de comandos de programação para criá-lo.

<br>

### Benefícios de usar modelos do ARM

Os modelos de ARM permitem automatizar implantações e usar a prática de IaC. O código do modelo se torna parte de sua infraestrutura e de seus projetos de desenvolvimento. Assim como o código do aplicativo, você pode armazenar os arquivos IaC em um repositório de origem e controlar a versão dele.

Os models do ARM são *idempotentes*, o que significa que você pode implantar o mesmo modelo várias vezes e obter os mesmos tipos de recursos no mesmo estado.

O Resource Manager orquestra a implantação dos recursos para que sejam criados na ordem correta. Quando possível os recursos são criados em paralelo, para que as implantações de modelo do ARM sejam concluídas mais rapidamente do que as implantações com script.

O Resource Manager também tem validação interna. Ele verifica o modelo antes de iniciar a implantação para garantir que seja bem-sucedida.

Caso as implantações se tornem mais complexas, será possível dividir seus modelos do ARM em componentes menores e reutilizáveis. É possível vincular esses modelos menores no momento da implantação. Também é possível aninhar modelos dentro de outros modelos.

No portal do Azure é possível examinar o histórico da implantação e obter informações sobre o estado dela. O portal exibe valores para todos os parâmetros e todas as saídas.

Você também pode integrar seus modelos do ARM a ferramentas de CI/CD (integração contínua e implantação contínua) como Azure Pipelines, o que pode automatizar seus pipelines de lançamento para atualizações rápidas e confiáveis de aplicativos e de infraestrutura. Ao usar as tarefas do Azure DevOps e do modelo do ARM, você pode criar e implantar seus projetos continuamente.

<br>

### Estrutura de arquivos do modelo do ARM

| Elemento | Descrição |
|:--|:--|
| schema | uma seção obrigatória que define a localização do arquivo de esquema JSON que descreva a estrutura de dados JSON. O número de versão usada depende do escopo da implantação e do editor de JSON. |
| contentVersion | uma seção obrigatória que define a versão do modelo (como 1.0.0.0). É possível usar esse valor para documentar alterações significativas no modelo a fim de garantir a implantação do modelo correto |
| apiProfile | seção opcional que define uma coleção de versões de API para tipos de recursos. É possível usar esse valor para evitar a especificação de versões de API para cada recurso no modelo. |
| parameters | uma seção opcional em que você define valores que são fornecidos durante a implantação. Você pode fornecer esses valores em um arquivo de parâmetro, por parâmetros de linha de comando ou no portal do Azure. |
| variables | uma seção opcional em que você define os valores que são usados para simplificar as expressões de linguagem do modelo. |
| functions | uma seção opcional em que é possível definir as funções definidas pelo usuário disponíveis no modelo. As funções definidas pelo usuário podem simplificar o modelo quando expressões complicadas forem usadas repetidamente nele. |
| resources | uma seção obrigatória que define os itens reais que você deseja implantar ou atualizar em um grupo de recursos ou em uma assinatura. |
| output | uma seção opcional em que você especifica os valores retornados no final da implantação. |

<br>

## Implantar um modelo do ARM no Azure

<br>

É possível implantar um modelo do ARM no Azure usando uma das seguintes maneiras:

- Implantar um modelo local
- Implantar um modelo vinculado
- Implantar em um pipeline de implantação contínua

<br>

Para implantar um modelo local, será necessário ter a Azure CLI ou o Azure PowerShell instalado localmente. 

<br>

Primeiro, faça o login: 

Azure CLI
```azurecli
az login
```

<br>

PowerShell
```powershell
Connect-AzAccount
```

<br>

Então defina o Resource Group. É possível criar um Resource Group ou usar um que já esteja definido. Neste exemplo, iremos criar um Resource Group novo


Azure CLI
```azurecli
az group create \
    --name {nome do Resource Group} \
    --location "{location}"

```

<br>

PowerShell
```powershell
New-AzResourceGroup `
    -Name {nome do Resource Group} `
    -Location "{location}"
```

<br>

Para iniciar uma implantação de modelo no Resource Group, use o comando da Azure CLI `az deployment group create` ou o comando do Azure PowerShell `new-AzResourceGroupDeployment`.    
Ambos os comandos exigem o Resource Group, a região e o nome da implantação para que você possa identificá-lo facilmente no histórico de implantação.   
Para maior conveniência, o exercício cria uma variável que armazena o caminho para o arquivo de modelo.  Essa variável facilita a execução dos comandos de implantação porque você não precisa digitar novamente o caminho a cada vez que implantar.   

Veja um exemplo:


Azure CLI
```azurecli
templateFile="{provide-the-path-to-the-template-file}"
az deployment group create \
    --name blanktemplate \
    --resource-group myResourceGroup \
    --template-file $templateFile

```

<br>

PowerShell
```powershell
$templateFile = "{provide-the-path-to-the-template-file}"
New-AzResourceGroupDeployment `
    -Name blanktemplate `
    -ResourceGroupName myResourceGroup `
    -TemplateFile $templateFile
```

<br>

Use modelos vinculados para implantar soluções complexas. É possível dividir um modelo em vários outros e implantá-los por meio de um modelo principal. Quando você implanta o modelo principal, ele dispara a implantação do modelo vinculado. É possível armazenar e proteger o modelo vinculado usando um token SAS.

Um pipeline de CI/CD automatiza a criação e a implantação de projetos de desenvolvimento, inclusive projetos de modelo do ARM. Os pipelines mais comuns usados para a implantação de modelo são o Azure Pipelines ou o GitHub Actions.