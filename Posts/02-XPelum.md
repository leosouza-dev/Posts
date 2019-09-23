# Criando Registro e Login de Usuários de uma forma Segura

Ao ligarmos nosso computador, acessarmos nosso email ou tentarmos entrar em nossa conta do banco notamos algo em comum - A necessidade de autenticação.

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


Note que não foi necessário criar nenhuma tela de Login e Registro para termos a Feature pronta. Isso nos auxilia muito tanto na velocidade de desenvolvimento como manutenção, pois é um Framework pronto que os Desenvolvedores .NET estão acostumados e familiarizados. Além de ser uma biblioteca com maturidade e segura.

Depois de darmos uma passada rápida na execução do Aplicação, vamos ver o que foi criado no nosso projeto. Focaremos no Identity.

---

## Conhecendo o Projeto com o Identity

### Arquivos novos

Ao criarmos um projeto com o Identity é possivel observar a criação de algumas pastas na arvore do projeto: "Areas" e "Data".

Dentro da pasta "Areas" temos uma pasta "Identity", que possue uma pasta "Pages", que por sua vez possue um arquivo "_ViewStart.cshtml".

Na pasta "Data" possuimos um arquivo "ApplicationDbContext.cs" que é o Contexto para a persistencia de dados com o Banco de Dados e uma pasta "Migration" com uma migration inicial para criação das tabelas.

![Conhecendo aplicação - Arvore do Projeto](imagens/02-xpelum/conhecendo-aplicacao-01.png)

A classe "ApplicationDbContext.cs" é bem simples. Ela herda de "IdentityDbContext" e possue um construtor passando o DbContextOptions (configurações) para a classe base. 

![Conhecendo aplicação - ApplicationDbContext](imagens/02-xpelum/conhecendo-aplicacao-02.png)

Os outros arquivos - "_ViewStart" apenas aponta para usar o Layout padrão do projeto e as migrations possuem um esquema de criação do Banco de Dados com as tabelas necessárias para o Iedntity.

---

### Appsettings.json e Startup.cs

Além dessas pastas e arquivos criados, o identity alterou alguns outros arquivos:

- No arquivo de configuração "appsettings.json" ele criou a ConnectionStrings padrão.

- Na classe "Startup.cs" no método "ConfigureServices" é adicionado o DbContext apontando para a ConnectionString e adicionado o iedntity. Já no metodo "Configure" é adicionado a Autenticação.

Arquivo appsettings.json:

![Conhecendo aplicação - appsettings](imagens/02-xpelum/conhecendo-aplicacao-03.png)

Arquivo Startup.cs, método "ConfigureServices":

![Conhecendo aplicação - ConfigureServices](imagens/02-xpelum/conhecendo-aplicacao-04.png)

Arquivo Startup.cs, método "Configure":

![Conhecendo aplicação - ConfigureServices](imagens/02-xpelum/conhecendo-aplicacao-05.png)

---

### Partial View

Além de todas essas alterações, o Identity utiliza uma Partial View para exibir no menu de navegação os links de "Register" e "login".

Esse arquivo é possivel ser localizado dentro do diretório "Views/Shared/_LoginPartial.cshtml".

![Conhecendo aplicação - _LoginPartial_diretório](imagens/02-xpelum/conhecendo-aplicacao-06.png)

![Conhecendo aplicação - _LoginPartial](imagens/02-xpelum/conhecendo-aplicacao-07.png)

Essa Partial View utiliza o Identity (SignInManager e UserManager) realizando uma lógica verificando se o usuário está logado ou não.

 Caso não esteja, será mostrado os Links de "Register" e "link". Após o Usuário logar-se, no lugar dos links anteriores, será exibido o nome do usuário e um link para "Logout".

- Menu de navegação sem o usuário de autenticar:
![Conhecendo aplicação - Menu sem autenticação](imagens/02-xpelum/conhecendo-aplicacao-08.png)

- Menu de navegação com o usuário autenticado:
![Conhecendo aplicação - Menu autenticado](imagens/02-xpelum/conhecendo-aplicacao-09.png)

Um ponto importante que temos que mencionar é onde essa "_LoginPartial" está sendo referenciada.

Ela é chamada na Partial view de Layout - "_Layout.cshtml", dentro da Tag "Nav". Ela encontra-se dentro de "Views/Shared".

![Conhecendo aplicação - _Layout](imagens/02-xpelum/conhecendo-aplicacao-10.png)

---

### Banco de Dados

Como falamos anteriormente, o ASP.NET Core Identity cria uma Migration inicial para a criação das tabelas padrões.
Ao executarmos o comando "update-database" será criado o banco de dados com as tabelas necessárias.

![Conhecendo aplicação - BD](imagens/02-xpelum/conhecendo-aplicacao-11.png)

Existem várias tabelas no Banco de Dados criado a partir do Identity, mas por hora vamos focar na tabela "AspNetUsers". Nela que é persistido os nossos usuários.

![Conhecendo aplicação - AspNetUsers](imagens/02-xpelum/conhecendo-aplicacao-12.png)

Existem diversas colunas e tabelas criadas por padrão pelo Identity, que muitas vezes não são utilizadas por uma aplicação mais simples. Mais para frente iremos falar como Customizar o Identity.

---

## Facilidades com o Identity

### Autenticação

Nossa aplicação, do jeito que está agora, possue todas as Views (Home e Privacy) "abertas" para todos acessarem, inclusive por usuários não autenticados.

Supondo que surgiu uma nova demanda - A view Privacy será aberta apenas por usuários autenticados.

Com o Identity, a implementação dessa Feature é muito simples. basta irmos na HomeController e incluirmos uma anotação [Authorize] sobre a action "Privacy".

![Mudando a aplicação - Authorize](imagens/02-xpelum/alterando-aplicacao-01.png)

Apenas com a inclusão dessa linha de código, quando um usuário não autenticado clicar no link "Privacy" será redirecionado para a View de Login. Um usuário autenticado possue acesso a essa View.

---

### Autorização

- Tá legal, mas e se for necessários termos grupos/funções de Usuários - Ex. Admin e User?

Para trabalharmos com grupos/funções de usuários podemos usar as "Roles".

Agora nossa nova demanda é que para o Usuário conseguir acessar a View Privacy, ele precisa ser "Admin" no sistema.

Para entendermos melhor os próximos passos, vamos olhar as tabelas do nosso Banco de Dados.

Na tabela "AspNetUser" é onde estão localizados nossos usuários. Atualmente temos dois usuários registrados: "leonardo.89@uol.com.br" e "ze@gmail.com".

![Banco de Dados - User](imagens/02-xpelum/bd-roles-01.png)

Na tabela "AspNetRoles" é onde estão as nossas Roles. Atualmente apenas com uma: "Admin".

![Banco de Dados - Roles](imagens/02-xpelum/bd-roles-02.png)

E na tabela "AspNetUserRoles" é onde fazemos a associação de usuários com as suas respectivas Roles (pode ser mais de uma). Atualmente temos uma associação do usuário "leonardo.89@uol.com.br" com a Rode "Admin" através de seus Id's.

![Banco de Dados - User-Roles](imagens/02-xpelum/bd-roles-03.png)

Na nossa action "Privacy" preciamos informar que elá terá acesso apenas para usuários autenticados e com a Role Admin. Para isso basta acrescentarmos na anotação a Role desejada.

![Mudando a aplicação - Autenicação com role](imagens/02-xpelum/alterando-aplicacao-02.png)

E por fim, mas não menos importante, devemos adicionar o middleware na classe startup, no método "ConfigureServices"

![Mudando a aplicação - Adicionando com role](imagens/02-xpelum/alterando-aplicacao-03.png)

---

Ao executarmos a aplicação e o usuário "ze@gmail.com" estiver logado e tentar acessar a View Privacy, ele será redirecionado para uma tela de "Acesso Negado", pois ele não possui a Role "Admin".

![Rodando Aplicação - Acesso Negado](imagens/02-xpelum/rodando-aplicacao-04.png)

Já o usuário "leonardo.89@uol.com.br" terá total acesso a View Privacy por ter a Role "Admin".

![Rodando Aplicação - Privacy](imagens/02-xpelum/rodando-aplicacao-05.png)

---

## Cadê as Views do Identity?

A partir do ASP.NET Core 2.1 as telas do Identity são do tipo "Razor Class Libraries". Ou seja, diferentemente das versões anteriores, não são criados as models e views no projeto.

- Então minhas telas não poderão ser traduzidas ou alteradas?

É possivel sim customizar as telas padrões do Identity.

Falaremos agora como adicionar o código-fonte das Razor Class Libraries para conseguirmos modifica-las.

---

### Importado as Razor Class Libraries

Para conseguirmos ter acesso às paginas criadas pelo Identity, temos que realizar um Scaffold.

Clicando com o botão direito do mouse sobre o projeto, selecionamos a opção "Add" > "New Scaffolded Item".

![New scaffolded item](imagens/02-xpelum/new-scaffolded-item.png)

Ao clicarmos em "New Scaffolded Item" uma nova janela irá se abrir. Devemos selecionar a opção "Identity", que está localizada no lado esquerdo da Aba, e clicar no botão "Add".

![New scaffolded item](imagens/02-xpelum/new-scaffolded-item-02.png)

Quando clicamos no botão "Add" outra janela irá se abrir (pode demorar um pouco). Nessa janela é onde selecionamos as telas que terão os seus códigos fontes importados para o projeto, sendo assim, possível edita-los.

Selecione as telas que desejar!

![New scaffolded item](imagens/02-xpelum/new-scaffolded-item-03.png)

Inicialmente, como forma de exemplo, realizei o Scaffold de três "views" - "Register", "Login" e "AccessDined".

Dentro do diretório Areas/Identity/Pages/ foi criado uma nova pasta - Account. Dentro dessa pasta possuimos alguns arquivos, mas inicialmente focaremos nos arquivos "AccsessDenied.cshtml", "Login.cshtml" e "Register.cshtml".

//testar aqui exlcuindo os outros arquivos para checar a real dependencia deles para funcionalidade das views.

![New scaffolded item](imagens/02-xpelum/new-scaffolded-item-04.png)

---

### Conhecendo as Razor Class Libraries

Se formos observar a criação das telas padrões do ASP.NET Core Identity pelo Scaffold, é um pouco diferente das "Views" que conhecemos dos projetos MVC. Não foi criado nenhuma Classe de Model e Controller para realizar o fluxo de chamadas dessas telas quando necessário.

Isso ocorre, por que como foi dito anteriormente, o Identity, a partir da versão do ASP.NET Core 2.1, trabalha com Razor Class Libraries.

O recurso "Razor Class Libraries" é algo novo no ASP.NET Core. Vamos entende-lo melhor com as Views criadas pelo Scaffold do Identity.

---

A Razor Class Libraries (RCL) permite encapsular Razor views, Paginas, Controladores, Razor Components, Views Components e Modelos de dados, podendo ser empacotados e reutilizados, como uma lib.

Inicialmente isso pode parecer um pouco confuso, mas analisando melhor, podemos observar algumas vantagens no uso das Razor Class Libraries e consecultivamente o uso das RCLs pelo Identity.

- Facilidade na compartilhamento de código (UI e Regra de negócio);
- Evitamos a repetição de códigos em diversos projetos;
- Abstração de códigos comuns;

Obs: Nós também podemos criar nossas prórpias Razor Class Libraries e reutiliza-las em nossas aplicaçãoes. Para usar uma RCL temos duas opções - Criando um pacote nuget ou Adicionando como Referência na Aplicação.

#### Analisando a Register.cshtml

A primeira coisa que notamos na Arvore do projeto é que possuimos dois arquivos relacionados a UI de Register - "Register.cshtml" que é Razor page e "Register.cshtml.cs" que é o código C#, que é basicamente a Modelo de dados da Page.

![Register](imagens/02-xpelum/register-01.png)

##### Register.cshtml

O código da Register.cshtml assemelha-se muito aos arquivos de exibição Razor que trabalhamos nos Projetos MVC. O que diferencia é a diretiva "@page".

A diretiva @page transforma o arquivo em uma ação do MVC, o que significa que ele trata as solicitações sem passar por um controlador.

É possvel notar a presença da diretiva "@model RegisterModel".

RegisterModel é criado dentro do arquivo "Register.cshtml.cs".

![Register](imagens/02-xpelum/register-02.png)

##### Register.cshtml.cs

O arquivo Register.cshtml.cs é classe modelo da Razor Page (é a classe PageModel, que nesse caso é "RegisterModel"). Por convenção possui o mesmo nome da Razor Page.

Analisando a classe RegisterModel notamos que é filha de PageModel e recebe por injeção de dependência o "SignInManager", "UserManager", "ILogger" e "IEmailSender".

![RegisterModel](imagens/02-xpelum/RegisterModel-01.png)

Possui duas propriedades publicas - "Input" do tipo InputModel e "ReturnUrl" do tipo string.

![RegisterModel](imagens/02-xpelum/RegisterModel-02.png)

Existe uma classe representando o formulário de registro contendo as propriedades "Email", "Password" e "ConfirmPassword". Todas propriedades decoradas com Data Annotations para validação client side (assemelhando-se a uma ViewModel).

![RegisterModel](imagens/02-xpelum/RegisterModel-03.png)

E por fim, possuis dois métodos que trabalham conforme as requisições do cliente. Temos o método "OnGet" que é executado quando o cliente envia uma requisição "Get" com a Url da razor page (/Identity/Account/Register). O Segundo método é executado quando há uma requisição do tipo "Post" - "OnPostAsync".

![RegisterModel](imagens/02-xpelum/RegisterModel-04.png)

No método "OnPostAsync" é realizado as validações de usuário do Identity e caso válido, persistido no Banco de Dados. Por padrão na coluna UserName é passado o valor do email passado no formulário.

Além da validação e persistencia, é possível notarmos a geração de código relacionado a Confirmação de Email, caso a aplicação possua esse requisito.

![RegisterModel](imagens/02-xpelum/RegisterModel-05.png)

---

## Entendendo como o ASP.NET Core Identity trabalha

Até o momento nós entendemos e implementamos o Identity em uma aplicação e pudemos notar que muita coisa se torna abstrata para o desenvolvedor.

Porém agora vamos entender o que o Identity faz "por baixo dos panos" para ajudar e facilitar a vida do desenvolvedor .NET.

Para conseguirmos entender melhor o Identity vamos analisar o seu código fonte. Podemos encontra-lo de forma aberta no GitHub do "aspnet" e no repositório "AspNetCore".

Dentro desse repositório existe o diretório "src" que possui todas as bibliotecas que estão dispobíveis para o DOT.NET Core. Lá podemos encontrar a pasta "Identity", que possui o seu código fonte.

---

### Classe Startup

Como vimos anteriormente, ao criarmos um projeto já com o Identity, uma das primeira coisas que notamos no código gerado pelo template do ASP.NET Core são as referências do Identity na classe Startup.cs.

No método ConfigureServices é criado as linhas que adicionam o Identity no projeto. No método Configure é criado a linha para ser usado a Autenticação no Projeto.

#### Observações

- Na figura abaixo é possivel ver uma instrução ".AddRoles< IdentityRole>()". Isso não foi criado pelo template. Foi colocado posteriormente, durante as explicações de Roles.

- A Autenticação citada acima não faz parte do Identity em si, porém é usado por ele para a realização da Autorização vista na Demo desse post.

#### Método ConifigureServices

![Startup.cs](imagens/02-xpelum/explicando-Identity-01.png)

#### Método Conifigure

![Startup.cs](imagens/02-xpelum/explicando-Identity-02.png)

---

#### AddDefaultIdentity

Agora vamos entender o que esses códigos acima realmente fazem (linha a linha).

Analisando a primeira linha do código que é reponsavel por adicionar o Identity no projeto, vemos que está sendo adicionado um serviço - **"services.AddDefaultIdentity< IdentityUser>()"**.

Podemos encontrar o método de **AddDefaultIdentity** dentro da classe **IdentityServiceCollectionUIExtensions** que está no diretório "Identity/UI". Sua responsabilidade é "adicionar um conjunto de serviços de identidade comuns ao aplicativo, incluindo um padrão UI, provedores de token e configurar a autenticação para usar cookies de identidade." Seu retorno é um **IdentityBuilder**.

![Identity](imagens/02-xpelum/explicando-Identity-03.png)

A classe **IdentityBuilder.cs** está no diretório "Identity/Extensions.Core/src". Possui a responsabilidade de gerar funções auxiliares de configuação dos serviços do Identity. Podemos citar o "AddRoles" que usamos nesse projeto.

![Identity](imagens/02-xpelum/explicando-Identity-04.png)

---

#### IdentityUser

Podemos encontrar a classe **IdentityUser.cs** no diretório "Identity/Extensions.Store/src". Essa classe herda de "IdentityUser< string>" e possui dois construtores que criam o "Id" e o "SecurityStamp" como novos "Guid" e atribui o UserName quando passado por parâmetro.

![Identity](imagens/02-xpelum/explicando-Identity-05.png)

A classe base **IdentityUser< string>** está no mesmo arquivo - **IdentityUser.cs**.

Podemos ver um construtor e diversas Propriedades que representam um Usuário pelo identity - Id, UserName, NormalizedUserName, Email, NormalizedEmail, EmailConfirmed, PasswordHash, SecurityStamp, ConcurrencyStamp, PhoneNumber, PhoneNumberConfirmed, TwoFactorEnabled, LockoutEnd, LockoutEnabled e AccessFailedCount.

Além disso, é sobrescrito o método "ToString" passando o valor de UserName.

Obs: A Classe IdentityUser.cs é usada para geração de uma tabela de banco de dados. Falaremos disso mais adiante.

![Identity](imagens/02-xpelum/explicando-Identity-06.png)

#### AddRole()

Continuando a análise do código usado pelo Identity, seguimos com a seguinte instrução - ".AddRoles< IdentityRole>()".

Lembrando que essa linha **não** foi gerada pelo template.

**AddRole()** é um método da classe **IdentityBuilder.cs**, que vimos agora pouco. Sua função é "Adicionar serviços relacionados à função do TRole, incluindo IRoleStore, IRoleValidator e RoleManager".

obs: Roles são usadas para autenticar grupos de usuário com características diferenciadas, por exemplo - Admin.

![Identity](imagens/02-xpelum/explicando-Identity-07.png)

#### IdentityRole

A classe **IdentityRole.cs** é responsável por "implementar o padrão do Microsoft.AspNetCore.Identity.IdentityRole" e que usa uma string como chave primária".

O arquivo da classe está no diretório "Identity/Extensions.Store/src".

Ela herda de "IdentityRole< string>" e possui dois construtores. O primeiro é vazio, onde é criado o "Id" como um guid transformado para string. O segundo construtor possui um parametro para receber o "RoleName".

![Identity](imagens/02-xpelum/explicando-Identity-08.png)

A classe base **IdentityRole< string>** está no mesmo arquivo - **IdentityRole.cs**.

Essa classe pois dois contrutores e diversas propriedades que representam uma Role - Id, Name, NormalizedName e ConcurrencyStamp.

Também possui a sobrescrita do método "ToString()" retornando o "Name".

Obs: A Classe IdentityRole.cs é usada para geração de uma tabela de banco de dados. Falaremos disso mais adiante.

![Identity](imagens/02-xpelum/explicando-Identity-09.png)

---

#### AddDefaultUI()

Na próxima linha, temos o seguinte código **.AddDefaultUI(UIFramework.Bootstrap4)**.
De cara notamos que é um método que está passando como parâmetro o Bootstrap 4 como a biblioteca padrão para ser utilizado nas páginas que o Identity gera automaticamente.

Mas não é só isso que esse método faz...

Esse método está localizado na classe "IdentityBuilderUIExtensions.cs", que por sua vez está no diretório "Identity/UI/src".

![Identity](imagens/02-xpelum/explicando-Identity-10.png)

Como podemos notar na imagem do método, a primeira coisa que ele está fazendo é executar o método "AddSignInManager()". É um método da classe que extende o IdentityBuilder - "IdentityBuilderExtensions.cs".

Além disso é adicionado alguns outros serviços e opções de configurações para importar toda a parte de UI da aplicação, como exemplo o IEmailSender e MVC.

Obs: Além do Bootstrap 4, podemos usar o Bootsrap 3 como framework padrão em nossas aplicações, caso seja necessário.

---

#### AddEntityFrameworkStores()

Na ultima linha criada no método "ConfigureServices" da classe "Startup.cs" temos o metodo "AddEntityFrameworkStores()" que pertence a classe "IdentityEntityFrameworkBuilderExtensions.cs", que é um extension methods de "IdentityBuilder".

També é possível notar a referêcia ao Contexto de dados que o EntityFramework Core irá usar - "ApplicationDbContext". Esse contexto também foi criado pelo Identity, porém falaremos mais dele adiante.

Essa classe está localizada no diretório "Identity/EntityFrameworkCore/src".

Como o nome do método sugere, é ele o responsável por adicionar o Entity Framework Core para persistir os dados do Identity.

Por utilizar o ORM Entity FrameworkCore como padrão, o Identity criará as tabelas necessárias a partir da abordagem Code First, onde mapeamos nossas classes de entidades primeiramente, e só depois, com a utilização de Migrations, é criado o Banco de Dados com as taelas necessárias.

![Identity](imagens/02-xpelum/explicando-Identity-11.png)

#### ApplicationDbContext

Nessa ultima instrução, também é passado como referência o Contexto **ApplicationDbContext** que também foi criado automaticamente pelo template do Identity.

A classe ApplicationDbContext.cs herda de IdentityDbContext e possui um construtor, passando o DbContextOptions para a classe base.

![Identity](imagens/02-xpelum/explicando-Identity-12.png)

Obs:**IdentityDbContext** herda de **IdentityUserContext**, que por sua vez herda de **DbContext**.

//eplicar as configurações de senha, usuario,

//como ele cria a senha hash, tabelas normalizadas

//entender onde e como ele selecioona as tabelas para criar a migration inicial

// falar da connection string

//falar do DbContext - como ele ccria o ApplicationDbCOntext

---

### UI

Como falamos anteriormente, as Interfaces de Usuários (UI) padrões que são criadas pelo Identity são do tipo Razor Class Library (RCL).

Já falamos também do que se trata as "Razor Class Libraries** - " É um tipo de recurso que permite encapsular em uma biblioteca construções como Razor Pages, Views e Controllers, contribuindo assim para um maior reaproveitamento de código em projetos Web baseados no ASP.NET Core."

No caso do Identity, foram encapsuladas Razor Pages. Podemos encontrar, no código fonte, as Razor Pages do Identity dentro do diretório **UI**.

Ao navegarmos pelo Diretório "UI", chegamos nos códigos fontes a partir do diretório **UI/src/Areas/Identity/Pages/..**. Dentro da pasta Pages existem mais outras duas Pastas - V3 e V4. Nesse caso, iremos estudar a mais recente - V4.

Dentro de **V4** existem diversas PartialViwes além da pasta **Account**. Essa Pasta Account é onde encontra-se a grande maioria das Razor Pages do Identity, que podemos importa-las em nossos projetos caso seja necessário modifica-las ou traduzi-las, por exemplo.

![Razor Class Library](imagens/02-xpelum/RCL-01.png)

Podemos notar que a sequência de pastas criadas ao realizarmos um Scaffolding (Importar a RCL para um projeto nosso) de uma "tela" em um projeto é muito parecida com a árvore do código do fonte do Identity.

Abaixo podemos ver um grande número de Razor Pages que são padrões do Identity, ou seja, podemos importar qualquer um dependendo da necessidade do projeto.

![Razor Class Library](imagens/02-xpelum/RCL-02.png)

No aplicação que criamos para a entendermos um pouco mais de como funciona o Identity, realizamos o Scaffolding de apenas três telas - Register, Login e Acesso Negado, que no identity estão representados por "Register.cshtml", "Login.cshtml" e "AccessDenied.cshtm" respectivamente, além dos arquivos cSharp (extensão cshtml.cs).

Analisando o código desses arquivos fontes, notamos que são identicos ao que importamos em nosso projeto:

- Register.cshtml - Esse arquivo inicia-se com a diretiva @page (já falado anteriormente) e possui o código HTML que representa o formulario de Registro de um Identity User padrão:

![Razor Class Library](imagens/02-xpelum/RCL-03.png)

- Register.cshtml.cs - Da mesma forma que o arquivo que representa o HTML da View Register é identico ao Importado em nossa aplicação, o arquivo CSharp também é. Possui uma classe **RegisterModel** que herda de PageModel. Existem algumas propriedades e uma classe interna **InputModel** que representa os campos que serão usados no formulário de Registro.

![Razor Class Library](imagens/02-xpelum/RCL-04.png)

Além disso ainda possui os métodos OnGetAsync e OnPostAsync que trabalham nas requisoções do Client.

![Razor Class Library](imagens/02-xpelum/RCL-05.png)

Analisando a Razor Class Library de Register, obeservamos que os códigos gerados pelo Scaffolding assemelha-se muito com o código fonte das Razaor Pages, com isso evita a necessidade de analisarmos o as outras Insterfaces de Usuário criadas - Login e Acesso negado, pois seguem o mesmo padrão.

---

### Registrando um Usuário

Agora vamos entender o processo de Registro de Usuário e como o Identity se comporta nesse momento.

Quando o cliente clica na oção "Register" no menu de navegação da aplicação, o método "OnGetAsync" da classe "RegisterModel" é executado. OnGetAsync podemos deduzir que se trata de um método do retorno Get, com a responsabilidade de retornar a "view" com o formulário de Registro.

Após o Cliente clicar no botão "Register" após preencher o formulário, o método "OnPostAsync" é executado. É dele a responsabilidade tratar as requisições do tipo "Post".

A primeira linha de instrução do código é para tratarmos e retornarmos a URL. Em seguida caimos no bloco de código que faz a verificação se ModelState é valido.

Com o ModelState válido, temos a seguinte linha de instrução **var user = new IdentityUser { UserName = Input.Email, Email = Input.Email };**. Onde é criado um novo IdentityUser passando o valor preenchido no campo da tela Email para as propriedades "UserName" e "Email".

O construtor padrão do IdentityUser possui apenas duas intruções - criação do Id e SecurityStamp, ambos do tipo Guid e convertidos para string.

![Razor Class Library](imagens/02-xpelum/RCL-06.png)

As propriedades usadas nesse momento são :

        [ProtectedPersonalData]
        public virtual string UserName { get; set; }

        [ProtectedPersonalData]
        public virtual string Email { get; set; }

A seguinte instrução **var result = await _userManager.CreateAsync(user, Input.Password);** é para criar um usuário passando o IdentityUser e a Senha digitada no Campo Password da view, através do método CreateAsync de _userManager.

Obs: Não apenas UserManager, mas como SignInManager, ILogger e IEmailSender estão injetado na classe via Injeção de Dependência.

Analisando o Método CreateAsync da classe UserManager notamos que aqui é verificado se o Usuario e Password são verificados se estão nulos.

![Razor Class Library](imagens/02-xpelum/RCL-07.png)

Caso Usuário e Password estejam preenchidos de acordo com o esperado, é executado o método **UpdatePasswordHash**, onde com o nome diz, cria uma senha com HASH: 

        private async Task<IdentityResult> UpdatePasswordHash(IUserPasswordStore<TUser> passwordStore,
            TUser user, string newPassword, bool validatePassword = true)
        {
            if (validatePassword)
            {
                var validate = await ValidatePasswordAsync(user, newPassword);
                if (!validate.Succeeded)
                {
                    return validate;
                }
            }
            var hash = newPassword != null ? PasswordHasher.HashPassword(user, newPassword) : null;
            await passwordStore.SetPasswordHashAsync(user, hash, CancellationToken);
            await UpdateSecurityStampInternal(user);
            return IdentityResult.Success;
        }

Obs.: Essa senha Hash é guardada no banco de dados. Não salvamos a senha que foi criada no formulário pelo usuário por questões de segurança.

Com a senha Hash criada, vamos para a próxima instrução.

                if (result.Succeeded)
                {
                    _logger.LogInformation("User created a new account with password.");

                    var code = await _userManager.GenerateEmailConfirmationTokenAsync(user);
                    var callbackUrl = Url.Page(
                        "/Account/ConfirmEmail",
                        pageHandler: null,
                        values: new { userId = user.Id, code = code },
                        protocol: Request.Scheme);

                    await _emailSender.SendEmailAsync(Input.Email, "Confirm your email",
                        $"Please confirm your account by <a href='{HtmlEncoder.Default.Encode(callbackUrl)}'>clicking here</a>.");

                    await _signInManager.SignInAsync(user, isPersistent: false);
                    return LocalRedirect(returnUrl);
                }

Aqui verificamos se o Resultado da criação, usando o CreateAsync, foi com sucesso (**var result = await _userManager.CreateAsync(user, Input.Password);**). 

Caso tenha sido uma criação com sucesso, o código vai para dentro do bloco "if". Dentro desse bloco vemos muito código responsável pela criação do email de confirmação ao registrar. Nesse exmplo não estamos aplicando essa funcionalidade, podemos falar em um futuro Post.

Além dos códigos de criação de Email de Confirmação, notamos uma mensagem de Logger ("User created a new account with password.") e também a execução do metodo "SignInAsync" do "_signInManager".

_signInManager é injetado no construtor através da classe SignInManager.cs. Podemos encontrar a classe no source do identity pelo diretório **Identity/Core/src/SignInManager.cs**

Abaixo temos o metodo SignInAsync:



### Logando na Aplicação

//ao clicar em Login, o que acontece?????????