## Descomplicando GitHub Actions


- [Descomplicando GitHub Actions](#descomplicando-github-actions)
- [O que esperar desse tutorial?](#o-que-esperar-desse-tutorial)
- [Introdução ao GitHub Actions](#introdução-ao-github-actions)
- [Conceitos Básicos](#conceitos-básicos)
    - [Exemplo de Workflow YAML](#exemplo-de-workflow-yaml)
- [Criando um Workflow Simples](#criando-um-workflow-simples)
- [Eventos que Disparam Workflows](#eventos-que-disparam-workflows)
- [Ações e Repositórios de Ações](#ações-e-repositórios-de-ações)
- [Executores e Ambientes](#executores-e-ambientes)
- [Segredos e Variáveis de Ambiente](#segredos-e-variáveis-de-ambiente)
- [Matrizes e Estratégias de Build](#matrizes-e-estratégias-de-build)
- [Armazenamento em Cache e Artefatos](#armazenamento-em-cache-e-artefatos)
- [Gatilhos Condicionais](#gatilhos-condicionais)
  - [Exemplos de Condições Comuns](#exemplos-de-condições-comuns)
  - [Variáveis de Contexto](#variáveis-de-contexto)
  - [Funções de Contexto](#funções-de-contexto)
  - [Melhorando a Manutenção](#melhorando-a-manutenção)
- [Actions Personalizadas](#actions-personalizadas)
  - [Tipos de Ações Personalizadas](#tipos-de-ações-personalizadas)
  - [Criando uma Ação JavaScript](#criando-uma-ação-javascript)
  - [Benefícios das Ações Personalizadas](#benefícios-das-ações-personalizadas)
  - [Exemplos de Uso](#exemplos-de-uso)
- [Tópicos Avançados](#tópicos-avançados)
  - [Minimizar o tempo de execução](#minimizar-o-tempo-de-execução)
  - [Segurança](#segurança)
  - [Manutenção do código](#manutenção-do-código)
- [Resumo e Próximos Passos](#resumo-e-próximos-passos)
  

## O que esperar desse tutorial?

Neste tutorial, vamos descomplicar o uso do GitHub Actions, uma ferramenta poderosa para automatizar fluxos de trabalho no desenvolvimento de software. Você aprenderá desde os conceitos básicos até tópicos avançados, permitindo que você aproveite ao máximo essa plataforma de CI/CD.

Começaremos com uma Introdução ao GitHub Actions, onde explicaremos o que é essa ferramenta e quais são seus principais benefícios e usos. Em seguida, abordaremos os Conceitos Básicos, incluindo a definição de Workflows, Jobs, e Steps, além da estrutura do arquivo YAML de configuração.

Depois, você aprenderá a Criar um Workflow Simples, conhecendo a estrutura básica de um workflow e vendo um exemplo prático com o famoso "Hello Giropops!". Também exploraremos os Eventos que Disparam Workflows, como push e pull_request, e como configurá-los.

No tópico de Ações e Repositórios de Ações, explicaremos o que são ações e como encontrar e usar ações da GitHub Marketplace. Em seguida, discutiremos os Executores e Ambientes disponíveis, como Ubuntu, Windows, e MacOS, e como configurar ambientes específicos.

Você também aprenderá a usar Segredos e Variáveis de Ambiente para proteger informações sensíveis e definir variáveis de ambiente. Exploraremos o uso de Matrizes e Estratégias de Build para testar múltiplas configurações e otimizar builds paralelos.

Além disso, veremos como utilizar Armazenamento em Cache e Artefatos para acelerar builds e gerenciar artefatos. Também abordaremos Gatilhos Condicionais, mostrando como implementar lógica condicional nos jobs e steps com exemplos práticos.

Por fim, nos Tópicos Avançados, discutiremos a criação de Actions Personalizadas, integração com outros serviços e APIs, e melhores práticas e otimizações para garantir eficiência e manutenção.

Ao final deste tutorial, você estará apto a criar, configurar e otimizar workflows no GitHub Actions, automatizando processos e melhorando a produtividade no desenvolvimento de software.

E o melhor, de um jeito bem descomplicado, como sempre gostamos de fazer!


## Introdução ao GitHub Actions

GitHub Actions é uma poderosa ferramenta de automação de fluxos de trabalho integrada ao GitHub. Ela permite que desenvolvedores automatizem tarefas comuns de desenvolvimento, como integração contínua (CI) e entrega contínua (CD), diretamente em seus repositórios.

Um dos principais benefícios do GitHub Actions é a sua integração nativa com o ecossistema GitHub. Isso significa que ele pode reagir a eventos do GitHub, como pull requests, pushes e issues, permitindo uma automação altamente personalizada e responsiva. A configuração é feita através de arquivos YAML, que são armazenados no repositório, garantindo que o histórico de configurações e mudanças seja versionado junto com o código. Sim eu sei, chega a ser lacrimejante. haha

Além disso, o GitHub Actions oferece uma ampla gama de executores para diferentes sistemas operacionais, incluindo Ubuntu, Windows e macOS. Isso facilita a criação de ambientes de build consistentes e permite testar aplicações em múltiplas plataformas.

A comunidade GitHub também contribui com um vasto repositório de ações pré-construídas, disponíveis no GitHub Marketplace. Essas ações podem ser facilmente integradas aos workflows, economizando tempo e esforço ao reutilizar soluções já testadas e validadas.

Em resumo, GitHub Actions é uma solução flexível e poderosa para automação de fluxos de trabalho, que se beneficia da integração profunda com o GitHub e da vasta gama de ações disponíveis na comunidade, tornando-o uma escolha ideal para desenvolvedores que buscam eficiência e agilidade em seus processos de desenvolvimento.




## Conceitos Básicos

Noções iniciais sobre GitHub Actions são cruciais para entender como configurar e executar automações. Aqui estão os conceitos fundamentais:



* **Workflows** - São definições de automação que descrevem um processo de integração contínua e entrega contínua (CI/CD). Cada workflow é composto por um ou mais jobs e steps.
* **Jobs** - Unidades de trabalho que são executadas em um executor. Cada job pode conter múltiplos steps e é executado de forma isolada. Jobs podem ser configurados para rodar em paralelo ou sequencialmente.
* **Steps** - Comandos individuais que são executados como parte de um job. Steps podem incluir scripts de shell, execução de ações ou comandos de configuração.
* **Arquivo YAML de configuração** - Workflows são definidos em arquivos YAML, que são armazenados no diretório `.github/workflows` do repositório. O formato YAML é utilizado por sua simplicidade e legibilidade.

Isso é o que precisamos entender agora, é importante saber para que serve cada um desses conceito que falamos a pouco. Vamos ver isso na prática, acho que é melhor para entender. 


#### Exemplo de Workflow YAML


```yaml
name: Giropops CI

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout no Repo
      uses: actions/checkout@v4

    - name: Run a one-line script
      run: echo Hello Giropops!

    - name: Run a multi-line script
      run: |
        echo Exemplo de mais um step,
        echo Giropops Strigus Girus.
```


Neste exemplo, temos um workflow chamado "CI" que é disparado por eventos de push e pull_request. O job `build` roda em um executor `ubuntu-latest` e contém três steps:



1. **Checkout code** - Usa a ação `actions/checkout@v4` para fazer o checkout do código do repositório.
2. **Run a one-line script** - Executa um comando simples de shell que imprime "Hello, world!".
3. **Run a multi-line script** - Executa múltiplos comandos de shell que imprimem mensagens.

Compreender esses conceitos básicos e a estrutura de um arquivo YAML é o primeiro passo para criar automações eficazes com GitHub Actions.


## Criando um Workflow Simples

Para criar um workflow simples no GitHub Actions, começamos definindo um arquivo de configuração no formato YAML. Este arquivo deve ser colocado no diretório `.github/workflows` do seu repositório. Vamos criar um exemplo básico de workflow que imprime "Hello Giropops!" quando um commit é feito no branch principal, simples como voar. :)

Primeiro, crie o arquivo `.github/workflows/hello-world.yml` no seu repositório. O conteúdo do arquivo será o seguinte:


```yaml
name: Workflow do Giropops

on: [push]

jobs:
  say_hello:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v4

    - name: Run a one-line script
      run: echo "Hello Giropops!"
```


Vamos detalhar cada seção do arquivo:



* **<code>name</code></strong>: Define o nome do workflow. Este é um campo opcional, mas ajuda a identificar o workflow na interface do GitHub.
* <code>on</code>: Especifica os eventos que disparam o workflow. No nosso exemplo, o workflow será disparado sempre que houver um <code>push</code> no repositório.
* <strong><code>jobs</code></strong>: Define um conjunto de tarefas que serão executadas. Cada job pode ter múltiplos <code>steps</code>.
* <strong><code>runs-on</code></strong>: Especifica o ambiente onde o job será executado. Aqui, estamos usando <code>ubuntu-latest</code> para indicar que o job deve rodar em uma máquina virtual com o Ubuntu.
* <strong><code>steps</code></strong>: Lista as etapas que compõem o job. Cada etapa pode utilizar uma ação ou executar comandos diretamente.

No exemplo acima, temos duas etapas:



1. **<code>Checkout repository</code></strong>: Utiliza a ação <code>actions/checkout@v4</code> para fazer o checkout do código do repositório.
2. <strong><code>Run a one-line script</code></strong>: Executa um comando simples que imprime "Hello Giropops!" no console.

Depois de adicionar e commitar este arquivo ao seu repositório, o GitHub Actions automaticamente detectará e executará o workflow quando um <code>push</code> for feito. Você pode verificar a execução do workflow na aba "Actions" do seu repositório no GitHub.

Este exemplo básico serve como ponto de partida. A partir daqui, você pode adicionar mais etapas, utilizar diferentes ações, e configurar workflows mais complexos para atender às necessidades do seu projeto.


## Eventos que Disparam Workflows

Os eventos que disparam workflows são fundamentais para a automação no GitHub Actions. Eles determinam quando um workflow deve ser executado, com base em ações específicas no repositório ou em eventos externos.

Um dos eventos mais comuns é o push. Este evento é disparado sempre que há um push para o repositório. Pode ser configurado para responder a pushes em branches específicos, tags ou até mesmo para ignorar certos padrões.

Outro evento amplamente utilizado é o pull_request (eu gosto muito). Este evento é acionado quando um pull request é aberto, sincronizado, reaberto ou fechado. É útil para executar testes e validações automáticas antes de mesclar mudanças no branch principal.

Além desses, existem muitos outros eventos que podem ser utilizados, como:



* **schedule** - Permite agendar a execução de workflows em intervalos regulares usando a sintaxe cron.
* **release** - Disparado quando uma nova release é publicada ou atualizada.
* **workflow_dispatch** - Permite que workflows sejam acionados manualmente através da interface do GitHub.

Cada evento pode ser configurado detalhadamente no arquivo YAML do workflow. Por exemplo, para configurar um workflow que é disparado em um evento de push para o branch `main`, a configuração seria algo assim:


```yaml
name: CI

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout no Repo
        uses: actions/checkout@v4
      # Adicione outros steps aqui
```


Além disso, os eventos podem ser combinados para criar fluxos de trabalho mais complexos. Por exemplo, um workflow pode ser configurado para ser executado tanto em um push para o branch `main` quanto em um pull request:


```yaml
name: CI

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout no Repo
        uses: actions/checkout@v4
      # Adicione outros steps aqui
```


A flexibilidade dos eventos permite a criação de pipelines de CI/CD altamente personalizados, que podem ser ajustados para atender às necessidades específicas de cada projeto.


## Ações e Repositórios de Ações

As ações são a unidade baásica de execução dentro de um workflow do GitHub Actions. Elas permitem que você automatize tarefas específicas, como executar testes, implantar código, ou realizar verificações de segurança. Existem ações pré-construídas disponíveis no GitHub Marketplace, que podem ser facilmente integradas ao seu workflow.

Ações são definidas em arquivos YAML e podem ser reutilizadas em diferentes workflows. Elas podem ser escritas em JavaScript ou como contêineres Docker, permitindo flexibilidade na escolha da tecnologia e ambiente de execução. Aqui está um exemplo básico de como usar uma ação do GitHub Marketplace:


```yaml
name: Exemplo maroto de Workflow

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout no Repo
      uses: actions/checkout@v4

    - name: Run a one-line script
      run: echo "Giropops Strigus Girus!"

    - name: Usando uma Action pre-built
      uses: actions/setup-node@v2
      with:
        node-version: '14'
```


No exemplo acima, a ação `actions/setup-node@v2` é usada para configurar o ambiente Node.js. O campo `with` permite passar parâmetros para a ação, como a versão do Node.js a ser usada.

Você também pode criar suas próprias ações personalizadas para atender necessidades específicas do seu projeto. Para isso, é necessário definir um repositório de ações, que contém o código e a configuração necessários para a ação. Um exemplo de estrutura de repositório de ação em JavaScript pode ser:

my-action/

├── action.yml

├── index.js

└── package.json

No arquivo `action.yml`, você define os metadados da ação, como nome, descrição, entradas e saídas. Aqui está um exemplo básico de `action.yml`:


```yaml
name: 'My Custom Action'
description: 'An example custom action'
inputs:
  myInput:
    description: 'An example input'
    required: true
    default: 'default value'
runs:
  using: 'node12'
  main: 'index.js'
```


O arquivo `index.js` conterá a lógica da sua ação. Por exemplo:


```yaml
const core = require('@actions/core');

try {
  const myInput = core.getInput('myInput');
  console.log(`My input is ${myInput}`);
} catch (error) {
  core.setFailed(error.message);
}
```


Depois de criar e testar sua ação, você pode publicá-la no GitHub Marketplace para que outros desenvolvedores possam usá-la. Isso envolve marcar uma versão do repositório e criar uma release.

Ao utilizar ações e repositórios de ações, você pode modularizar e compartilhar automações, melhorando a eficiência e a consistência dos seus workflows.


## Executores e Ambientes

Os executores são as máquinas virtuais que executam os jobs definidos nos workflows. GitHub Actions oferece diferentes tipos de executores, cada um adequado para diferentes necessidades de desenvolvimento e teste.



* Ubuntu - Ideal para a maioria dos projetos devido à sua popularidade e suporte a diversas ferramentas de desenvolvimento. As versões disponíveis incluem Ubuntu 18.04 e 20.04.
* Windows - Adequado para projetos que dependem de ferramentas específicas do Windows ou para testar software em um ambiente Windows. As versões disponíveis incluem Windows Server 2019.
* macOS - Necessário para projetos que requerem um ambiente macOS, como desenvolvimento de aplicativos iOS. As versões disponíveis incluem macOS Catalina e Big Sur.

Para escolher um executor, você define a chave `runs-on` no arquivo YAML do workflow. Por exemplo, para usar um executor Ubuntu, você pode escrever:


```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout no Repo
        uses: actions/checkout@v4
```


Além dos executores padrão, é possível configurar self-hosted runners, que são máquinas gerenciadas pelo próprio usuário. Isso oferece maior controle sobre o ambiente de execução e pode ser útil para projetos que requerem hardware específico ou software que não está disponível nos executores hospedados pelo GitHub.

Para configurar um self-hosted runner, você deve:



1. Registrar o runner no repositório ou organização.
2. Instalar o software do runner na máquina.
3. Configurar o runner para conectar-se ao GitHub e executar jobs.

Os ambientes de execução também podem ser personalizados através da instalação de dependências adicionais ou configuração de variáveis de ambiente específicas. Por exemplo, se você precisar instalar uma versão específica do Node.js, pode adicionar um step no workflow:


```yaml
steps:
  - name: Set up Node.js
    uses: actions/setup-node@v2
    with:
      node-version: '14'
```


Para definir variáveis de ambiente, utilize a chave `env`:


```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    env:
      NODE_ENV: production
    steps:
      - name: Checkout no Repo
        uses: actions/checkout@v4
```


Esses recursos permitem criar ambientes de build altamente configuráveis e adaptados às necessidades específicas do projeto, garantindo que os testes e builds sejam executados de forma consistente e eficiente.


## Segredos e Variáveis de Ambiente

Os segredos são utilizados para armazenar informações sensíveis, como chaves de API, tokens de acesso e senhas, que não devem ser expostas no código-fonte. Para adicionar um segredo em um repositório, você pode acessar a aba "Settings" do repositório, selecionar "Secrets" e adicionar um novo segredo com um nome e valor correspondente.

As variáveis de ambiente são úteis para configurar o comportamento de jobs e steps sem hardcoding valores no arquivo YAML. Você pode definir variáveis de ambiente no nível de workflow, job ou step. Aqui está um exemplo básico de como definir e usar variáveis de ambiente:


```yaml
name: Example Workflow

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    env:
      GLOBAL_VAR: "Essa é uma variável global"

    steps:
    - name: Checkout no Repo
      uses: actions/checkout@v4

    - name: Printando a variável
      run: echo ${{ env.GLOBAL_VAR }}

    - name: Definindo a variável no nível do job
      run: |
        JOB_VAR="Giropops no job-level!"
        echo "JOB_VAR=$JOB_VAR" >> $GITHUB_ENV

    - name: Printando a variável no nível do job
      run: echo ${{ env.JOB_VAR }}

    - name: Definindo uma variável no nível do step
      run: |
        STEP_VAR="Giropops no step-level"
        echo "STEP_VAR=$STEP_VAR" >> $GITHUB_ENV

    - name: Printando a variável no nível do step
      run: echo ${{ env.STEP_VAR }}
```


No exemplo acima, `GLOBAL_VAR` é uma variável global disponível para todos os steps dentro do job. `JOB_VAR` é definida em um step e adicionada ao ambiente do job usando `echo "VAR_NAME=VALUE" >> $GITHUB_ENV`, tornando-a disponível para steps subsequentes. `STEP_VAR` é uma variável definida e usada dentro do mesmo step.

Para acessar segredos, você pode referenciá-los utilizando a sintaxe `${{ secrets.SECRET_NAME }}`. Por exemplo:


```yaml
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout no Repo
      uses: actions/checkout@v4

    - name: Use a secret
      run: echo "O Secret é o ${{ secrets.MY_SECRET }}"
```


Neste exemplo, `MY_SECRET` é um segredo previamente adicionado ao repositório. Ele será substituído pelo valor do segredo durante a execução do workflow. Magicamente! :D

Utilizar segredos e variáveis de ambiente de maneira eficaz ajuda a manter a segurança e a flexibilidade dos workflows no GitHub Actions.


## Matrizes e Estratégias de Build

A utilização de matrizes permite que você teste diferentes combinações de variáveis em seus workflows. Isso é extremamente útil para garantir que seu código funcione em várias configurações. Por exemplo, você pode testar seu projeto em diferentes versões de um runtime, como Node.js, ou em diferentes sistemas operacionais.

Para definir uma matriz, você especifica uma lista de variáveis e suas possíveis combinações no arquivo YAML. Aqui está um exemplo básico:


```yaml
name: Node.js CI

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [12, 14, 16]
    steps:
    - uses: actions/checkout@v4
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v2
      with:
        node-version: ${{ matrix.node-version }}
    - run: npm install
    - run: npm test
```


Neste exemplo, o job "build" será executado três vezes, uma para cada versão do Node.js especificada na matriz. Isso garante que seu projeto seja testado em todas essas versões, ajudando a identificar problemas de compatibilidade.

Além das matrizes, as estratégias de build permitem definir como e quando os jobs devem ser executados. Você pode configurar a execução paralela de jobs para otimizar o tempo de build, ou definir dependências entre jobs para garantir que um job só execute após a conclusão de outro.

Aqui está um exemplo de configuração de estratégia de build com dependências:


```yaml
name: CI Pipeline

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Build
      run: make build

  test:
    runs-on: ubuntu-latest
    needs: build
    steps:
    - uses: actions/checkout@v4
    - name: Executando testes
      run: make test

  deploy:
    runs-on: ubuntu-latest
    needs: test
    steps:
    - uses: actions/checkout@v4
    - name: Deploy
      run: make deploy
```


Neste exemplo, vamos imaginar comigo que o job "test" só será executado após a conclusão do job "build", e o job "deploy" só será executado após a conclusão do job "test". Isso cria uma pipeline de CI/CD organizada e eficiente.

Utilizar matrizes e estratégias de build de maneira eficaz pode melhorar significativamente a qualidade e a eficiência do seu processo de desenvolvimento, garantindo que seu código seja robusto e compatível com diferentes ambientes e configurações.


## Armazenamento em Cache e Artefatos

O armazenamento em cache e o uso de artefatos são técnicas essenciais para otimizar e gerenciar a eficiência dos workflows no GitHub Actions. Utilizar cache pode reduzir significativamente o tempo de execução ao evitar a repetição de tarefas que consomem muito tempo, como a instalação de dependências.

Para implementar o cache, você pode usar a ação `actions/cache`. Aqui está um exemplo de como configurar o cache para dependências do Node.js:


```yaml
name: Cache Example

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
    - name: Cache Node.js modules
      uses: actions/cache@v2
      with:
        path: ~/.npm
        key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
        restore-keys: |
          ${{ runner.os }}-node-
    - run: npm install
    - run: npm test
```


Neste exemplo, a ação `actions/cache` armazena os módulos Node.js em `~/.npm`, utilizando o arquivo `package-lock.json` para gerar uma chave única. Se o cache existir, ele será restaurado, economizando tempo ao evitar a reinstalação das dependências.

Já os artefatos são usados para armazenar e compartilhar arquivos gerados durante a execução dos workflows. Por exemplo, você pode querer salvar logs, resultados de testes ou builds para referência futura. A ação `actions/upload-artifact` permite fazer isso facilmente:


```yaml
name: Artifact Example

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
    - name: Build project
      run: npm run build
    - name: Upload build artifacts
      uses: actions/upload-artifact@v2
      with:
        name: build-artifacts
        path: build/
```


Neste exemplo, após a execução do comando de build, os arquivos gerados na pasta `build/` são carregados como artefatos com o nome `build-artifacts`. Esses artefatos podem ser baixados posteriormente na aba "Actions" do repositório no GitHub.

Utilizar cache e artefatos de maneira eficiente pode melhorar significativamente a performance e a gestão dos workflows, garantindo que processos repetitivos sejam otimizados e que os resultados importantes sejam armazenados e acessíveis quando necessário.


## Gatilhos Condicionais

Os gatilhos condicionais permitem que você controle a execução de jobs e steps em um workflow do GitHub Actions com base em determinadas condições. Eles são especialmente úteis para evitar a execução desnecessária de tarefas, economizando tempo e recursos.

Para utilizar gatilhos condicionais, você pode adicionar a diretiva `if` em qualquer nível de jobs ou steps dentro do seu arquivo YAML de configuração. A sintaxe básica para utilizar `if` é a seguinte:


```yaml
jobs:
  example_job:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout no Repo
        uses: actions/checkout@v4

      - name: Executando testes
        if: ${{ github.event_name == 'push' }}
        run: npm test
```


No exemplo acima, o step "Run tests" só será executado se o evento que disparou o workflow for um `push`.


### Exemplos de Condições Comuns



1. **Verificar o evento que disparou o workflow:**


```yaml
if: ${{ github.event_name == 'pull_request' }}
```


Este step será executado apenas se o evento for um pull_request.



2. **Verificar a branch:**


```yaml
if: ${{ github.ref == 'refs/heads/main' }}
```


Este step será executado apenas se o workflow estiver rodando na branch main.



3. **Verificar o status de um job anterior:**


```yaml
if: ${{ success() }}
```


Este step será executado apenas se todos os jobs anteriores tiverem sido bem-sucedidos.



4. **Combinações de condições:**


```yaml
if: ${{ github.event_name == 'push' && github.ref == 'refs/heads/main' }}
```


Este step será executado apenas se o evento for um push e a branch for main.


### Variáveis de Contexto

Você pode utilizar várias variáveis de contexto para construir suas condições:



* `github`: Contém informações sobre o repositório, evento, e contexto de execução.
* `runner`: Informações sobre o executor que está rodando o workflow.
* `env`: Variáveis de ambiente definidas no workflow.

Por exemplo:


```yaml
if: ${{ runner.os == 'Linux' && env.MY_VAR == 'true' }}
```



### Funções de Contexto

GitHub Actions também fornece funções que podem ser usadas dentro de condições:



* `success()`: Retorna `true` se todos os jobs anteriores foram bem-sucedidos.
* `failure()`: Retorna `true` se qualquer job anterior falhou.
* `always()`: Sempre retorna `true`, útil para steps que devem rodar independentemente do resultado anterior.


```yaml
if: ${{ always() }}
```



### Melhorando a Manutenção

Para manter seu workflow limpo e fácil de manter, você pode definir condições complexas como variáveis no início do arquivo YAML e referenciá-las nos seus steps.


```yaml
env:
  RUN_TESTS: ${{ github.event_name == 'push' && github.ref == 'refs/heads/main' }}

jobs:
  example_job:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout no Repo
        uses: actions/checkout@v4

      - name: Executando testes
        if: ${{ env.RUN_TESTS }}
        run: npm test
```


Assim, você pode facilmente ajustar a lógica condicional sem precisar modificar múltiplos steps.

Os gatilhos condicionais são uma ferramenta poderosa para otimizar e controlar a execução dos seus workflows, garantindo que apenas as tarefas necessárias sejam executadas sob as condições apropriadas.


## Actions Personalizadas

Uma das funcionalidades mais poderosas do <span style="text-decoration:underline;">GitHub Actions</span> é a capacidade de criar <span style="text-decoration:underline;">Actions Personalizadas</span>. Essas ações permitem que você encapsule e reutilize lógica específica que pode ser compartilhada entre diferentes workflows e projetos.


### Tipos de Ações Personalizadas

Existem três tipos principais de ações personalizadas que você pode criar:



* **<span style="text-decoration:underline;">Ações Docker</span>** - Executadas dentro de um contêiner Docker, permitindo um ambiente controlado e consistente. Isso é útil quando você precisa de dependências específicas ou um ambiente de execução isolado.
* **<span style="text-decoration:underline;">Ações JavaScript</span>** - Executadas diretamente no executor, sem a necessidade de um contêiner. São rápidas e ideais para tarefas que podem ser realizadas com bibliotecas disponíveis no Node.js.
* **<span style="text-decoration:underline;">Ações Composites</span>** - Permitem combinar múltiplos comandos e outras ações em uma única ação. São úteis para agrupar lógica complexa em uma única unidade reutilizável.


### Criando uma Ação JavaScript

Para criar uma ação JavaScript:



1. **Estrutura do Projeto:**
    * Crie um repositório ou uma pasta para a ação.
    * Adicione um arquivo `action.yml` na raiz do projeto.
2. **Definindo a Ação:**
    * No `action.yml`, defina os metadados da ação, incluindo o nome, descrição, entradas e saídas.


```yaml
name: 'Hello World Action'
description: 'Uma simples ação de exemplo'
inputs:
  who-to-greet:
    description: 'A quem cumprimentar'
    required: true
    default: 'World'
runs:
  using: 'node12'
  main: 'index.js'

```

3. Implementação em JavaScript:
    * Crie um arquivo `index.js` para implementar a lógica da ação.


```js
const core = require('@actions/core');

try {
  const nameToGreet = core.getInput('who-to-greet');
  console.log(`Hello ${nameToGreet}!`);
  const time = (new Date()).toTimeString();
  core.setOutput('time', time);
} catch (error) {
  core.setFailed(error.message);
}

```

4. Publicação e Uso:
    * Commit e push do código para o repositório.
    * Utilize a ação em um workflow referenciando o repositório.


```yaml
jobs:
  example-job:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      - name: Run custom action
        uses: username/repository@v1
        with:
          who-to-greet: 'GitHub Actions'
```

### Benefícios das Ações Personalizadas



* **Reutilização**: Encapsular lógica comum em ações facilita a reutilização em múltiplos workflows.
* **Compartilhamento**: Publicar ações no <span style="text-decoration:underline;">GitHub Marketplace</span> permite que outros desenvolvedores as utilizem.
* **Manutenção**: Centralizar lógica em ações facilita a manutenção e atualização do código.


### Exemplos de Uso



* **CI/CD Pipelines**: Automatizar testes, builds e deploys.
* **Automação de Tarefas**: Scripts de automação para tarefas repetitivas, como formatação de código ou verificação de segurança.
* **Integrações**: Conectar workflows com serviços externos via APIs.

Criar e utilizar ações personalizadas amplia significativamente as capacidades de automação no GitHub, permitindo que você adapte os workflows às necessidades específicas do seu projeto.

## Tópicos Avançados

No tópico de Actions Personalizadas, abordamos como criar suas próprias ações para reutilizar código e facilitar a automação de tarefas específicas. Isso envolve escrever scripts em JavaScript ou criar contêineres Docker que podem ser executados como parte de um workflow.

A integrar ações personalizadas com outros serviços e APIs é uma habilidade valiosa. Por exemplo, você pode configurar uma ação para enviar notificações para um canal do Slack ou atualizar um banco de dados sempre que um novo código for mesclado no repositório.

Melhores práticas e otimizações são cruciais para garantir que seus workflows sejam eficientes e seguros. Isso inclui:


* **Minimizar o tempo de execução**- Utilize cache e paralelismo para reduzir o tempo de execução dos jobs.
* **Segurança** - Proteja segredos e evite expor informações sensíveis.
* **Manutenção do código** - Organize e documente seus workflows para facilitar a manutenção.

Além disso, a utilização de gatilhos condicionais permite executar jobs apenas quando certas condições são atendidas, economizando recursos e tempo. Por exemplo, você pode configurar um job para rodar apenas se uma determinada pasta no repositório for modificada.

Finalmente, a análise de logs e a depuração são partes essenciais do desenvolvimento de workflows complexos. Ferramentas como a visualização de logs de execução e a configuração de mensagens de erro detalhadas ajudam a identificar e corrigir problemas rapidamente.

Esses tópicos avançados permitem que você aproveite ao máximo o potencial do GitHub Actions, criando pipelines de CI/CD eficientes e personalizados para suas necessidades específicas.


### Minimizar o tempo de execução

Para minimizar o tempo de execução dos seus workflows, é fundamental utilizar técnicas que otimizem o desempenho e reduzam o tempo ocioso. Uma das abordagens mais eficazes é o uso de cache para armazenar dependências e artefatos que não mudam frequentemente. Isso evita a necessidade de baixar ou compilar novamente esses recursos em cada execução.

Outra técnica importante é a paralelização de jobs. Ao dividir o workflow em múltiplos jobs que podem ser executados simultaneamente, você aproveita melhor os recursos disponíveis e reduz o tempo total de execução. Por exemplo, se você tem testes que podem ser executados independentemente, configure-os para rodar em paralelo.

Além disso, é essencial otimizar os scripts e comandos utilizados dentro dos jobs. Certifique-se de que cada comando seja necessário e elimine qualquer redundância. Utilize ferramentas de análise de desempenho para identificar gargalos e ajustar conforme necessário.

A escolha do ambiente de execução também pode impactar significativamente o tempo de execução. Optar por máquinas mais rápidas ou ajustar a configuração dos runners pode trazer melhorias notáveis. Em alguns casos, você pode considerar o uso de runners autohospedados, que podem ser configurados com hardware específico para atender melhor às necessidades do seu workflow.

Finalmente, a configuração de gatilhos condicionais pode ser usada para evitar a execução desnecessária de jobs. Por exemplo, você pode configurar um job para rodar apenas quando arquivos específicos forem modificados, evitando assim a execução de testes ou builds desnecessários.

Essas práticas, quando combinadas, podem resultar em uma redução significativa no tempo de execução dos seus workflows, aumentando a eficiência e a produtividade do seu processo de desenvolvimento.


### Segurança

Ao abordar a segurança em workflows de automação, é essencial considerar a proteção de segredos e a prevenção de vulnerabilidades. Uma prática comum é utilizar Secretos no GitHub Actions para armazenar informações sensíveis como tokens de API, credenciais de banco de dados e chaves privadas. Esses segredos são criptografados e só podem ser acessados pelos workflows do repositório.

Além disso, é importante restringir o acesso a quem pode modificar os workflows. Apenas colaboradores confiáveis devem ter permissões para editar arquivos de configuração, evitando assim a introdução de código malicioso. Utilizar branch protection rules pode ajudar a garantir que mudanças nos workflows passem por revisões de código antes de serem mescladas.

Outra consideração é a execução de ações de terceiros. Sempre que possível, utilize ações verificadas e de fontes confiáveis. Revise o código-fonte das ações que você incorpora em seus workflows para garantir que não há comportamentos inesperados ou maliciosos. A execução de ações de terceiros em um ambiente isolado, como em contêineres Docker, pode adicionar uma camada extra de segurança.

Monitorar e auditar logs de execução também é crucial. Logs detalhados permitem identificar atividades suspeitas e responder rapidamente a incidentes de segurança. Configurar alertas para atividades incomuns pode ajudar a detectar e mitigar ameaças em tempo real.

Finalmente, manter os componentes do seu ambiente de CI/CD atualizados é vital. Isso inclui manter o software de automação, bibliotecas e dependências sempre nas versões mais recentes, que geralmente contêm correções de segurança importantes. A adoção de uma abordagem proativa na gestão de vulnerabilidades ajuda a proteger seus workflows contra ameaças emergentes.


### Manutenção do código

Manter o código de workflows organizado e bem documentado é essencial para garantir a longevidade e a facilidade de manutenção dos projetos. Uma prática recomendada é utilizar comentários detalhados dentro dos arquivos de configuração YAML para explicar a finalidade de cada etapa e os parâmetros utilizados. Isso ajuda outros desenvolvedores a entender rapidamente o que cada parte do workflow faz.

Além disso, dividir workflows complexos em arquivos menores e mais gerenciáveis pode facilitar a manutenção. Por exemplo, você pode criar workflows separados para build, testes e deploy, e depois chamar esses workflows menores a partir de um workflow principal. Isso permite que cada parte do processo seja desenvolvida e depurada independentemente.

A reutilização de ações também é uma prática recomendada. Em vez de duplicar código, você pode criar ações personalizadas ou utilizar ações da comunidade que já estão disponíveis no GitHub Marketplace. Isso não só reduz a quantidade de código que você precisa manter, mas também aproveita soluções que já foram testadas e validadas por outros desenvolvedores.

Versionamento é outro aspecto crucial. Manter um histórico claro de mudanças nos arquivos de workflow e utilizar tags ou releases para marcar versões estáveis pode ajudar a rastrear alterações e reverter para versões anteriores, se necessário. Isso é particularmente útil em ambientes de produção onde a estabilidade é crítica.

Finalmente, a automação de testes para os próprios workflows pode ser implementada. Por exemplo, você pode configurar um workflow que testa mudanças em outros workflows em um ambiente de staging antes de implementá-las em produção. Isso garante que quaisquer alterações nos workflows não introduzam novos problemas.

Essas práticas de manutenção ajudam a garantir que seus workflows sejam robustos, eficientes e fáceis de atualizar, facilitando a colaboração e a continuidade do projeto.


## Resumo e Próximos Passos

Durante este tutorial, exploramos desde os conceitos básicos até tópicos avançados. Começamos com uma introdução ao GitHub Actions, entendendo seus benefícios e usos. Aprendemos sobre a estrutura de workflows, jobs e steps, além da configuração de arquivos YAML. Criamos um workflow simples e exploramos os diferentes eventos que podem disparar esses workflows, como push e pull_request.

Também discutimos como utilizar ações disponíveis no GitHub Marketplace e como configurar diferentes executores e ambientes. A importância de proteger informações sensíveis com segredos e o uso de variáveis de ambiente foram outros pontos abordados. Além disso, exploramos como utilizar matrizes para testar múltiplas configurações e estratégias de build paralelas, e como acelerar builds com cache e gerenciar artefatos.

Com gatilhos condicionais, aprendemos a usar lógica condicional nos jobs e steps, aumentando a flexibilidade dos workflows. Nos tópicos avançados, discutimos a criação de actions personalizadas, integração com outros serviços e APIs, e melhores práticas para otimização.

Para continuar aprimorando suas habilidades, recomendamos:

* **Explorar a Documentação Oficial**: A documentação do GitHub Actions é uma fonte rica de informações e exemplos práticos.
* **Participar da Comunidade**: Engajar-se com a comunidade de desenvolvedores no GitHub e em fóruns pode fornecer insights valiosos e soluções para problemas comuns.
* **Experimentar com Projetos Reais**: Aplicar o conhecimento adquirido em projetos reais ajudará a solidificar sua compreensão e a descobrir novos desafios e soluções.
* **Acompanhar Atualizações e Novidades**: O GitHub Actions está em constante evolução. Manter-se atualizado com as últimas funcionalidades e melhorias pode trazer benefícios significativos.

Com essas recomendações, você estará bem preparado para utilizar o GitHub Actions de maneira eficiente e eficaz em seus projetos, aproveitando ao máximo todas as suas funcionalidades.

Inclusive agora você já tem o conhecimento necessário para espalhar a palavra! Compartilhe o seu conhecimento com mais pessoas, crie um artigo, um treinamento, uma bate-papo, sei lá! Mas compartilhe! :)
