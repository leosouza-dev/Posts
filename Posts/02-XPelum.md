# Criando Registro e Login de Usuários de uma forma Segura

Ao ligarmos nosso computador, acessarmos nosso email ou tentar entrar em nossa conta do banco notamos algo em comum - A necessidade de autenticação.

Hoje em dia, ao navegarmos pelos sites e sistemas percebos que é algo muito comum as telas de Registro e Login de usuários. Ou seja, é algo rotineiro para o desenvolvimento de sistemas.

Pensando assim, supondo que somos desenvolvedores de software focado em .NET, e surgiu um novo trabalho ou uma nova demanda que é a criação de um sistema que precisa ter Autenticação, como faremos essa Autenticação?

Muitas vezes pode surgir a ideia de criarmos nossa Feature de Registro e Login na "mão". Ou seja, nós mesmos implementarmos criarmos todo o fluxo de registro e login de um usuário.

Mas será se essa seria a melhor escolha? 

---

Como vimos, Autenticação de Usuario é um probelma recorrente na vida de Desenvolvedores. Quando temos situações assim, alguem provavelmente já desenvolveu algo para facilitar as nossas vidas.

Claro que criar uma Autenticação do zero não está errado, mas será muito trabalhoso e poderá existir brechas de segurança. Não que as soluções prontas não possuem brechas, mas são anos de maturidade, melhorando o código e tornando-se cada vez mais seguras, além da facilidade e velocida de serem implementadas nas aplicações.

Agora que decidimos que não iremos escrever a nossa Feature na mão (espero que tenha dado algums motivações haha), qual solução pronta iremos usar em nossa aplicação ASP.NET Core?

## ASP.NET Core Identity

Um framework muito utilizado pela comunidade .NET para autenticação é o ASP.NET Core Identity, ou simplemente Identity.

Além de ser uma solução segura pronta para podermos utilizarmos para termos nossas telas de Registro, Login, erros, etc, o Identity nos traz muitas facilidades como o envio de email para confirmação de registro, registro usando OAuth para usuarios poderem se conectarem por provedores externos (Facebook, Twitter, Google e Microsoft), entre outras que falaremos a adiante.

Mas nada melhor para aprender e entender melhor do que usar o Identity...

## Criando Projeto com o Identity

Esse projeto está sendo criado com .NET Core, ASP.NET Core 2.2 e usando o Visual Studio 2019.

O Template do projeto é ASP.NET Core Web Application (MVC). Já iniciei o projeto com Autenticação usando o Identity.

![Create a New Project](imagens/02-xpelum/novo-projeto-01.png)

---

Ao Clicarmos em "Create a new Project" vamos para a seguinte tela, onde devemos selecionar "ASP.NET Core Web Applications e clicar em "next":

![ASP.NET Core Web Applications](imagens/02-xpelum/novo-projeto-02.png)

---

Nessa tela é onde definimos o Nome do nosso projeto, nome da Solução e o diretório onde será salvo. Clicamos em create para prosseguir:

![Nome e Diretório](imagens/02-xpelum/novo-projeto-03.png)

---

Na tela seguinte selecionamos o Template da aplicação, se terá Autorização, qual a versão do ASP.NET iremos utilizar. Primeiro Selecionamos que será ASP.NET Core 2.2 e o template - (MVC).

![Nome e Diretório](imagens/02-xpelum/novo-projeto-04.png)

---

Ainda na mesma tela vamos mudar a opção de autenticação. Ao clicarmos em "change" abrirá aba mostrando as opções. Selecione "Individual user Account" clique em OK. Após isso clique em Create para gerar o novo projeto.

![Template](imagens/02-xpelum/novo-projeto-05.png)

---

Após essa configuração inicial, nosso projeto está criado:

![Template](imagens/02-xpelum/novo-projeto-06.png)

---

## Rodando o Projeto com o Identity

Ao executarmos o projeto, teremos a seguinte tela inicial:

![Rodando aplicação - tela inicial](imagens/02-xpelum/rodando-aplicacao-01.png)

Note que no menu de Navegação temos os links para "Home", "Privacy", "Register" e "Login". Sendo que esses dois últimos foram criados pelo "Identity".

---

Clicando no Link "Register" seremos redirecionados para seguinte tela:

![Rodando aplicação - tela de registro](imagens/02-xpelum/rodando-aplicacao-02.png)

E clicando no Link "Login" seremos redirecionados para seguinte tela:

![Rodando aplicação - tela de Login](imagens/02-xpelum/rodando-aplicacao-03.png)

---

Note que não foi necessário criar nenhuma tela de Login e Registro para termos a Feature pronta. Isso nos auxilia muito tanto na velocidade de desenvolvimento como manutenção, pois é um Framework pronto que os Desenvolvedores .NET estão acostumados e familiarizados. Além de ser uma biblioteca com maturidade e segura.

Depois de darmos uma passada rápida na execução do Aplicação, vamos ver o que foi criado no nosso projeto. Focaremos no Identity.

## Conhecendo o Projeto com o Identity

Ao criarmos um projeto com o Identity é possivel observar a criação de algumas pastas na arvore do projeto: "Areas" e "Data".

Dentro da pasta "Areas" temos uma pasta "Identity", que possue uma pasta "Pages", que por sua vez possue um arquivo "_ViewStart.cshtml".

Na pasta "Data" possuimos um arquivo "ApplicationDbContext.cs" que é o Contexto para a persistencia de dados com o Banco de Dados e uma pasta "Migration" com uma migration inicial para criação das tabelas.

![Conhecendo aplicação - Arvore do Projeto](imagens/02-xpelum/conhecendo-aplicacao-01.png)

A classe "ApplicationDbContext.cs" é bem simples. Ela herda de "IdentityDbContext" e possue um construtor passando o DbContextOptions (configurações) para a classe base. 

![Conhecendo aplicação - ApplicationDbContext](imagens/02-xpelum/conhecendo-aplicacao-02.png)

Os outros arquivos - "_ViewStart" apenas aponta para usar o Layout padrão do projeto e as migrations possuem um esquema de criação do Banco de Dados com as tabelas necessárias para o Iedntity.

---

