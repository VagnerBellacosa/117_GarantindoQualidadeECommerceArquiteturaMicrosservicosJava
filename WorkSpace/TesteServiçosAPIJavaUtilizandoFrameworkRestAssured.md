[![Roberto Da Silva Filho](https://miro.medium.com/fit/c/56/56/0*iQUK4oJhnaEpmXIe.jpg)](https://medium.com/@roberto.siilva3x?source=post_page-----5a42b65a452e-----------------------------------) - [Roberto Da Silva Filho](https://medium.com/@roberto.siilva3x?source=post_page-----5a42b65a452e-----------------------------------) - [Jul 9, 2020·9 min read](https://medium.com/@roberto.siilva3x/teste-de-serviços-api-com-java-utilizando-framework-rest-assured-5a42b65a452e?source=post_page-----5a42b65a452e-----------------------------------)



# Teste de serviços(API) com java utilizando framework Rest-assured

![img](https://miro.medium.com/max/1400/1*f6Ior4oEwcpL3tBUlk4V6Q@2x.jpeg)

Hoje vamos mostrar como utilizar o framework Rest-assured.

primeiro vamos dar uma breve introdução do que é uma API,quais serviços ela possui e algumas ferramentas para estar realizando os teste de serviço.Em seguida iremos falar sobre o framework Rest-assured, o que é esse framework, quais ferramentas usar,para que ele serve, mostrar passo a passo de como usar, quais suas vantagens e por ultimo e não menos importante, os desafios.

O que é API ?

![img](https://miro.medium.com/max/60/1*hUFYQfr9hy10x4m3SjKltQ@2x.jpeg?q=20)

![img](https://miro.medium.com/max/630/1*hUFYQfr9hy10x4m3SjKltQ@2x.jpeg)

API é a abreviação de “Application Programming Interface” que no português significa (interface de programação de aplicativos).Trata-se de um conjunto de metodos e padrões estabelecidos em uma aplicação que consiga entregar funcionalidades recursos e serviços de forma simplificada a outras aplicações que não precisam conhecer a implementação interna dessas funcionalidades.

Ela pode se comunicar em diferentes linguagens como Java,php,Ruby,.net.Basta consumir os dados de determinado serviço.

Dessa forma, elas proporcionam interoperabilidade entre aplicações proporcionando que uma aplicação possa utilizar funcionalidades de diversas outras, permitindo a comunicação entre aplicações e usuários.Podemos citar como exemplo um aplicativo mobile acessando a API do GitHub para obter repositorios e outros dados.

Abaixo,podemos vê um exemplo do funcionamento de uma API, onde o usuário(Browser) faz uma solictação (requisição Resquest) para o servidor processar toda informação solicitada e devolve a resposta(Response) para o usuário(Browser).

![img](https://miro.medium.com/max/60/1*g3H2Jp3cTlcpCMhr55kMTg@2x.jpeg?q=20)

![img]()

Representação dos dados

Necessitamos de um padrão para representar os dados que serão transmitidos que seja legivél tanto para máquinas quanto para humanos.

Atualmente o padrão mais utilizado para a troca de dados entre diferente APIs é o formato JSON(Javascript Object Notation), também tem APIs que representam dados utilizando XML, mais seu número é menor.

Abaixo podemos vê um exemplo de JSON;

{

“nome”:”Joao”,

“cpf”:”09089767865",

“email”:”joao@gmail.com”

}

Representação de dados no formato XML:

<Contato>

<id>200</id>

<nome>Joao</nome>

<email>joao@gmail.com</email>

<Telefones>

<Telefone>

<id>1</id>

<ddd>11</ddd>

<numero>998076543</numero>

</Telefone>

<Telefone>

<id>2</id>

<ddd>81</ddd>

<numero>999876576</numero>

</Telefone>

</Telefones>

</Contato>

Esses dois tipos de formatos apresentado, especifica um dados do usuário.

Digamos que um usuário precise cadastrar seus dados em um sistema web. A forma de tráfego ela a aplicação web e a API será de um dos dois tipos informado acima.

Levando em consideração que o formato JSON é recomendado na maioria das vezes.

HTTP

HTTP(Protocolo de transferência de hipertexto) é uma comunicação que existe em toda a internet em que os sites e conteúdos que tragam hiperlinks possam ser encontrados mais facil pelo publico.

O navegador que você usa é um cliente HTTP que envia solitações para um determidado servidor.

Quando um usuário acessa uma URL do site, o navegador cria uma solicitação HTTP e a envia ao endereço de IP indicado pela URL.Sendo assim,o servidor recebe essa solicitação e retorna os arquivos(dados) associados.

HTTP fornece alguns verbos que possibilita fazer requisições para que possamos: recuperar, criar, atualizar e deletar dados.

abaixo iremos abordar os principais:

.GET : O GET é utilizado para a leitura de dados

.POST : O POST é utilizado para a criação de novos dados

.PUT: O é utilizado para atualizar dados

.DELETE : O DELETE é utilizado para excluir dados

Vamos dar um exemplo que como funciona um sistema se comunicando com outro sistema usado por um usuário.

Digamos quem o gerente de um loja precise fazer o cadastro de um produto no sitema de estoque. O usuário(gerente) cadastra todos os dados necessários no sistema. O mesmo clica no botão de cadastrar, o sistema internamente enviar uma requisição POST

para uma determinada API. Nesses dados que são enviado pelo sistema WEB para uma API estão: os dados enviado do produto em um formado JSON e o endereço que foi enviado (URL). Se todas as informações foram completas e foram bem sucedidas a API fica responsável de retornar

alguma informação para o sistema WEB.

Segue a imagem abaixo explicando como funciona o tráfego de informação.

![img](https://miro.medium.com/max/60/1*n8nJXnqwjWcGONtJgGoAqw@2x.jpeg?q=20)

![img]()

Status HTTP

Os códigos de status das respostas HTTP indicam se uma requisição HTTP foi corretamente concluída.As respostas são agrupadas em cinco classes:

1.Respostas de informaççao

2.Respostas de sucesso

3.Redirecionamentos

4.Erros do cliente

5.Erros do servidor

Respostas de informação: Indica que a solicitação foi recebida e que o servidor está pronto para dar continuidade ao processo

Os códigos mais comuns são:

.100 Continuar

.101 Mudando protocolo

Respostas de sucesso: Indica que ndica que a solicitação foi recebida, entendida e que será processada com êxito pelo servidor.

Os códigos mais comuns são:

.200 OK;

.201 Criado;

.202 Aceito;

.203 não-autorizado;

.204 Nenhum conteúdo;

.205 Reset;

.206 Conteúdo parcial;

.207-Status Multi.

Redirecionamentos : Indica que você será redirecionado a outra página. Isso acontece, por exemplo, quando a URL que você pesquisou foi alterada

Os códigos mais comuns são:

.300 Múltipla escolha;

.301 Movido Permanentemente;

.302 Encontrado;

.304 Não modificado;

.305 Use Proxy;

.307 Redirecionamento temporário.

Erros do cliente : Indica que o servidor não conseguiu processar a solicitação porque o cliente a fez de forma errada

Os códigos mais comuns são:

.400 Requisição inválida;

.401 Não autorizado;

.402 Pagamento necessário;

.403 Proibido;

.404 Não encontrado;

.405 Método não permitido;

.406 Não Aceitável;

Erros do servidor : Indica que, por um erro do servidor, a sua solicitação não pode ser atendida

Os códigos mais comuns são:

.500 Erro interno do servidor;

.501 Não implementado;

.502 Bad Gateway;

.503 Serviço indisponível;

.504 Gateway Time-Out;

.505 HTTP Version not supported.

Abaixo segue a imagem dos status mais usados:

![img](https://miro.medium.com/max/60/1*qbme-elpwzUxnAaD9kPnRg@2x.jpeg?q=20)

![img]()

Bom,agora vamos falar sobre o framework(Rest-assured) usado para fazer teste em api.

Oque é Rest Assured ?

O Rest Assured é uma biblioteca em java que permite testar serviços RESTful em java de uma maneira muito simples.Ele nos provê uma maneira de criar chamadas HTTP,como se fossemos um cliente acessando a API. Isso nos possibilita uma série de funcionalidade para que se teste os serviços,requests com diferentes verbos e combinações de dados até as respostas recebidas do servidor incluindo código de retorno, cabeçalho e corpo da response.

A ferramenta que escolhemos para estar executando este tutorial é o IntelliJ IDEA Community.

Com a IDE,o java e o Maven instalados,vamos criar um projeto Maven.No IntelliJ conseguimos fazer da seguinte maneira a seguir;

1- Clicar em Create New Project

![img](https://miro.medium.com/max/60/1*afxd-r-yIhoHQdGAPS-dFA@2x.jpeg?q=20)

![img]()

2-Selecionar o “Maven” que fica no lado esquerdo e logo apos clicar em “Next”

![img](https://miro.medium.com/max/60/1*fl1qnRFdrdr_3wTDOOiimA@2x.jpeg?q=20)

![img]()

3- Expandir. o Artifact Coordinates e preencher GroupId: “br.com.tutorial” ArtifactId: “restAssuredTutorial” Após preencher com essas informações clicar em “Finish”

![img](https://miro.medium.com/max/60/1*Q11ezO0Qarq_mX_8edEyUg@2x.jpeg?q=20)

![img]()

Ao criar o projeto a IDE vai atualizar as dependências necessárias e apresentar o projeto com uma estrutura basica.

O maven utiliza o arquivo “pom.xml” é o controlador de versões do projeto.

basta adicionar as dependências e salvar o arquivo.

Agora vamos adicionar a dependência ao nosso projeto.Acessar [http://mvnrepository.com](http://mvnrepository.com/)

1-Pesquisar por JUnit. Clicar em JUnit e depois na versão 4.13. Copiar a dependência do Maven

Feito isso, dar um duplo-clique no arquivo pom.xml, clicar na aba pom.xml, criar as tags <dependencies></dependencies> e colar a dependência antes da tag </dependencies>.

2-Pesquisar por Rest-assured. Clicar em Rest-assured e depois clicar na versão 4.3.0.

Copiar a dependência do Maven. Feito isso, colar a dependência antes da tag </dependencies>.

O arquivo “pom.xml” ficara da seguinte forma:

https://gist.github.com/amandabandeira/488c3ef9f5514750683e594728e41296

Neste arquivo dizemos para o Maven que queremos usar o Rest Assured, Junit, Json Path e o Json Schema.

Ele tratará de baixar o que for necessário e deixar tudo configurado para o nosso uso.

Com o ambiente configurado em sua máquina,a primeira coisa a fazer é criar a classe de teste “RestAssuredExemplo”.

dentro do package “src > test > java > exemplo. Com a classe criada vamos configurar qual URL da API vamos testar, nesse exemplo vamos usar o endpoint https://reqres.in/api/users

private String url = “https://reqres.in/api/users”;

A sintaxe de escrita dos comandos do Rest Assured ele usa o formato Given/When/Then, que é a mesma sintaxe utilizada no Behavior Driven Development (BDD)

esse padrão facilita o entendimento da escrita do teste e permite que você tenha a suas precondições, ações e resultados esperados de uma maneira clara no seu teste.

Um método ou verbo indica uma ação que deve ser realizada em um recurso.A baixo vou mostrar exemplos dos quatros principais

verbos:

GET

O verbo GET ele deve ser utilizado quando se deseja consultar ou recuperar dados e não deve ser utilizado para alterar o estado do recurso acessado.

Podemos observar no primeiro teste, que temos o GET para recuperar os dados da página 01.o método Given() é utilizado para configurar as precondições para rodar o teste, nesse caso temos o parâmetro “page=1",

que indica que queremos recuperar os dados da primeira página.

@Test

public void getOneTest(){

given().

param(“page”, “1").

when().

get(url).

then().

statusCode(200).

body(“page”, equalTo(1));

}

O When() informamos o verbo que queremos utilizar passando a URL alvo do nosso teste (GET).Temos as validações que desejamos fazer no nosso teste,

nesse caso estamos validando o status code e dentro do Response Body verificamos se o atributo page retornado indica a página que solicitamos, nesse caso a página 1.

POST

Vamos usar o POST para fazer o cadastro de um novo usuário,

para isso vamos criar um objeto JSON para representar o usuário e passarmos ele no body da nossa chamada,

vamos criar o objeto com os valores name e job

JSONObject requestParams = new JSONObject();

requestParams.put(“name”, “Maria”);

requestParams.put(“job”, “Analista de Teste Pleno”);

Logo após a criação do objeto vamos utilizar o metodo body,para indicar ao Rest Assured que vamos utilizar o objeto JSON que criamos anteriormente.

Fazemos a chamada ao método POST passando a URL. E para finalizar, validamos se o status code retornado foi 201(created)

e se o Response Body possui o atributo create date.

given().

body(requestParams.toJSONString()).

when().

post(url).

then().

statusCode(201).

body(containsString(“createdAt”));

Usuário criado, observe que o endpoint apenas retorna o status code, ID e data da criação.

PUT

O metodo é utilizado para atualizar os dados de um recurso previamente cadastrado.Observem que a estrutura é bem parecida com a do POST

@Test

public void putUserTest(){

JSONObject requestParams = new JSONObject();

requestParams.put(“name”, “Madalena.”);

requestParams.put(“job”, “QA”);

As diferenças do POST para o PUT,é que PUT passamos os valores atualizados no request Body, também passamos como parâmetro além da URL, o ID do usuário que desejamos atualizar.

given().

body(requestParams.toJSONString()).

when().

put(url + “/2").

then().

statusCode(200).

body(containsString(“updatedAt”));

}

O status code,nesse caso do PUT o retorno é o 200 (OK) e no body é retornado o campo update date.

DELETE

Para executar o delete, simplesmente chamamos o verbo, passando o ID do usuário que desejamos apagar.

Para validar a exclusão basta verificar o status code 204 (No Content) retornado pelo endpoint.

@Test

public void deleteUserTest(){

when().

delete(url + “/2").

then()

.statusCode(204);

}

O código completo fica da seguinte forma:

https://gist.github.com/amandabandeira/4f0470622983bf05f85d007bfe5744fa

A escolha da ide pode ser a de sua preferência,caso queira utilizar outra que possua mais familiaridade também pode usar.

Abaixo segue as ferramentas com os links para a página de instalação,o processo de instalação é simples,basta seguir o que esta nos tutoriais.

.IntelliJ IDEA Community

https://www.jetbrains.com/idea/download/#section=windows

Maven

https://maven.apache.org/install.html

.Java JDK 8+

https://java.com/en/download/

Vantagens de utilIzar API

.Alto poder de integração

.Otimização da gestão interna

.Viabilização de parcerias

.Customização dos serviços

Desafios

O grande desafio é mudar a forma de pensar quando se fala em criar uma aplicação e entregar a um usuário final.

O pensamento é “nos vamos criar uma aplicação que através dela, iremos ajudar outras aplicações a entregar seus serviços.”

Então, tem que tomar mais cuidado com as decisões com a arquitetura, os motivos, as tecnologias que serão utilizadas, performance, para que tenha um tempo de resposta baixo, conteúdo enxuto para o usuário, como o sistema vai se comportar com vários acessos simultâneo entre outras séries de testes para assegurar a qualidade e entrega de valor da api.

Joanna Amanda  & [Roberto Da Silva Filho](https://medium.com/@roberto.siilva3x?source=post_sidebar--------------------------post_sidebar--------------)

