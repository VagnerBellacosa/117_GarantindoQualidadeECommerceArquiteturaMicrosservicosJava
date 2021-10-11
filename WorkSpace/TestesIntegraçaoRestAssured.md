# TESTES DE INTEGRAÇÃO COM REST ASSURED

- [Qualidade](https://blog.onedaytesting.com.br/category/qualidade/)

As APIs tornaram-se fundamentais para o funcionamento de quase todos os produtos digitais que são consumidos atualmente e isso se deve à crescente expansão de programas que precisam se comunicar com outras aplicações.

Podemos imaginar uma loja virtual que forneça seus produtos juntamente com o preço do frete. Para este valor ser fornecido é necessário uma API se comunicar com os correios para validar o custo do envio de seu produto. Este e outros tipos de casos são constantemente usados na vida cotidiana mesmo que o usuário não saiba.

Entendendo a importância desta integração em nosso cotidiano é evidente que qualquer erro que possa ocorrer em uma API vá influenciar o serviço dependente. É neste cenário que entramos na qualidade de software.

Para construir aplicações com qualidade, segundo um [artigo](https://www.dtidigital.com.br/blog/por-que-automatizar-testes/) que li recentemente, é necessário termos sistemas adaptáveis, resilientes, flexíveis e evoluíveis. Ou seja, aplicações que realizam o esperado de forma eficiente. 

Para validar este funcionamento surgiram os testes de integração, que visam testar se nossas aplicações estão sendo integradas de forma correta e eficiente, além de respeitar as regras de negócio. É neste meio que surge a ferramenta que iremos explorar neste artigo: **o Rest Assured**.

## O que é Rest Assured?

Rest-Assured é uma ferramenta que foi desenvolvida para facilitar a criação de testes automatizados para APIs REST. Esta oferece suporte para validar protocolo HTTP e requisições em JSON. 

O Rest Assured oferece também extensas opções de validações das requisições que são enviadas nos serviços REST, tais como: Status Code, Headers e também elementos do Body. Tornando a ferramenta extremamente flexível para utilizar na criação de testes automatizados de API. 

Agora que temos uma pequena base do que é e para que serve o Rest Assured, podemos começar a explorar coisas mais práticas com esta ferramenta.

Neste artigo utilizarei um exemplo de uma aplicação REST que desenvolvi para demonstrar o funcionamento da ferramenta. Neste exemplo utilizo a linguagem Kotlin para desenvolver a aplicação, pois tem uma ótima integração com a ferramenta. Existem outras versões desenvolvidas do Rest Assured em outras linguagens como [.Net](https://github.com/lamchakchan/RestAssured.Net) e [Go](https://github.com/Jesse0Michael/go-rest-assured). Você pode clonar o projeto com o seguinte comando: 

```
| > git clone https://github.com/defalt388/restAssured.git
```

Na aplicação que vamos usar como exemplo iremos utilizar o gradle para gerenciar as dependências.

```
testImplementation("io.rest-assured:rest-assured:3.1.1")
testImplementation ("io.rest-assured:json-path:3.1.1")
testImplementation("org.assertj:assertj-core:3.16.1")
testImplementation("io.rest-assured:xml-path:3.1.1")
testImplementation("io.rest-assured:json-schema-validator:3.1.1")
testImplementation ("io.rest-assured:json-path:3.1.1")
testImplementation("org.assertj:assertj-core:3.16.1")
testImplementation("io.rest-assured:xml-path:3.1.1")
testImplementation("io.rest-assured:json-schema-validator:3.1.1")
```

Segundo a [documentação](https://github.com/rest-assured/rest-assured/wiki/GettingStarted) do Rest Assured estamos basicamente importando:

- **Rest-Assured:** Dependência que importa a ferramenta Rest Assured. Versões acima do Java 9 importam todos as outras dependências que iremos comentar automaticamente. 
- **Json-Path:** Dependência que contém funções semelhantes ao XPath. JSONPath é usado para selecionar e extrair os valores de propriedade de um documento JSON. Podendo ser importada automaticamente em versões acima do Java 9. Caso queira conhecer um pouco mais sobre a ferramenta pode ler a documentação do [JSONPath](https://github.com/json-path/JsonPath).
- **Xml-Path:** Dependência que facilita a conversão de respostas em XML. Podendo ser importada automaticamente em versões acima do Java 9.
- **Json-Schema-Validator:** Permite realizar validações com arquivos em Schemas JSON. 
- **AssertJ:** Dependência que permite realizar as assertivas na aplicação. 

## Iniciando com o básico

Para começarmos a entender como o Rest Assured funciona, iremos realizar um teste muito simples, na qual se valida um endpoint que retorna uma lista. Para avaliarmos se a operação ocorreu de forma correta, iremos validar se o Status Code de nossa aplicação retornou um 200. 

```
private val ENDPOINT: String = "/turismo"

@LocalServerPort
internal var port: Int = 0 -> porta aleatória da aplicação

@Test
fun `Dado que a operação seja um sucesso é retornado uma lista com todos os guias turísticos`() {

     val before = repository.findAll()
     val after = given() -> serão usadas posteriormente

.port(port)
.log().all()
.`when`()
.get("$ENDPOINT/guias")
.then()
.log().all()
.statusCode(OK.value()) -> status Code 200
}
```

O Rest Assured, como podemos notar, utiliza a sintaxe da linguagem GHERKIN (Given, When, Then), amplamente utilizada em [práticas como BDD](https://blog.onedaytesting.com.br/bdd-introducao/). Essa sintaxe é utilizada para dividir o código em seções para demonstrar seu comportamento. Abaixo explico resumidamente cada uma delas:

- **Given:** Define o contexto da aplicação, como por exemplo destacar quais headers, parâmetros, portas e tokens que a aplicação deve ter para ser inicializada.

- **When:** Este trecho identifica a proposta de seu cenário. “Quando” você insere um dado algo deve acontecer.

- **Method:** Este campo logo após o “when” define o método que será executado na aplicação, podendo ser um POST, PATCH, GET e entre outros.

- **Then:** Será o resultado a ser exibido. Nele você pode validar qual foi a resposta da aplicação.

[**Você pode se aprofundar em Gherkin neste nosso artigo.**](https://blog.onedaytesting.com.br/gherkin/)

Agora que conhecemos a sintaxe, podemos compreender melhor o Rest Assured. Quando executamos aquele teste que fizemos, a resposta de nossa aplicação será uma lista dos guias contidos no nosso banco seguido de um status code 200, caso contrário será lançado uma exceção.

Mas como podemos validar se a resposta está realmente correta? Pois os dados do nosso banco podem ser retornados e estarem errados, não é? Para isso, podemos acrescentar algumas linhas depois do status code:

```
.spec(
   expect()
       .header("content-type", `is`(("application/json")))
       .body("$", not(emptyOrNullString()))
)
.extract().body().jsonPath().getList(".", turismo::class.java)
assertThat(after).isEqualTo(before)
```

Basicamente o que estamos fazendo a partir do spec é: 

- Validando que esperamos que nossa aplicação nos retorne uma resposta em JSON. 
- Nossa body não pode estar vazia ou nula
- Extraímos o arquivo passando o caminho para o jsonPath (uma das dependências que importamos) e convertemos a resposta para o modelo de nossa entity, no caso a classe turismo. 
- Por fim, utilizando a biblioteca AssertJ, usamos as variáveis que criamos no início para validar os campos. A variável **findBD** estará realizando um GET diretamente no banco pela classe repository, enquanto a **findAPI** realiza a requisição via Rest Assured. 
- Ao final validamos se o conteúdo de nosso banco está igual ao que nos foi retornado pela API. Desta forma podemos testar se nossa aplicação está retornando os dados corretamente.

## Rest Assured – Post

Terminamos de demonstrar um exemplo com o método GET, mas sabemos que o Rest Assured serve para testar os métodos de uma API REST. Portanto, iremos conhecer como é realizado um teste validando a inserção de um novo usuário, método conhecido também como POST:

![img](https://blog.onedaytesting.com.br/wp-content/uploads/2020/09/2020-08-20_10-37.png)

Basicamente, o que estamos fazendo é:

- Com a variável ***guia\*** criamos um usuário com a classe de nossa entity e por meio do [**Jackson**](https://github.com/FasterXML/jackson), na qual pode ser definido como um conjunto de ferramentas que analisa e converte dados. Em nosso caso utilizamos para convertermos a variável ***guia\*** em um objeto JSON, como pode ser visto no ***payload\***.
- Em nossa requisição, por ser um post, devemos utilizar o ***content-type\*** para dizer que tipo de arquivo estamos enviando para nossa aplicação. Em nosso caso um JSON. 
- Seguindo adiante, em nossa body enviamos nosso payload. Em seguida, dizemos qual método utilizaremos e passamos nosso ***endpoint\***. 
- Ao final, realizamos uma busca em nosso banco por meio da classe repository. Em seguida realizamos um Assert validando se cada campo deste usuário no banco é igual ao nosso payload.

## Rest Assured – Patch

Nossa aplicação basicamente consiste em um banco que armazena guias turísticos, mas, caso um funcionário seja trocado, como faríamos para trocar os dados de nosso banco?

Para fazer esta alteração em um único usuário realizamos o PATCH. Caso fosse necessário realizar uma alteração em todos os campos seria feito um PUT, porém nosso objetivo é alterar apenas um campo.

Para entender um pouco mais sobre estas operações temos um [artigo](https://blog.onedaytesting.com.br/teste-de-api/) publicado no blog que comenta um pouco mais sobre PATCH e PUT. 

Por estarmos testando uma aplicação, nossa preocupação é ver se esse tipo de operação está funcionando corretamente, pois quem garante que se ao trocar o nome de um usuário o restante não seja trocado também, não é? 

Vejamos primeiro a forma que nos é retornado os campos em JSON: 

```
{
    "id": 1,
    "nome": "Miguel Ferreira",
    "genero": "M",
    "pontoturistico": "Cristo Redentor"
}
```

Como podemos observar, é nos retornado quatro campos. Neste nosso exemplo queremos validar se nossa a operação está alterando apenas um campo, mais especificamente o campo “nome”. 

Para fazermos isso precisamos primeiro mapear o campo que iremos alterar: 

```
val value = mapOf("nome" to "Matheus Oliveira")
```

Desta forma nossa variável mapeia nosso campo “nome” e insere um novo valor. Agora veremos uma segunda validação: 

Vejamos agora nosso código com as validações posteriores:

![img](https://blog.onedaytesting.com.br/wp-content/uploads/2020/09/unnamed.png)

O que basicamente fizemos aqui foi:

- Com a variável ***before\*** realizamos uma busca em nosso banco com o ID do usuário que queremos alterar e, em seguida, verificamos se este resultado é diferente de nosso ***value\***, pois não faria sentido alterars para o mesmo valor.
- Mais pro final criamos uma segunda variável chamada ***after\****,* que realiza a mesma função do ***before,\*** e em seguida realizamos um assert verificando se o campo “nome” é igual ao nosso ***value\***. 
- Por fim, realizamos um último assert validando se todos os campos com exceção do “nome”, que já validamos acima, são iguais ao nosso ***before.\*** Desta forma fica evidente que foi alterado apenas o campo “nome”. 

## Rest Assured – Validando Exceções

Como último exemplo de nossa aplicação, realizaremos uma validação em que verifica se quando busca um ID que não existe ele retorna uma exceção informando o erro. 

Vejamos então nossa mensagem de erro:

```
{
    "timestamp": "2020-08-20T14:32:58.836+00:00",
    "status": 404,
    "message": [
        "O Id buscado não existe!"
    ]
}
```

Este exemplo contém a mesma estrutura do primeiro que apresentei. Porém, a diferença está no Status Code e também nas validações finais:

![img](https://blog.onedaytesting.com.br/wp-content/uploads/2020/09/2020-08-21_14-28.png)

Neste teste fizemos o seguinte:

- Nosso endpoint, caso fosse um sucesso, nos retornaria apenas um dado. Contudo, o ID que enviamos não existe. Desta forma ele nos retornará um erro 404.
- No expect realizamos algumas assertivas que validam nossa mensagem de erro. Como por exemplo, verificamos se nossa aplicação contém um content-type em JSON. 
- Timestamp não pode ser nulo ou estar vazio 
- O Status retornado deve ser um 404
- E por fim validamos se a mensagem retornada está correta.

## Conclusão

Como foi demonstrado neste artigo, é evidente que o Rest Assured se torna uma ferramenta muito eficiente em testar nossas APIs. Apesar dos exemplos apresentados terem sido simples, eles oferecem uma boa introdução à ferramenta. É importante destacar também que a documentação também é muito concisa, o que torna uma ferramenta relativamente fácil de ser usada e consultada.