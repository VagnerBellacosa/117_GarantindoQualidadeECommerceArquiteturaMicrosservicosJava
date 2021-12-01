

# Introdução a Testes Unitários com JUnit e Mockito no Android

## Criando testes unitários em uma aplicação utilizando MVVM Model-View View Model e DataBinding com Kotlin

[![Matheus Tadeu](https://miro.medium.com/fit/c/56/56/1*xCSnbE67xOvCgcvhvgLNnw.jpeg)](https://medium.com/@tadeumx1?source=post_page-----67104232b878-----------------------------------) -  [Matheus Tadeu](https://medium.com/@tadeumx1?source=post_page-----67104232b878-----------------------------------) . [Jul 7, 2019·13 min read](https://medium.com/@tadeumx1/introdução-a-testes-unitários-com-junit-e-mockito-no-android-67104232b878?source=post_page-----67104232b878-----------------------------------)







![img](https://miro.medium.com/max/1400/1*YXAFrnNR4nbm250edUy7YQ.png)

Cada vez mais é necessário, garantir confiabilidade para nossas aplicações, pois elas mudam a todo tempo sempre precisamos trocar algo, ou desenvolver um novo recurso, assim ter a certeza que o restante das funcionalidades que já existem, irão continuar funcionando de forma correta, é fundamental.

E exatamente para termos essa garantia existem os testes unitários, com eles podemos testar toda a lógica de nossa aplicação, garantindo assim que tudo esteja funcionando da forma correta, e que ao desenvolver uma nova feature, ela não acabe quebrando o restante do projeto, isso ocorre pois na maioria das vezes só estamos preocupados em testar o fluxo feliz, em que tudo funciona corretamente, e não nos atentamos em também testar os erros que podem ocorrer como por exemplo, conexão ruim durante o uso do aplicativo, o usuário fechar o aplicativo durante uma requisição na API, e por aí vai.

<iframe src="https://cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fgiphy.com%2Fembed%2Fl2JhEItioAxac7toQ%2Ftwitter%2Fiframe&amp;url=https%3A%2F%2Fgiphy.com%2Fgifs%2Fnfl-football-new-york-jets-l2JhEItioAxac7toQ&amp;image=https%3A%2F%2Fmedia.giphy.com%2Fmedia%2Fl2JhEItioAxac7toQ%2Fgiphy.gif&amp;key=a19fcc184b9711e1b4764040d3dc5c07&amp;type=text%2Fhtml&amp;schema=giphy" allowfullscreen="" frameborder="0" height="251" width="435" title="Celebrating New York Jets GIF by NFL - Find &amp; Share on GIPHY" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 392.361px;"></iframe>

Quando seus testes passam de primeira

**JUnit**

Para escrever **testes unitários no Android**, utlizamos o JUnit que é um framework open-source, criado por [Erich Gamma](https://pt.wikipedia.org/wiki/Erich_Gamma) e [Kent Beck](https://pt.wikipedia.org/wiki/Kent_Beck), que conta com as principais funcionalidades necessárias para esse fim.

Geralmente, esse framework já vem configurado no `build.gradle` no módulo app do projeto dessa forma, mas caso não tiver adicione essa linha

```
dependencies {
  
  // outras dependências da aplicação  // adicionar essa linha
  testImplementation 'junit:junit:4.12'

}
```

Lembrando que devemos adicionar o `JUnit` utilizando o `testImplementation `pois dessa forma, ele só vai ser usado em ambiente de teste, quando for preciso, e não vai ser carregado por exemplo quando o APK final for gerado, diminuindo seu tamanho.

**Diferenças entre o JUnit4 e JUnit5**

Como deve ter reparado estamos usando a versão 4 do JUnit. Apesar dela vir como padrão em projetos Android, recentemente (já faz um tempo hahaha) a sua nova versão chamada JUnit5 foi lançada, e trás algumas vantagens em relação a sua antiga versão como:

- Modularização em três pacotes, que te permite usar realmente o que é necessário no seu projeto
- Maior compatibilidade com novos recursos do Java 8 principalmente as lambdas functions
- Novas Annotations e Assertions que podem resolver muito dos seus problemas com versões anteriores do framework

Caso tenha interesse em saber mais sobre essa atualização, e a como utilizar em seu projeto recomendo a leitura de um artigo, disponível nesse [link](https://medium.com/android-dev-br/utilizando-junit-5-no-android-82d752708985) e também da sua [documentação](https://junit.org/junit5/docs/current/user-guide/#overview), que conta com um guia muito intuitivo.

Agora que já entendemos o porque de escrever testes unitários para nossos aplicativo, e já conhecemos a ferramenta que vamos utilizar no Android. O objetivo de um teste unitário é testar de forma isolada algum comportamento que existe no seu projeto, geralmente classes e métodos, um bom exemplo inicial, seria testar um método que soma dois valores:

Método

```
public int sum(int firstValue, int secondValue) {  
   
  return firstValue + secondValue; }
```

Teste do método

```
@Test 
public void plusOperationTest() {  assertEquals(4, sum(2, 2));}
```

Com isso está sendo testado o método `sum` que recebe dois números inteiros e retorna para o usuário a soma desses números, nesse teste os números passados são 2 e 2 assim o valor da soma deve ser 4, para validar esse resultado é usado o método assertEquals, passando o resultado esperado e chamando o método que queremos testar seu resultado, abaixo tem outra forma de testar a soma entre dois números mas dessa vez, já definidos no teste

```
@Test
public void sumTest() {  int value = 7
  int anotherValue = 3  int resultado = value + anotherValue  assertEquals(10, resultado)}
```

Nesse caso está sendo feito o teste da soma de dois valores, que é feita pelo método `sumTest` estamos declarando duas variáveis do tipo inteiro, que recebem os valores de 7 e 3 checando o resultado dessa soma, que deve ser 10, utilizando o método `assertEquals` do JUnit4, que recebe dois parâmetros e verifica caso eles são iguais, geralmente o primeiro é o valor que você espera da operação, e o segundo é o resultado da sua operação nesse caso, uma soma entre dois números inteiros.

Lembrando que para indicar, que aquele método é um teste unitário, é necessário utilizar a anotação `@ Test` do JUnit4, a sua forma de identificar testes.

Em alguns casos, quando a estrutura da classe ou método a ser testada é mais complexa e depende de outras classes ou objetos, podemos mockar esses objetos, com o objetivo de garantir que nosso teste, apenas estará testando um comportamento de forma isolada.

**Mockito**

Para mockar objetos em testes no Android, é utilizado o Mockito, uma biblioteca com o objetivo de facilitar o processo de mockar métodos ou classes dependentes no seu teste, criado em 2015 pela comunidade. É o framework de mock mais utilizado para a escrita de testes unitários em Java e também em aplicações Android.

Para configurar o Mockito em seu projeto é necessário, adicionar os pacotes necessários no arquivo `build.gradle` do módulo app no seu projeto:

```
dependencies {
  
  // outras dependências da aplicação  // Dependência principal do Mockito
  testImplementation 'org.mockito:mockito-core:2.28.2'  // Dependência do Mockito para testes no Android
  androidTestImplementation 'org.mockito:mockito-android:2.28.2'  // Dependência do Mockito para ser possível mockar classes e métodos constantes
  testImplementation 'org.mockito:mockito-inline:2.28.2'}
```

Depois disso, é só sicronizar o Gradle do projeto, e temos o Mockito configurado pronto para uso.

Agora que já temos tudo configurado no nosso projeto, podemos começar a escrever nossos testes 😃

**Conhecendo o aplicativo**

Como esse é um texto introdutório ao assunto preparei um exemplo bem simples, um aplicativo que faz o cálculo do combustível que um veículo irá gastar em uma viagem considerando a distância do local, preço do combustível e a autonomia do carro usado.

O aplicativo está funcionando dessa forma:

![img](https://miro.medium.com/freeze/max/36/1*RpqYFVxVtkUgqnccjp_Ixg.gif?q=20)

![img]()

Lembrando que esse projeto foi feito utilizando o padrão de arquitetura de apresentação, **Model-View View Model (MVVM)** e o principal benefício disso, é que a lógica de negócio de cada tela fica no ViewModel uma classe que é responsável, por ligar a interface com os dados utilizados na aplicação, com o uso desse modelo fica mais fácil escrever testes unitários no projeto, já que dividimos as responsabilidades entre a interface (View), lógica de negócio (ViewModel) e a representação dos dados utilizados no seu projeto (Model) para um melhor entendimento sobre esse padrão, recomendo a leitura de um artigo disponível nesse [link](https://medium.com/@soutoss/arquiteturas-em-android-mvvm-kotlin-retrofit-parte-1-2ac77c8a26)

Como o foco desse artigo são os testes unitários, somente vou apresentar o código do ViewModel desse projeto:

<iframe src="https://medium.com/media/f150bbcaaffaf681f21d7df3a1af477d" allowfullscreen="" frameborder="0" height="0" width="0" title="Post Introdução a Testes Unitários com JUnit e Mockito no Android" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 680px;"></iframe>

Esse é o ViewModel da Activity principal do projeto, estamos estendendo da classe `AndroidViewModel` que está no pacote do [Android Component](https://medium.com/android-dev-moz/aac1-bc22abbabecc)s da Google, temos os valores dos inputs usados na aplicação usando o [Android DataBinding](https://medium.com/android-dev-br/começando-com-android-data-binding-d7719333eecc) uma biblioteca faz parte do [Android JetPack](https://developer.android.com/jetpack?hl=pt-br), que tem por objetivo facilitar o [binding](https://developer.android.com/topic/libraries/data-binding?hl=pt-br) entre os layouts XML e código Java ou Kotlin, evitando assim o famigerado findViewById() e ainda, nesse caso temos a facilidade de chamar a função `handleCalculateButtonClick` diretamente da declaração do botão no XML dessa forma:

```
<?xml version="1.0" encoding="utf-8"?><layout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools">

    <data>

        <variable
                name="viewModel"
                type="com.example.mytrip.viewmodels.MainActivityViewModel" />

    </data>

<ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@color/colorLightGray">
    
    <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical">    ...      <Button
            android:id="@+id/buttonCalculate"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_margin="15dp"
            android:padding="20dp"
            android:text="@string/calcular"
            <!-- Chamada da função diretamente pelo XML -->
            android:onClick="@{() ->     viewModel.handleCalculateButtonClick()}"
            android:background="@drawable/round_btn"
            android:textAllCaps="true"
            android:textColor="@color/colorLightGray"
            android:textSize="20sp" />    ...    </LinearLayout>

</ScrollView>

</layout><!-- activity_main.xml -->
```

Quando o botão for clicado ele vai chamar a função `handleCalculateButtonClick()` responsável, por chamar a função `handleCalculate()` que vai validar os valores dos inputs utilizando a função `isValid()` que valida, caso realmente os campos foram preenchidos e também que o valor da autonomia deve ser maior que zero. Após isso é realizado o cálculo do valor de combustível que o veículo iria gastar em uma viagem, por exemplo.

**Testes unitários**

E nesse momento entram finalmente os testes unitários, vamos precisar checar o comportamento das funções no ViewModel, como por exemplo validar o cálculo do combustível e caso os valores dos inputs são números e estão corretos.

Os **testes unitários** em um projeto Android estão localizados no pacote `test` dentro de src assim sendo src/test

![img](https://miro.medium.com/max/60/1*Ml2-b_mQVBAIrPZ9LRFyqQ.png?q=20)

![img](https://miro.medium.com/max/565/1*Ml2-b_mQVBAIrPZ9LRFyqQ.png)

Já os **testes instrumentados** ou automatizados, que são outro tipo de testes para projetos Android, onde o objetivo é testar o comportamento da interface do aplicativo ficam localizados no pacote `androidTest` dentro de src assim sendo src/androidTest

Geralmente eles são feitos usando o [Espresso](https://developer.android.com/training/testing/espresso) que é um framework de testes fornecido pelo Android Testing Support Library. Ele contém as APIs necessárias para escrever testes de UI e simular as interações do usuário com o aplicativo.

![img](https://miro.medium.com/max/60/1*y9jIEnqeW4WKmqhzNgREGw.png?q=20)

![img](https://miro.medium.com/max/572/1*y9jIEnqeW4WKmqhzNgREGw.png)

Lembrando que esse tipo de teste é bem interessante e muito usado, não vou me aprofundar muito aqui, mas te recomendo estudar sobre a implementação desses testes, isso podemos deixar para um próximo artigo, já que é um assunto bem importante.

Nesse projeto criei os testes do ViewModel tanto em Kotlin e também Java para observar as diferenças, somente por questão de estudo mesmo, por isso temos dois arquivos de testes para o ViewModel.

Vamos criar a classe `MainActivityViewModelTest` dentro do pacote `test` para nela conter os testes unitários dos métodos do ViewModel, lembrando que é muito legal seguir esse padrão de nomenclatura para suas classes de teste sendo o nome da sua classe + test assim, como estamos fazendo.

<iframe src="https://medium.com/media/42b7eb4560e2cfc3e0ce39c58eea789d" allowfullscreen="" frameborder="0" height="3004" width="680" title="Post Introdução a Testes Unitários com JUnit e Mockito no Android" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 3003.99px;"></iframe>

Esse é o ViewModel com todos os testes, do aplicativo como já foi dito está sendo testado, desde de validação do input até o clique do botão e o cálculo do combustível.

Agora vamos analisando cada teste, e o que ele está realmente testando

```
@Before
fun setUp() {
    MockitoAnnotations.initMocks(this)
}
```

No início temos a função `setUp()` ela é responsável por inicializar os mocks do Mockito em cada teste que estiver nesse classe, e a annotation **Before** é quem dá o poder para a função fazer isso, toda função que estiver com essa marcação vai ser executada, antes de cada teste que estiver na classe de teste.

```
@Test
fun isValidReturnTrueTest() {

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("100")

    val preco = mainActivityViewModel.preco
    preco.set("30")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("15")


    assertTrue(mainActivityViewModel.isValid())

}
```

Já o teste `isValidReturnTrueTest()` valida caso estamos, preenchendo corretamente os inputs do aplicativo, sem deixar nenhum vazio, e com o valor da autonomia maior que zero, assim garantindo que posteriormente o cálculo do combustível, vai poder ser feito sem problemas. Importante atentar que estamos instanciando o nosso ViewModel e mockando a classe Application, que é necessária no seu funcionamento real, pois estamos utilizando o contexto do aplicativo dentro do ViewModel, para fazer o uso de Toast para exibir uma mensagem de erro, caso os campos forem preenchidos de forma incorreta.

Mas minha recomendação, é que sempre no possível, não utilizem o contexto da aplicação dentro do ViewModel, afim de deixa-ló mais limpo possível e somente com a lógica da tela. Só estou fazendo isso para demonstrar como é possível mockar uma classe ou qualquer outro objeto, que precisamos, para testar o comportamento da nossa classe, tanto que no código disponível no final do artigo não estou usando o contexto dessa forma e nem chamando o Toast dentro do ViewModel.

> Mais uma observação importante perante a esse teste, para mockar qualquer objeto, com o Mockito, é só utilizar o Mockito.mock(ObjetoQueVaiSerMockado) passando o objeto que irá ser mockado. Esse framework facilita muito esse processo

Após isso, é usada função `assertTrue` do JUnit que aceita um parâmetro, que pode ser uma variável, objeto, ou um retorno de uma função que é o nosso caso. Essa função valida caso o valor que foi passado é true, ao contrário, ou seja o valor sendo false, ele dá erro e assim o teste quebra.

```
@Test
fun isValidReturnFalseTest() {

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("")

    val preco = mainActivityViewModel.preco
    preco.set("")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("")

    assertFalse(mainActivityViewModel.isValid())

}
```

No teste `isValidReturnFalseTest()` é feito o fluxo ao contrário do anterior, que é quando o usuário não preencheu os campos. Assim também é necessário instanciar o ViewModel e atribuir o valor vazio para os inputs, e nesse caso utilizar a função `assertFalse()` do JUnit que é igual, a função que usamos anteriormente, mas valida caso o valor passado é igual a false, assim a função `isValid()` vai retornar false, e o teste irá passar sem problemas.

```
@Test
fun ValidHandleCalculation() {

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("30")

    val preco = mainActivityViewModel.preco
    preco.set("15")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("250")

    val resultado = mainActivityViewModel.resultado

    mainActivityViewModel.handleCalculate()

    assertEquals("Total: R$ 1.8", resultado.get())

}
```

Esse é um dos testes mais importantes do aplicativo, o `ValidHandleCalculation()` ele é responsável por testar caso o cálculo do combustível está sendo feito da maneira esperada, nele são preenchidos todos os inputs corretamente, e o método handleCalculate é chamado, onde o cálculo é feito, após isso o valor do resultado do cálculo, é obtido através da variável resultado que está ligada ao TextView que mostra esse valor no aplicativo utilizando o DataBinding no ViewModel. O valor esperado é de R$ 1.8 e para validar caso o valor que foi calculado está correto, está sendo usado a função `assertEquals()` do JUnit, que funciona dessa forma `assertEquals(expected: Any!, actual: Any!)` o primeiro parâmetro será o valor esperado para o teste funcionar, já o segundo é o valor da operação que está sendo testada, nesse teste o resultado do cálculo, caso os valores forem iguais o teste irá passar, caso o contrário vai quebrar, assim garantindo o funcionamento correto do aplicativo.

```
@Test
fun ValidHandleCalculationWrongNumber() {

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("asadsaddsasdsdadssd")

    val preco = mainActivityViewModel.preco
    preco.set("15")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("250")

    val resultado = mainActivityViewModel.resultado

    var numberFormatException = false

    try {
        mainActivityViewModel.handleCalculate()
        numberFormatException = false
    } catch (e : Exception) {
        numberFormatException = true
    }

    assertTrue(numberFormatException)

}
```

Esse teste `validHandleCalculationWrongNumber()` é responsável por verificar caso os valores inseridos nos inputs são números e não letras, ou qualquer outro tipo de caractere incorreto, para depois ser possível realizar o cálculo e o aplicativo funcionar da maneira correta.

Nesse teste estou colocando um texto no valor do input de distância, e números no restante, após isso dentro de um try catch assim como no código, do ViewModel tento realizar cálculo, é esperado que caia dentro do catch onde valido o erro usando a variável `numberFormatException` que agora tem o valor true, garantindo que caso qualquer um dos inputs tenha valores diferentes de números, o cálculo não seja feito.

```
@Test
fun handleCalculateButtonClickCallHandleCalculate() {

    // Test the handleCalculateButtonClick call HandleCalculate

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("30")

    val preco = mainActivityViewModel.preco
    preco.set("15")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("250")

    val spy = spy(mainActivityViewModel)

    spy.handleCalculateButtonClick()

    verify(spy, Mockito.times(1)).handleCalculate()

}
```

No último teste o `handleCalculateButtonClickCallHandleCalculate()` está sendo validado, se após o botão ser clicado e a função `handleCalculateButtonClick()` for chamada pelo Data Binding da classe, essa função vai chamar a função a `handleCalculate()` que de fato vai realizar o cálculo do combustível, como já foi dito.

**Mockito - Spy**

Nesse teste estamos usando alguns recursos interessantes que o Mockito nos oferece, o primeiro deles é o spy, esse é um conceito bem conhecido em testes unitários no geral, quando precisamos observar e copiar o comportamento de um objeto, sendo ele uma classe ou método para utilizar nos testes, usamos o spy, como se estivéssemos realmente espiando o objeto real no código. Nesse caso estamos fazendo o spy de nosso ViewModel e chamando a função `handleCalculateButtonClick()` simulando o clique do botão

**Mockito - Verify**

Como nesse caso está sendo feito o spy do nosso ViewModel podemos usar algumas funções do Mockito para verificar interações de métodos no nosso código, como por exemplo caso o método retornou o que foi esperado, caso o tipo de retorno do método está correto, e por aí vai, essas funções são a `when()` `doReturn()` e também a `verify()` que estamos utilizando nesse teste, após a chamar a função do clique do botão, vamos usar o verify dessa forma:

```
verify(spy, Mockito.times(1)).handleCalculate()
```

Nesse caso a função `verify()` está sendo usada para checar caso a função `handleCalculate()` que está no spy do ViewModel foi chamada uma vez, e é esperado que ela seja, porque a função responsável pelo clique do botão a `handleCalculateButtonClick()` foi chamada antes dela, com isso o objetivo do teste unitário foi concluído.

Com isso acabamos os testes unitários do nosso aplicativo usando o **JUnit** e o **Mockito** em projeto utilizando MVVM

Apesar de esse, ter sido um artigo focado para esse tipo de teste no Android, acredito que foram apresentados diversos conceitos muitos importantes como:

- As vantangens de usar um padrão de arquitetura com o objetivo de deixar seu projeto mais testável
- Porque realizar testes unitários
- A diferença com os testes intrumentados
- Utilizar o Mockito e suas principais funções
- O motivo de mockar objetos em testes
- Como o spy pode te ajudar em seus testes

E o mais importante fazer testes unitários na prática.

Resultado final

![img](https://miro.medium.com/max/60/1*oXJ5aNJBkeuMqC6gkrf8YA.png?q=20)

![img](https://miro.medium.com/max/630/1*oXJ5aNJBkeuMqC6gkrf8YA.png)

O projeto está disponível nesse [repositório](https://github.com/tadeumx1/MyTripMVVMAndroid) no GitHub e qualquer dúvida que tiverem, ou quiserem acrescentar algo, é só deixar um comentário.

Também não esqueça de me acompanhar nas redes sociais, para gente trocar aquela ideia

[matheustadeu.com](https://matheustadeu.com/)

[www.linkedin.com/in/matheus-tadeu/](https://www.linkedin.com/in/matheus-tadeu/)

**Referências**

[Criando testes para seu aplicativo Android - AndroidProNo mundo do desenvolvimento de softwares, sempre há situações em que acontecem coisas que nós não prevemos ou até mesmo…www.androidpro.com.br](https://www.androidpro.com.br/blog/desenvolvimento-android/criando-testes-para-seu-aplicativo-android/)

[JUnit 5 vs JUnit 4 - HowToDoInJavaJUnit 5 aims to adapt java 8 style of coding and to be more robust and flexible than JUnit 4. In this post, JUnit 5 vs…howtodoinjava.com](https://howtodoinjava.com/junit5/junit-5-vs-junit-4/)

[Testes em Android - Parte I: Por onde começar?Fala, Comunidade! Este post é o primeiro de uma série sobre testes em Android. Você aprenderá conceitos essenciais…tasafo.wordpress.com](https://tasafo.wordpress.com/2017/01/26/testes-em-android-parte-i-por-onde-comecar/)

[Unit Testing with JUnit - TutorialIn general it it safe to ignore trivial code. For example, it is typical useless to write tests for getter and setter…www.vogella.com](https://www.vogella.com/tutorials/JUnit/article.html)

[Android testing: Unit testing (Part 1) - Android development and testingToday I would like the series of articles about Android Testing. I'm planning create articles about different type of…alexzh.com](https://alexzh.com/2016/03/24/android-testing-unit-testing/)

[How to Use Mockito in Android - DZone MobileLearn how to integrate the Mockito autmated testing framework with your mobile app and use the mock and spy methods to…dzone.com](https://dzone.com/articles/how-to-use-mockito-in-android)

[Android Testing with JUnit & mockitoTips, study notes, and mini-code samplesmedium.com](https://medium.com/@Shahawi/android-testing-with-junit-mockito-d40b5f6c68a7)

Muito obrigado pela atenção pessoal e espero que tenham gostado.

[Matheus Tadeu](https://medium.com/@tadeumx1?source=post_sidebar--------------------------post_sidebar--------------)

Software Developer at Midway (RCHLO) and a EDM Lover

Follow



MATHEUS TADEU FOLLOWS

- [![Iran Junior | Dev Mobile](https://miro.medium.com/fit/c/18/18/1*sAwB2zWASyckJDO0VWTWfA.png)](https://iranjunior.medium.com/?source=blogrolls_sidebar-----67104232b878-----------------------------------)

  [Iran Junior | Dev Mobile](https://iranjunior.medium.com/?source=blogrolls_sidebar-----67104232b878-----------------------------------)

- [![Charleston A.](https://miro.medium.com/fit/c/18/18/1*f8PmqAYOQ-mm2mXtb2c4kw.jpeg)](https://charleston-anjos.medium.com/?source=blogrolls_sidebar-----67104232b878-----------------------------------)

  [Charleston A.](https://charleston-anjos.medium.com/?source=blogrolls_sidebar-----67104232b878-----------------------------------)

- [![Pedro Vallese](https://miro.medium.com/fit/c/18/18/2*t416Y7mRkOCBjHNTU2eF_g.jpeg)](https://pedrovallese.medium.com/?source=blogrolls_sidebar-----67104232b878-----------------------------------)

  [Pedro Vallese](https://pedrovallese.medium.com/?source=blogrolls_sidebar-----67104232b878-----------------------------------)

- [![Velrino](https://miro.medium.com/fit/c/18/18/0*K3YuuAGnplDVXzcg.)](https://medium.com/@velrino?source=blogrolls_sidebar-----67104232b878-----------------------------------)

  [Velrino](https://medium.com/@velrino?source=blogrolls_sidebar-----67104232b878-----------------------------------)

- [![Laura Beatris](https://miro.medium.com/fit/c/18/18/2*1y-Aw2AOc6B2i2iPvrdJfQ.png)](https://medium.com/@laurabeatris?source=blogrolls_sidebar-----67104232b878-----------------------------------)

  [Laura Beatris](https://medium.com/@laurabeatris?source=blogrolls_sidebar-----67104232b878-----------------------------------)

[See all (28)](https://medium.com/@tadeumx1/following?source=blogrolls_sidebar-----67104232b878-----------------------------------)



80





Thanks to Marcos Campos. 

80









- [Android](https://medium.com/tag/android)
- [Android Studio](https://medium.com/tag/android-studio)
- [Android App Development](https://medium.com/tag/android-app-development)
- [AndroidDev](https://medium.com/tag/androiddev)
- [Unit Testing](https://medium.com/tag/unit-testing)

## [More from Matheus Tadeu](https://medium.com/@tadeumx1?source=follow_footer-----67104232b878-----------------------------------)

Follow



Software Developer at Midway (RCHLO) and a EDM Lover

[Published in **Nerdzão/Nerdgirlz**](https://medium.com/nerdzao?source=follow_footer-----67104232b878----0-------------------------------)[·Feb 11, 2019](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?source=follow_footer-----67104232b878----0-------------------------------)[Leitura de QRCode no React Native](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?source=follow_footer-----67104232b878----0-------------------------------)Criando uma aplicação para a leitura de QRCode, integrada com uma WebView e navegador utilizando Linking[![img](https://miro.medium.com/max/630/1*HkfIjUcLoPbI_oUhbFHm3w.jpeg)](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?source=follow_footer-----67104232b878----0-------------------------------)Nos dias hoje, muitos aplicativos utilizam os chamados QRCode de diversas formas: anúncios, propagandas, campanhas de marketing, e até para obter mais informações sobre monumentos e obras em espaços públicos ou museus.Resumindo, um QRCode é um código de barras bidimensional, que pode ser facilmente escaneado usando a maioria dos…[Read more · 5 min read](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?readmore=1&source=follow_footer-----67104232b878----0-------------------------------)227[2](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?responsesOpen=true&source=follow_footer-----67104232b878----0-------------------------------)[Published in **Nerdzão/Nerdgirlz**](https://medium.com/nerdzao?source=follow_footer-----67104232b878----1-------------------------------)[·Jan 7, 2019](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?source=follow_footer-----67104232b878----1-------------------------------)[Utilizando Rotas com a Google Maps API no React Native](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?source=follow_footer-----67104232b878----1-------------------------------)Criando uma aplicação para o cálculo de rotas em mapas e integrando com o Google Maps[![img](https://miro.medium.com/max/630/1*RCI6zOXWkRWKfIUvHtNWjw.png)](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?source=follow_footer-----67104232b878----1-------------------------------)Atualmente não é difícil ver diversos aplicativos utilizando mapas integrados com a Google Maps API com ela podemos, fazer desde aplicativos mais simples que listam lugares, até mais complexos como por exemplo aqueles de carros compartilhados.O último tipo citado usa um recurso interessante disponível na Maps API, o cálculo…[Read more · 7 min read](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?readmore=1&source=follow_footer-----67104232b878----1-------------------------------)261[6](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?responsesOpen=true&source=follow_footer-----67104232b878----1-------------------------------)[Dec 10, 2018](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?source=follow_footer-----67104232b878----2-------------------------------)[Utilizando Mapas no React Native](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?source=follow_footer-----67104232b878----2-------------------------------)Criando uma aplicação com mapa nativo da Google Maps API[![img](https://miro.medium.com/max/630/1*nzkBi3V8EHiu9CjsfwQHyA.png)](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?source=follow_footer-----67104232b878----2-------------------------------)Hoje em dia não é difícil ver diversos aplicativos utilizando mapas integrados com a Google Maps API com ela podemos, fazer desde aplicativos mais simples que listam lugares, até mais complexos como por exemplo aqueles de carros compartilhados.Irei fazer uma série de “artigos” mostrando como podemos usar as mais…[Read more · 8 min read](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?readmore=1&source=follow_footer-----67104232b878----2-------------------------------)192[2](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?responsesOpen=true&source=follow_footer-----67104232b878----2-------------------------------)



[About](https://medium.com/about?autoplay=1&source=post_page-----67104232b878-----------------------------------)

[Write](https://medium.com/new-story?source=post_page-----67104232b878-----------------------------------)

[Help](https://help.medium.com/hc/en-us?source=post_page-----67104232b878-----------------------------------)

[Legal](https://policy.medium.com/medium-terms-of-service-9db0094a1e0f?source=post_page-----67104232b878-----------------------------------)[Matheus Tadeu](https://medium.com/@tadeumx1?source=post_page-----67104232b878-----------------------------------)

[105 Followers](https://medium.com/@tadeumx1/followers?source=post_page-----67104232b878-----------------------------------)[About](https://medium.com/@tadeumx1/about?source=post_page-----67104232b878-----------------------------------)Follow





[Upgrade](https://medium.com/plans?source=upgrade_membership---nav_full-------------------------------------)







# Introdução a Testes Unitários com JUnit e Mockito no Android

## Criando testes unitários em uma aplicação utilizando MVVM Model-View View Model e DataBinding com Kotlin

[![Matheus Tadeu](https://miro.medium.com/fit/c/56/56/1*xCSnbE67xOvCgcvhvgLNnw.jpeg)](https://medium.com/@tadeumx1?source=post_page-----67104232b878-----------------------------------)

[Matheus Tadeu](https://medium.com/@tadeumx1?source=post_page-----67104232b878-----------------------------------)

[Jul 7, 2019·13 min read](https://medium.com/@tadeumx1/introdução-a-testes-unitários-com-junit-e-mockito-no-android-67104232b878?source=post_page-----67104232b878-----------------------------------)







![img](https://miro.medium.com/max/1400/1*YXAFrnNR4nbm250edUy7YQ.png)

Cada vez mais é necessário, garantir confiabilidade para nossas aplicações, pois elas mudam a todo tempo sempre precisamos trocar algo, ou desenvolver um novo recurso, assim ter a certeza que o restante das funcionalidades que já existem, irão continuar funcionando de forma correta, é fundamental.

E exatamente para termos essa garantia existem os testes unitários, com eles podemos testar toda a lógica de nossa aplicação, garantindo assim que tudo esteja funcionando da forma correta, e que ao desenvolver uma nova feature, ela não acabe quebrando o restante do projeto, isso ocorre pois na maioria das vezes só estamos preocupados em testar o fluxo feliz, em que tudo funciona corretamente, e não nos atentamos em também testar os erros que podem ocorrer como por exemplo, conexão ruim durante o uso do aplicativo, o usuário fechar o aplicativo durante uma requisição na API, e por aí vai.

<iframe src="https://cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fgiphy.com%2Fembed%2Fl2JhEItioAxac7toQ%2Ftwitter%2Fiframe&amp;url=https%3A%2F%2Fgiphy.com%2Fgifs%2Fnfl-football-new-york-jets-l2JhEItioAxac7toQ&amp;image=https%3A%2F%2Fmedia.giphy.com%2Fmedia%2Fl2JhEItioAxac7toQ%2Fgiphy.gif&amp;key=a19fcc184b9711e1b4764040d3dc5c07&amp;type=text%2Fhtml&amp;schema=giphy" allowfullscreen="" frameborder="0" height="251" width="435" title="Celebrating New York Jets GIF by NFL - Find &amp; Share on GIPHY" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 392.361px;"></iframe>

Quando seus testes passam de primeira

**JUnit**

Para escrever **testes unitários no Android**, utlizamos o JUnit que é um framework open-source, criado por [Erich Gamma](https://pt.wikipedia.org/wiki/Erich_Gamma) e [Kent Beck](https://pt.wikipedia.org/wiki/Kent_Beck), que conta com as principais funcionalidades necessárias para esse fim.

Geralmente, esse framework já vem configurado no `build.gradle` no módulo app do projeto dessa forma, mas caso não tiver adicione essa linha

```
dependencies {
  
  // outras dependências da aplicação  // adicionar essa linha
  testImplementation 'junit:junit:4.12'

}
```

Lembrando que devemos adicionar o `JUnit` utilizando o `testImplementation `pois dessa forma, ele só vai ser usado em ambiente de teste, quando for preciso, e não vai ser carregado por exemplo quando o APK final for gerado, diminuindo seu tamanho.

**Diferenças entre o JUnit4 e JUnit5**

Como deve ter reparado estamos usando a versão 4 do JUnit. Apesar dela vir como padrão em projetos Android, recentemente (já faz um tempo hahaha) a sua nova versão chamada JUnit5 foi lançada, e trás algumas vantagens em relação a sua antiga versão como:

- Modularização em três pacotes, que te permite usar realmente o que é necessário no seu projeto
- Maior compatibilidade com novos recursos do Java 8 principalmente as lambdas functions
- Novas Annotations e Assertions que podem resolver muito dos seus problemas com versões anteriores do framework

Caso tenha interesse em saber mais sobre essa atualização, e a como utilizar em seu projeto recomendo a leitura de um artigo, disponível nesse [link](https://medium.com/android-dev-br/utilizando-junit-5-no-android-82d752708985) e também da sua [documentação](https://junit.org/junit5/docs/current/user-guide/#overview), que conta com um guia muito intuitivo.

Agora que já entendemos o porque de escrever testes unitários para nossos aplicativo, e já conhecemos a ferramenta que vamos utilizar no Android. O objetivo de um teste unitário é testar de forma isolada algum comportamento que existe no seu projeto, geralmente classes e métodos, um bom exemplo inicial, seria testar um método que soma dois valores:

Método

```
public int sum(int firstValue, int secondValue) {  
   
  return firstValue + secondValue; }
```

Teste do método

```
@Test 
public void plusOperationTest() {  assertEquals(4, sum(2, 2));}
```

Com isso está sendo testado o método `sum` que recebe dois números inteiros e retorna para o usuário a soma desses números, nesse teste os números passados são 2 e 2 assim o valor da soma deve ser 4, para validar esse resultado é usado o método assertEquals, passando o resultado esperado e chamando o método que queremos testar seu resultado, abaixo tem outra forma de testar a soma entre dois números mas dessa vez, já definidos no teste

```
@Test
public void sumTest() {  int value = 7
  int anotherValue = 3  int resultado = value + anotherValue  assertEquals(10, resultado)}
```

Nesse caso está sendo feito o teste da soma de dois valores, que é feita pelo método `sumTest` estamos declarando duas variáveis do tipo inteiro, que recebem os valores de 7 e 3 checando o resultado dessa soma, que deve ser 10, utilizando o método `assertEquals` do JUnit4, que recebe dois parâmetros e verifica caso eles são iguais, geralmente o primeiro é o valor que você espera da operação, e o segundo é o resultado da sua operação nesse caso, uma soma entre dois números inteiros.

Lembrando que para indicar, que aquele método é um teste unitário, é necessário utilizar a anotação `@ Test` do JUnit4, a sua forma de identificar testes.

Em alguns casos, quando a estrutura da classe ou método a ser testada é mais complexa e depende de outras classes ou objetos, podemos mockar esses objetos, com o objetivo de garantir que nosso teste, apenas estará testando um comportamento de forma isolada.

**Mockito**

Para mockar objetos em testes no Android, é utilizado o Mockito, uma biblioteca com o objetivo de facilitar o processo de mockar métodos ou classes dependentes no seu teste, criado em 2015 pela comunidade. É o framework de mock mais utilizado para a escrita de testes unitários em Java e também em aplicações Android.

Para configurar o Mockito em seu projeto é necessário, adicionar os pacotes necessários no arquivo `build.gradle` do módulo app no seu projeto:

```
dependencies {
  
  // outras dependências da aplicação  // Dependência principal do Mockito
  testImplementation 'org.mockito:mockito-core:2.28.2'  // Dependência do Mockito para testes no Android
  androidTestImplementation 'org.mockito:mockito-android:2.28.2'  // Dependência do Mockito para ser possível mockar classes e métodos constantes
  testImplementation 'org.mockito:mockito-inline:2.28.2'}
```

Depois disso, é só sicronizar o Gradle do projeto, e temos o Mockito configurado pronto para uso.

Agora que já temos tudo configurado no nosso projeto, podemos começar a escrever nossos testes 😃

**Conhecendo o aplicativo**

Como esse é um texto introdutório ao assunto preparei um exemplo bem simples, um aplicativo que faz o cálculo do combustível que um veículo irá gastar em uma viagem considerando a distância do local, preço do combustível e a autonomia do carro usado.

O aplicativo está funcionando dessa forma:

![img](https://miro.medium.com/freeze/max/36/1*RpqYFVxVtkUgqnccjp_Ixg.gif?q=20)

![img]()

Lembrando que esse projeto foi feito utilizando o padrão de arquitetura de apresentação, **Model-View View Model (MVVM)** e o principal benefício disso, é que a lógica de negócio de cada tela fica no ViewModel uma classe que é responsável, por ligar a interface com os dados utilizados na aplicação, com o uso desse modelo fica mais fácil escrever testes unitários no projeto, já que dividimos as responsabilidades entre a interface (View), lógica de negócio (ViewModel) e a representação dos dados utilizados no seu projeto (Model) para um melhor entendimento sobre esse padrão, recomendo a leitura de um artigo disponível nesse [link](https://medium.com/@soutoss/arquiteturas-em-android-mvvm-kotlin-retrofit-parte-1-2ac77c8a26)

Como o foco desse artigo são os testes unitários, somente vou apresentar o código do ViewModel desse projeto:

<iframe src="https://medium.com/media/f150bbcaaffaf681f21d7df3a1af477d" allowfullscreen="" frameborder="0" height="0" width="0" title="Post Introdução a Testes Unitários com JUnit e Mockito no Android" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 680px;"></iframe>

Esse é o ViewModel da Activity principal do projeto, estamos estendendo da classe `AndroidViewModel` que está no pacote do [Android Component](https://medium.com/android-dev-moz/aac1-bc22abbabecc)s da Google, temos os valores dos inputs usados na aplicação usando o [Android DataBinding](https://medium.com/android-dev-br/começando-com-android-data-binding-d7719333eecc) uma biblioteca faz parte do [Android JetPack](https://developer.android.com/jetpack?hl=pt-br), que tem por objetivo facilitar o [binding](https://developer.android.com/topic/libraries/data-binding?hl=pt-br) entre os layouts XML e código Java ou Kotlin, evitando assim o famigerado findViewById() e ainda, nesse caso temos a facilidade de chamar a função `handleCalculateButtonClick` diretamente da declaração do botão no XML dessa forma:

```
<?xml version="1.0" encoding="utf-8"?><layout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools">

    <data>

        <variable
                name="viewModel"
                type="com.example.mytrip.viewmodels.MainActivityViewModel" />

    </data>

<ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@color/colorLightGray">
    
    <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical">    ...      <Button
            android:id="@+id/buttonCalculate"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_margin="15dp"
            android:padding="20dp"
            android:text="@string/calcular"
            <!-- Chamada da função diretamente pelo XML -->
            android:onClick="@{() ->     viewModel.handleCalculateButtonClick()}"
            android:background="@drawable/round_btn"
            android:textAllCaps="true"
            android:textColor="@color/colorLightGray"
            android:textSize="20sp" />    ...    </LinearLayout>

</ScrollView>

</layout><!-- activity_main.xml -->
```

Quando o botão for clicado ele vai chamar a função `handleCalculateButtonClick()` responsável, por chamar a função `handleCalculate()` que vai validar os valores dos inputs utilizando a função `isValid()` que valida, caso realmente os campos foram preenchidos e também que o valor da autonomia deve ser maior que zero. Após isso é realizado o cálculo do valor de combustível que o veículo iria gastar em uma viagem, por exemplo.

**Testes unitários**

E nesse momento entram finalmente os testes unitários, vamos precisar checar o comportamento das funções no ViewModel, como por exemplo validar o cálculo do combustível e caso os valores dos inputs são números e estão corretos.

Os **testes unitários** em um projeto Android estão localizados no pacote `test` dentro de src assim sendo src/test

![img](https://miro.medium.com/max/60/1*Ml2-b_mQVBAIrPZ9LRFyqQ.png?q=20)

![img](https://miro.medium.com/max/565/1*Ml2-b_mQVBAIrPZ9LRFyqQ.png)

Já os **testes instrumentados** ou automatizados, que são outro tipo de testes para projetos Android, onde o objetivo é testar o comportamento da interface do aplicativo ficam localizados no pacote `androidTest` dentro de src assim sendo src/androidTest

Geralmente eles são feitos usando o [Espresso](https://developer.android.com/training/testing/espresso) que é um framework de testes fornecido pelo Android Testing Support Library. Ele contém as APIs necessárias para escrever testes de UI e simular as interações do usuário com o aplicativo.

![img](https://miro.medium.com/max/60/1*y9jIEnqeW4WKmqhzNgREGw.png?q=20)

![img](https://miro.medium.com/max/572/1*y9jIEnqeW4WKmqhzNgREGw.png)

Lembrando que esse tipo de teste é bem interessante e muito usado, não vou me aprofundar muito aqui, mas te recomendo estudar sobre a implementação desses testes, isso podemos deixar para um próximo artigo, já que é um assunto bem importante.

Nesse projeto criei os testes do ViewModel tanto em Kotlin e também Java para observar as diferenças, somente por questão de estudo mesmo, por isso temos dois arquivos de testes para o ViewModel.

Vamos criar a classe `MainActivityViewModelTest` dentro do pacote `test` para nela conter os testes unitários dos métodos do ViewModel, lembrando que é muito legal seguir esse padrão de nomenclatura para suas classes de teste sendo o nome da sua classe + test assim, como estamos fazendo.

<iframe src="https://medium.com/media/42b7eb4560e2cfc3e0ce39c58eea789d" allowfullscreen="" frameborder="0" height="3004" width="680" title="Post Introdução a Testes Unitários com JUnit e Mockito no Android" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 3003.99px;"></iframe>

Esse é o ViewModel com todos os testes, do aplicativo como já foi dito está sendo testado, desde de validação do input até o clique do botão e o cálculo do combustível.

Agora vamos analisando cada teste, e o que ele está realmente testando

```
@Before
fun setUp() {
    MockitoAnnotations.initMocks(this)
}
```

No início temos a função `setUp()` ela é responsável por inicializar os mocks do Mockito em cada teste que estiver nesse classe, e a annotation **Before** é quem dá o poder para a função fazer isso, toda função que estiver com essa marcação vai ser executada, antes de cada teste que estiver na classe de teste.

```
@Test
fun isValidReturnTrueTest() {

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("100")

    val preco = mainActivityViewModel.preco
    preco.set("30")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("15")


    assertTrue(mainActivityViewModel.isValid())

}
```

Já o teste `isValidReturnTrueTest()` valida caso estamos, preenchendo corretamente os inputs do aplicativo, sem deixar nenhum vazio, e com o valor da autonomia maior que zero, assim garantindo que posteriormente o cálculo do combustível, vai poder ser feito sem problemas. Importante atentar que estamos instanciando o nosso ViewModel e mockando a classe Application, que é necessária no seu funcionamento real, pois estamos utilizando o contexto do aplicativo dentro do ViewModel, para fazer o uso de Toast para exibir uma mensagem de erro, caso os campos forem preenchidos de forma incorreta.

Mas minha recomendação, é que sempre no possível, não utilizem o contexto da aplicação dentro do ViewModel, afim de deixa-ló mais limpo possível e somente com a lógica da tela. Só estou fazendo isso para demonstrar como é possível mockar uma classe ou qualquer outro objeto, que precisamos, para testar o comportamento da nossa classe, tanto que no código disponível no final do artigo não estou usando o contexto dessa forma e nem chamando o Toast dentro do ViewModel.

> Mais uma observação importante perante a esse teste, para mockar qualquer objeto, com o Mockito, é só utilizar o Mockito.mock(ObjetoQueVaiSerMockado) passando o objeto que irá ser mockado. Esse framework facilita muito esse processo

Após isso, é usada função `assertTrue` do JUnit que aceita um parâmetro, que pode ser uma variável, objeto, ou um retorno de uma função que é o nosso caso. Essa função valida caso o valor que foi passado é true, ao contrário, ou seja o valor sendo false, ele dá erro e assim o teste quebra.

```
@Test
fun isValidReturnFalseTest() {

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("")

    val preco = mainActivityViewModel.preco
    preco.set("")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("")

    assertFalse(mainActivityViewModel.isValid())

}
```

No teste `isValidReturnFalseTest()` é feito o fluxo ao contrário do anterior, que é quando o usuário não preencheu os campos. Assim também é necessário instanciar o ViewModel e atribuir o valor vazio para os inputs, e nesse caso utilizar a função `assertFalse()` do JUnit que é igual, a função que usamos anteriormente, mas valida caso o valor passado é igual a false, assim a função `isValid()` vai retornar false, e o teste irá passar sem problemas.

```
@Test
fun ValidHandleCalculation() {

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("30")

    val preco = mainActivityViewModel.preco
    preco.set("15")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("250")

    val resultado = mainActivityViewModel.resultado

    mainActivityViewModel.handleCalculate()

    assertEquals("Total: R$ 1.8", resultado.get())

}
```

Esse é um dos testes mais importantes do aplicativo, o `ValidHandleCalculation()` ele é responsável por testar caso o cálculo do combustível está sendo feito da maneira esperada, nele são preenchidos todos os inputs corretamente, e o método handleCalculate é chamado, onde o cálculo é feito, após isso o valor do resultado do cálculo, é obtido através da variável resultado que está ligada ao TextView que mostra esse valor no aplicativo utilizando o DataBinding no ViewModel. O valor esperado é de R$ 1.8 e para validar caso o valor que foi calculado está correto, está sendo usado a função `assertEquals()` do JUnit, que funciona dessa forma `assertEquals(expected: Any!, actual: Any!)` o primeiro parâmetro será o valor esperado para o teste funcionar, já o segundo é o valor da operação que está sendo testada, nesse teste o resultado do cálculo, caso os valores forem iguais o teste irá passar, caso o contrário vai quebrar, assim garantindo o funcionamento correto do aplicativo.

```
@Test
fun ValidHandleCalculationWrongNumber() {

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("asadsaddsasdsdadssd")

    val preco = mainActivityViewModel.preco
    preco.set("15")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("250")

    val resultado = mainActivityViewModel.resultado

    var numberFormatException = false

    try {
        mainActivityViewModel.handleCalculate()
        numberFormatException = false
    } catch (e : Exception) {
        numberFormatException = true
    }

    assertTrue(numberFormatException)

}
```

Esse teste `validHandleCalculationWrongNumber()` é responsável por verificar caso os valores inseridos nos inputs são números e não letras, ou qualquer outro tipo de caractere incorreto, para depois ser possível realizar o cálculo e o aplicativo funcionar da maneira correta.

Nesse teste estou colocando um texto no valor do input de distância, e números no restante, após isso dentro de um try catch assim como no código, do ViewModel tento realizar cálculo, é esperado que caia dentro do catch onde valido o erro usando a variável `numberFormatException` que agora tem o valor true, garantindo que caso qualquer um dos inputs tenha valores diferentes de números, o cálculo não seja feito.

```
@Test
fun handleCalculateButtonClickCallHandleCalculate() {

    // Test the handleCalculateButtonClick call HandleCalculate

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("30")

    val preco = mainActivityViewModel.preco
    preco.set("15")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("250")

    val spy = spy(mainActivityViewModel)

    spy.handleCalculateButtonClick()

    verify(spy, Mockito.times(1)).handleCalculate()

}
```

No último teste o `handleCalculateButtonClickCallHandleCalculate()` está sendo validado, se após o botão ser clicado e a função `handleCalculateButtonClick()` for chamada pelo Data Binding da classe, essa função vai chamar a função a `handleCalculate()` que de fato vai realizar o cálculo do combustível, como já foi dito.

**Mockito - Spy**

Nesse teste estamos usando alguns recursos interessantes que o Mockito nos oferece, o primeiro deles é o spy, esse é um conceito bem conhecido em testes unitários no geral, quando precisamos observar e copiar o comportamento de um objeto, sendo ele uma classe ou método para utilizar nos testes, usamos o spy, como se estivéssemos realmente espiando o objeto real no código. Nesse caso estamos fazendo o spy de nosso ViewModel e chamando a função `handleCalculateButtonClick()` simulando o clique do botão

**Mockito - Verify**

Como nesse caso está sendo feito o spy do nosso ViewModel podemos usar algumas funções do Mockito para verificar interações de métodos no nosso código, como por exemplo caso o método retornou o que foi esperado, caso o tipo de retorno do método está correto, e por aí vai, essas funções são a `when()` `doReturn()` e também a `verify()` que estamos utilizando nesse teste, após a chamar a função do clique do botão, vamos usar o verify dessa forma:

```
verify(spy, Mockito.times(1)).handleCalculate()
```

Nesse caso a função `verify()` está sendo usada para checar caso a função `handleCalculate()` que está no spy do ViewModel foi chamada uma vez, e é esperado que ela seja, porque a função responsável pelo clique do botão a `handleCalculateButtonClick()` foi chamada antes dela, com isso o objetivo do teste unitário foi concluído.

Com isso acabamos os testes unitários do nosso aplicativo usando o **JUnit** e o **Mockito** em projeto utilizando MVVM

Apesar de esse, ter sido um artigo focado para esse tipo de teste no Android, acredito que foram apresentados diversos conceitos muitos importantes como:

- As vantangens de usar um padrão de arquitetura com o objetivo de deixar seu projeto mais testável
- Porque realizar testes unitários
- A diferença com os testes intrumentados
- Utilizar o Mockito e suas principais funções
- O motivo de mockar objetos em testes
- Como o spy pode te ajudar em seus testes

E o mais importante fazer testes unitários na prática.

Resultado final

![img](https://miro.medium.com/max/60/1*oXJ5aNJBkeuMqC6gkrf8YA.png?q=20)

![img](https://miro.medium.com/max/630/1*oXJ5aNJBkeuMqC6gkrf8YA.png)

O projeto está disponível nesse [repositório](https://github.com/tadeumx1/MyTripMVVMAndroid) no GitHub e qualquer dúvida que tiverem, ou quiserem acrescentar algo, é só deixar um comentário.

Também não esqueça de me acompanhar nas redes sociais, para gente trocar aquela ideia

[matheustadeu.com](https://matheustadeu.com/)

[www.linkedin.com/in/matheus-tadeu/](https://www.linkedin.com/in/matheus-tadeu/)

**Referências**

[Criando testes para seu aplicativo Android - AndroidProNo mundo do desenvolvimento de softwares, sempre há situações em que acontecem coisas que nós não prevemos ou até mesmo…www.androidpro.com.br](https://www.androidpro.com.br/blog/desenvolvimento-android/criando-testes-para-seu-aplicativo-android/)

[JUnit 5 vs JUnit 4 - HowToDoInJavaJUnit 5 aims to adapt java 8 style of coding and to be more robust and flexible than JUnit 4. In this post, JUnit 5 vs…howtodoinjava.com](https://howtodoinjava.com/junit5/junit-5-vs-junit-4/)

[Testes em Android - Parte I: Por onde começar?Fala, Comunidade! Este post é o primeiro de uma série sobre testes em Android. Você aprenderá conceitos essenciais…tasafo.wordpress.com](https://tasafo.wordpress.com/2017/01/26/testes-em-android-parte-i-por-onde-comecar/)

[Unit Testing with JUnit - TutorialIn general it it safe to ignore trivial code. For example, it is typical useless to write tests for getter and setter…www.vogella.com](https://www.vogella.com/tutorials/JUnit/article.html)

[Android testing: Unit testing (Part 1) - Android development and testingToday I would like the series of articles about Android Testing. I'm planning create articles about different type of…alexzh.com](https://alexzh.com/2016/03/24/android-testing-unit-testing/)

[How to Use Mockito in Android - DZone MobileLearn how to integrate the Mockito autmated testing framework with your mobile app and use the mock and spy methods to…dzone.com](https://dzone.com/articles/how-to-use-mockito-in-android)

[Android Testing with JUnit & mockitoTips, study notes, and mini-code samplesmedium.com](https://medium.com/@Shahawi/android-testing-with-junit-mockito-d40b5f6c68a7)

Muito obrigado pela atenção pessoal e espero que tenham gostado.

[Matheus Tadeu](https://medium.com/@tadeumx1?source=post_sidebar--------------------------post_sidebar--------------)

Software Developer at Midway (RCHLO) and a EDM Lover

Follow



MATHEUS TADEU FOLLOWS

- [![Iran Junior | Dev Mobile](https://miro.medium.com/fit/c/18/18/1*sAwB2zWASyckJDO0VWTWfA.png)](https://iranjunior.medium.com/?source=blogrolls_sidebar-----67104232b878-----------------------------------)

  [Iran Junior | Dev Mobile](https://iranjunior.medium.com/?source=blogrolls_sidebar-----67104232b878-----------------------------------)

- [![Charleston A.](https://miro.medium.com/fit/c/18/18/1*f8PmqAYOQ-mm2mXtb2c4kw.jpeg)](https://charleston-anjos.medium.com/?source=blogrolls_sidebar-----67104232b878-----------------------------------)

  [Charleston A.](https://charleston-anjos.medium.com/?source=blogrolls_sidebar-----67104232b878-----------------------------------)

- [![Pedro Vallese](https://miro.medium.com/fit/c/18/18/2*t416Y7mRkOCBjHNTU2eF_g.jpeg)](https://pedrovallese.medium.com/?source=blogrolls_sidebar-----67104232b878-----------------------------------)

  [Pedro Vallese](https://pedrovallese.medium.com/?source=blogrolls_sidebar-----67104232b878-----------------------------------)

- [![Velrino](https://miro.medium.com/fit/c/18/18/0*K3YuuAGnplDVXzcg.)](https://medium.com/@velrino?source=blogrolls_sidebar-----67104232b878-----------------------------------)

  [Velrino](https://medium.com/@velrino?source=blogrolls_sidebar-----67104232b878-----------------------------------)

- [![Laura Beatris](https://miro.medium.com/fit/c/18/18/2*1y-Aw2AOc6B2i2iPvrdJfQ.png)](https://medium.com/@laurabeatris?source=blogrolls_sidebar-----67104232b878-----------------------------------)

  [Laura Beatris](https://medium.com/@laurabeatris?source=blogrolls_sidebar-----67104232b878-----------------------------------)

[See all (28)](https://medium.com/@tadeumx1/following?source=blogrolls_sidebar-----67104232b878-----------------------------------)



80





Thanks to Marcos Campos. 

80









- [Android](https://medium.com/tag/android)
- [Android Studio](https://medium.com/tag/android-studio)
- [Android App Development](https://medium.com/tag/android-app-development)
- [AndroidDev](https://medium.com/tag/androiddev)
- [Unit Testing](https://medium.com/tag/unit-testing)

## [More from Matheus Tadeu](https://medium.com/@tadeumx1?source=follow_footer-----67104232b878-----------------------------------)

Follow



Software Developer at Midway (RCHLO) and a EDM Lover

[Published in **Nerdzão/Nerdgirlz**](https://medium.com/nerdzao?source=follow_footer-----67104232b878----0-------------------------------)[·Feb 11, 2019](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?source=follow_footer-----67104232b878----0-------------------------------)[Leitura de QRCode no React Native](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?source=follow_footer-----67104232b878----0-------------------------------)Criando uma aplicação para a leitura de QRCode, integrada com uma WebView e navegador utilizando Linking[![img](https://miro.medium.com/max/630/1*HkfIjUcLoPbI_oUhbFHm3w.jpeg)](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?source=follow_footer-----67104232b878----0-------------------------------)Nos dias hoje, muitos aplicativos utilizam os chamados QRCode de diversas formas: anúncios, propagandas, campanhas de marketing, e até para obter mais informações sobre monumentos e obras em espaços públicos ou museus.Resumindo, um QRCode é um código de barras bidimensional, que pode ser facilmente escaneado usando a maioria dos…[Read more · 5 min read](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?readmore=1&source=follow_footer-----67104232b878----0-------------------------------)227[2](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?responsesOpen=true&source=follow_footer-----67104232b878----0-------------------------------)[Published in **Nerdzão/Nerdgirlz**](https://medium.com/nerdzao?source=follow_footer-----67104232b878----1-------------------------------)[·Jan 7, 2019](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?source=follow_footer-----67104232b878----1-------------------------------)[Utilizando Rotas com a Google Maps API no React Native](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?source=follow_footer-----67104232b878----1-------------------------------)Criando uma aplicação para o cálculo de rotas em mapas e integrando com o Google Maps[![img](https://miro.medium.com/max/630/1*RCI6zOXWkRWKfIUvHtNWjw.png)](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?source=follow_footer-----67104232b878----1-------------------------------)Atualmente não é difícil ver diversos aplicativos utilizando mapas integrados com a Google Maps API com ela podemos, fazer desde aplicativos mais simples que listam lugares, até mais complexos como por exemplo aqueles de carros compartilhados.O último tipo citado usa um recurso interessante disponível na Maps API, o cálculo…[Read more · 7 min read](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?readmore=1&source=follow_footer-----67104232b878----1-------------------------------)261[6](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?responsesOpen=true&source=follow_footer-----67104232b878----1-------------------------------)[Dec 10, 2018](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?source=follow_footer-----67104232b878----2-------------------------------)[Utilizando Mapas no React Native](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?source=follow_footer-----67104232b878----2-------------------------------)Criando uma aplicação com mapa nativo da Google Maps API[![img](https://miro.medium.com/max/630/1*nzkBi3V8EHiu9CjsfwQHyA.png)](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?source=follow_footer-----67104232b878----2-------------------------------)Hoje em dia não é difícil ver diversos aplicativos utilizando mapas integrados com a Google Maps API com ela podemos, fazer desde aplicativos mais simples que listam lugares, até mais complexos como por exemplo aqueles de carros compartilhados.Irei fazer uma série de “artigos” mostrando como podemos usar as mais…[Read more · 8 min read](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?readmore=1&source=follow_footer-----67104232b878----2-------------------------------)192[2](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?responsesOpen=true&source=follow_footer-----67104232b878----2-------------------------------)



[About](https://medium.com/about?autoplay=1&source=post_page-----67104232b878-----------------------------------)

[Write](https://medium.com/new-story?source=post_page-----67104232b878-----------------------------------)

[Help](https://help.medium.com/hc/en-us?source=post_page-----67104232b878-----------------------------------)

[Legal](https://policy.medium.com/medium-terms-of-service-9db0094a1e0f?source=post_page-----67104232b878-----------------------------------)[Matheus Tadeu](https://medium.com/@tadeumx1?source=post_page-----67104232b878-----------------------------------)

[105 Followers](https://medium.com/@tadeumx1/followers?source=post_page-----67104232b878-----------------------------------)[About](https://medium.com/@tadeumx1/about?source=post_page-----67104232b878-----------------------------------)Follow





[Upgrade](https://medium.com/plans?source=upgrade_membership---nav_full-------------------------------------)







# Introdução a Testes Unitários com JUnit e Mockito no Android

## Criando testes unitários em uma aplicação utilizando MVVM Model-View View Model e DataBinding com Kotlin

[![Matheus Tadeu](https://miro.medium.com/fit/c/56/56/1*xCSnbE67xOvCgcvhvgLNnw.jpeg)](https://medium.com/@tadeumx1?source=post_page-----67104232b878-----------------------------------)

[Matheus Tadeu](https://medium.com/@tadeumx1?source=post_page-----67104232b878-----------------------------------)

[Jul 7, 2019·13 min read](https://medium.com/@tadeumx1/introdução-a-testes-unitários-com-junit-e-mockito-no-android-67104232b878?source=post_page-----67104232b878-----------------------------------)







![img](https://miro.medium.com/max/1400/1*YXAFrnNR4nbm250edUy7YQ.png)

Cada vez mais é necessário, garantir confiabilidade para nossas aplicações, pois elas mudam a todo tempo sempre precisamos trocar algo, ou desenvolver um novo recurso, assim ter a certeza que o restante das funcionalidades que já existem, irão continuar funcionando de forma correta, é fundamental.

E exatamente para termos essa garantia existem os testes unitários, com eles podemos testar toda a lógica de nossa aplicação, garantindo assim que tudo esteja funcionando da forma correta, e que ao desenvolver uma nova feature, ela não acabe quebrando o restante do projeto, isso ocorre pois na maioria das vezes só estamos preocupados em testar o fluxo feliz, em que tudo funciona corretamente, e não nos atentamos em também testar os erros que podem ocorrer como por exemplo, conexão ruim durante o uso do aplicativo, o usuário fechar o aplicativo durante uma requisição na API, e por aí vai.

<iframe src="https://cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fgiphy.com%2Fembed%2Fl2JhEItioAxac7toQ%2Ftwitter%2Fiframe&amp;url=https%3A%2F%2Fgiphy.com%2Fgifs%2Fnfl-football-new-york-jets-l2JhEItioAxac7toQ&amp;image=https%3A%2F%2Fmedia.giphy.com%2Fmedia%2Fl2JhEItioAxac7toQ%2Fgiphy.gif&amp;key=a19fcc184b9711e1b4764040d3dc5c07&amp;type=text%2Fhtml&amp;schema=giphy" allowfullscreen="" frameborder="0" height="251" width="435" title="Celebrating New York Jets GIF by NFL - Find &amp; Share on GIPHY" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 392.361px;"></iframe>

Quando seus testes passam de primeira

**JUnit**

Para escrever **testes unitários no Android**, utlizamos o JUnit que é um framework open-source, criado por [Erich Gamma](https://pt.wikipedia.org/wiki/Erich_Gamma) e [Kent Beck](https://pt.wikipedia.org/wiki/Kent_Beck), que conta com as principais funcionalidades necessárias para esse fim.

Geralmente, esse framework já vem configurado no `build.gradle` no módulo app do projeto dessa forma, mas caso não tiver adicione essa linha

```
dependencies {
  
  // outras dependências da aplicação  // adicionar essa linha
  testImplementation 'junit:junit:4.12'

}
```

Lembrando que devemos adicionar o `JUnit` utilizando o `testImplementation `pois dessa forma, ele só vai ser usado em ambiente de teste, quando for preciso, e não vai ser carregado por exemplo quando o APK final for gerado, diminuindo seu tamanho.

**Diferenças entre o JUnit4 e JUnit5**

Como deve ter reparado estamos usando a versão 4 do JUnit. Apesar dela vir como padrão em projetos Android, recentemente (já faz um tempo hahaha) a sua nova versão chamada JUnit5 foi lançada, e trás algumas vantagens em relação a sua antiga versão como:

- Modularização em três pacotes, que te permite usar realmente o que é necessário no seu projeto
- Maior compatibilidade com novos recursos do Java 8 principalmente as lambdas functions
- Novas Annotations e Assertions que podem resolver muito dos seus problemas com versões anteriores do framework

Caso tenha interesse em saber mais sobre essa atualização, e a como utilizar em seu projeto recomendo a leitura de um artigo, disponível nesse [link](https://medium.com/android-dev-br/utilizando-junit-5-no-android-82d752708985) e também da sua [documentação](https://junit.org/junit5/docs/current/user-guide/#overview), que conta com um guia muito intuitivo.

Agora que já entendemos o porque de escrever testes unitários para nossos aplicativo, e já conhecemos a ferramenta que vamos utilizar no Android. O objetivo de um teste unitário é testar de forma isolada algum comportamento que existe no seu projeto, geralmente classes e métodos, um bom exemplo inicial, seria testar um método que soma dois valores:

Método

```
public int sum(int firstValue, int secondValue) {  
   
  return firstValue + secondValue; }
```

Teste do método

```
@Test 
public void plusOperationTest() {  assertEquals(4, sum(2, 2));}
```

Com isso está sendo testado o método `sum` que recebe dois números inteiros e retorna para o usuário a soma desses números, nesse teste os números passados são 2 e 2 assim o valor da soma deve ser 4, para validar esse resultado é usado o método assertEquals, passando o resultado esperado e chamando o método que queremos testar seu resultado, abaixo tem outra forma de testar a soma entre dois números mas dessa vez, já definidos no teste

```
@Test
public void sumTest() {  int value = 7
  int anotherValue = 3  int resultado = value + anotherValue  assertEquals(10, resultado)}
```

Nesse caso está sendo feito o teste da soma de dois valores, que é feita pelo método `sumTest` estamos declarando duas variáveis do tipo inteiro, que recebem os valores de 7 e 3 checando o resultado dessa soma, que deve ser 10, utilizando o método `assertEquals` do JUnit4, que recebe dois parâmetros e verifica caso eles são iguais, geralmente o primeiro é o valor que você espera da operação, e o segundo é o resultado da sua operação nesse caso, uma soma entre dois números inteiros.

Lembrando que para indicar, que aquele método é um teste unitário, é necessário utilizar a anotação `@ Test` do JUnit4, a sua forma de identificar testes.

Em alguns casos, quando a estrutura da classe ou método a ser testada é mais complexa e depende de outras classes ou objetos, podemos mockar esses objetos, com o objetivo de garantir que nosso teste, apenas estará testando um comportamento de forma isolada.

**Mockito**

Para mockar objetos em testes no Android, é utilizado o Mockito, uma biblioteca com o objetivo de facilitar o processo de mockar métodos ou classes dependentes no seu teste, criado em 2015 pela comunidade. É o framework de mock mais utilizado para a escrita de testes unitários em Java e também em aplicações Android.

Para configurar o Mockito em seu projeto é necessário, adicionar os pacotes necessários no arquivo `build.gradle` do módulo app no seu projeto:

```
dependencies {
  
  // outras dependências da aplicação  // Dependência principal do Mockito
  testImplementation 'org.mockito:mockito-core:2.28.2'  // Dependência do Mockito para testes no Android
  androidTestImplementation 'org.mockito:mockito-android:2.28.2'  // Dependência do Mockito para ser possível mockar classes e métodos constantes
  testImplementation 'org.mockito:mockito-inline:2.28.2'}
```

Depois disso, é só sicronizar o Gradle do projeto, e temos o Mockito configurado pronto para uso.

Agora que já temos tudo configurado no nosso projeto, podemos começar a escrever nossos testes 😃

**Conhecendo o aplicativo**

Como esse é um texto introdutório ao assunto preparei um exemplo bem simples, um aplicativo que faz o cálculo do combustível que um veículo irá gastar em uma viagem considerando a distância do local, preço do combustível e a autonomia do carro usado.

O aplicativo está funcionando dessa forma:

![img](https://miro.medium.com/freeze/max/36/1*RpqYFVxVtkUgqnccjp_Ixg.gif?q=20)

![img]()

Lembrando que esse projeto foi feito utilizando o padrão de arquitetura de apresentação, **Model-View View Model (MVVM)** e o principal benefício disso, é que a lógica de negócio de cada tela fica no ViewModel uma classe que é responsável, por ligar a interface com os dados utilizados na aplicação, com o uso desse modelo fica mais fácil escrever testes unitários no projeto, já que dividimos as responsabilidades entre a interface (View), lógica de negócio (ViewModel) e a representação dos dados utilizados no seu projeto (Model) para um melhor entendimento sobre esse padrão, recomendo a leitura de um artigo disponível nesse [link](https://medium.com/@soutoss/arquiteturas-em-android-mvvm-kotlin-retrofit-parte-1-2ac77c8a26)

Como o foco desse artigo são os testes unitários, somente vou apresentar o código do ViewModel desse projeto:

<iframe src="https://medium.com/media/f150bbcaaffaf681f21d7df3a1af477d" allowfullscreen="" frameborder="0" height="0" width="0" title="Post Introdução a Testes Unitários com JUnit e Mockito no Android" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 680px;"></iframe>

Esse é o ViewModel da Activity principal do projeto, estamos estendendo da classe `AndroidViewModel` que está no pacote do [Android Component](https://medium.com/android-dev-moz/aac1-bc22abbabecc)s da Google, temos os valores dos inputs usados na aplicação usando o [Android DataBinding](https://medium.com/android-dev-br/começando-com-android-data-binding-d7719333eecc) uma biblioteca faz parte do [Android JetPack](https://developer.android.com/jetpack?hl=pt-br), que tem por objetivo facilitar o [binding](https://developer.android.com/topic/libraries/data-binding?hl=pt-br) entre os layouts XML e código Java ou Kotlin, evitando assim o famigerado findViewById() e ainda, nesse caso temos a facilidade de chamar a função `handleCalculateButtonClick` diretamente da declaração do botão no XML dessa forma:

```
<?xml version="1.0" encoding="utf-8"?><layout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools">

    <data>

        <variable
                name="viewModel"
                type="com.example.mytrip.viewmodels.MainActivityViewModel" />

    </data>

<ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@color/colorLightGray">
    
    <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical">    ...      <Button
            android:id="@+id/buttonCalculate"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_margin="15dp"
            android:padding="20dp"
            android:text="@string/calcular"
            <!-- Chamada da função diretamente pelo XML -->
            android:onClick="@{() ->     viewModel.handleCalculateButtonClick()}"
            android:background="@drawable/round_btn"
            android:textAllCaps="true"
            android:textColor="@color/colorLightGray"
            android:textSize="20sp" />    ...    </LinearLayout>

</ScrollView>

</layout><!-- activity_main.xml -->
```

Quando o botão for clicado ele vai chamar a função `handleCalculateButtonClick()` responsável, por chamar a função `handleCalculate()` que vai validar os valores dos inputs utilizando a função `isValid()` que valida, caso realmente os campos foram preenchidos e também que o valor da autonomia deve ser maior que zero. Após isso é realizado o cálculo do valor de combustível que o veículo iria gastar em uma viagem, por exemplo.

**Testes unitários**

E nesse momento entram finalmente os testes unitários, vamos precisar checar o comportamento das funções no ViewModel, como por exemplo validar o cálculo do combustível e caso os valores dos inputs são números e estão corretos.

Os **testes unitários** em um projeto Android estão localizados no pacote `test` dentro de src assim sendo src/test

![img](https://miro.medium.com/max/60/1*Ml2-b_mQVBAIrPZ9LRFyqQ.png?q=20)

![img](https://miro.medium.com/max/565/1*Ml2-b_mQVBAIrPZ9LRFyqQ.png)

Já os **testes instrumentados** ou automatizados, que são outro tipo de testes para projetos Android, onde o objetivo é testar o comportamento da interface do aplicativo ficam localizados no pacote `androidTest` dentro de src assim sendo src/androidTest

Geralmente eles são feitos usando o [Espresso](https://developer.android.com/training/testing/espresso) que é um framework de testes fornecido pelo Android Testing Support Library. Ele contém as APIs necessárias para escrever testes de UI e simular as interações do usuário com o aplicativo.

![img](https://miro.medium.com/max/60/1*y9jIEnqeW4WKmqhzNgREGw.png?q=20)

![img](https://miro.medium.com/max/572/1*y9jIEnqeW4WKmqhzNgREGw.png)

Lembrando que esse tipo de teste é bem interessante e muito usado, não vou me aprofundar muito aqui, mas te recomendo estudar sobre a implementação desses testes, isso podemos deixar para um próximo artigo, já que é um assunto bem importante.

Nesse projeto criei os testes do ViewModel tanto em Kotlin e também Java para observar as diferenças, somente por questão de estudo mesmo, por isso temos dois arquivos de testes para o ViewModel.

Vamos criar a classe `MainActivityViewModelTest` dentro do pacote `test` para nela conter os testes unitários dos métodos do ViewModel, lembrando que é muito legal seguir esse padrão de nomenclatura para suas classes de teste sendo o nome da sua classe + test assim, como estamos fazendo.

<iframe src="https://medium.com/media/42b7eb4560e2cfc3e0ce39c58eea789d" allowfullscreen="" frameborder="0" height="3004" width="680" title="Post Introdução a Testes Unitários com JUnit e Mockito no Android" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 3003.99px;"></iframe>

Esse é o ViewModel com todos os testes, do aplicativo como já foi dito está sendo testado, desde de validação do input até o clique do botão e o cálculo do combustível.

Agora vamos analisando cada teste, e o que ele está realmente testando

```
@Before
fun setUp() {
    MockitoAnnotations.initMocks(this)
}
```

No início temos a função `setUp()` ela é responsável por inicializar os mocks do Mockito em cada teste que estiver nesse classe, e a annotation **Before** é quem dá o poder para a função fazer isso, toda função que estiver com essa marcação vai ser executada, antes de cada teste que estiver na classe de teste.

```
@Test
fun isValidReturnTrueTest() {

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("100")

    val preco = mainActivityViewModel.preco
    preco.set("30")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("15")


    assertTrue(mainActivityViewModel.isValid())

}
```

Já o teste `isValidReturnTrueTest()` valida caso estamos, preenchendo corretamente os inputs do aplicativo, sem deixar nenhum vazio, e com o valor da autonomia maior que zero, assim garantindo que posteriormente o cálculo do combustível, vai poder ser feito sem problemas. Importante atentar que estamos instanciando o nosso ViewModel e mockando a classe Application, que é necessária no seu funcionamento real, pois estamos utilizando o contexto do aplicativo dentro do ViewModel, para fazer o uso de Toast para exibir uma mensagem de erro, caso os campos forem preenchidos de forma incorreta.

Mas minha recomendação, é que sempre no possível, não utilizem o contexto da aplicação dentro do ViewModel, afim de deixa-ló mais limpo possível e somente com a lógica da tela. Só estou fazendo isso para demonstrar como é possível mockar uma classe ou qualquer outro objeto, que precisamos, para testar o comportamento da nossa classe, tanto que no código disponível no final do artigo não estou usando o contexto dessa forma e nem chamando o Toast dentro do ViewModel.

> Mais uma observação importante perante a esse teste, para mockar qualquer objeto, com o Mockito, é só utilizar o Mockito.mock(ObjetoQueVaiSerMockado) passando o objeto que irá ser mockado. Esse framework facilita muito esse processo

Após isso, é usada função `assertTrue` do JUnit que aceita um parâmetro, que pode ser uma variável, objeto, ou um retorno de uma função que é o nosso caso. Essa função valida caso o valor que foi passado é true, ao contrário, ou seja o valor sendo false, ele dá erro e assim o teste quebra.

```
@Test
fun isValidReturnFalseTest() {

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("")

    val preco = mainActivityViewModel.preco
    preco.set("")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("")

    assertFalse(mainActivityViewModel.isValid())

}
```

No teste `isValidReturnFalseTest()` é feito o fluxo ao contrário do anterior, que é quando o usuário não preencheu os campos. Assim também é necessário instanciar o ViewModel e atribuir o valor vazio para os inputs, e nesse caso utilizar a função `assertFalse()` do JUnit que é igual, a função que usamos anteriormente, mas valida caso o valor passado é igual a false, assim a função `isValid()` vai retornar false, e o teste irá passar sem problemas.

```
@Test
fun ValidHandleCalculation() {

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("30")

    val preco = mainActivityViewModel.preco
    preco.set("15")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("250")

    val resultado = mainActivityViewModel.resultado

    mainActivityViewModel.handleCalculate()

    assertEquals("Total: R$ 1.8", resultado.get())

}
```

Esse é um dos testes mais importantes do aplicativo, o `ValidHandleCalculation()` ele é responsável por testar caso o cálculo do combustível está sendo feito da maneira esperada, nele são preenchidos todos os inputs corretamente, e o método handleCalculate é chamado, onde o cálculo é feito, após isso o valor do resultado do cálculo, é obtido através da variável resultado que está ligada ao TextView que mostra esse valor no aplicativo utilizando o DataBinding no ViewModel. O valor esperado é de R$ 1.8 e para validar caso o valor que foi calculado está correto, está sendo usado a função `assertEquals()` do JUnit, que funciona dessa forma `assertEquals(expected: Any!, actual: Any!)` o primeiro parâmetro será o valor esperado para o teste funcionar, já o segundo é o valor da operação que está sendo testada, nesse teste o resultado do cálculo, caso os valores forem iguais o teste irá passar, caso o contrário vai quebrar, assim garantindo o funcionamento correto do aplicativo.

```
@Test
fun ValidHandleCalculationWrongNumber() {

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("asadsaddsasdsdadssd")

    val preco = mainActivityViewModel.preco
    preco.set("15")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("250")

    val resultado = mainActivityViewModel.resultado

    var numberFormatException = false

    try {
        mainActivityViewModel.handleCalculate()
        numberFormatException = false
    } catch (e : Exception) {
        numberFormatException = true
    }

    assertTrue(numberFormatException)

}
```

Esse teste `validHandleCalculationWrongNumber()` é responsável por verificar caso os valores inseridos nos inputs são números e não letras, ou qualquer outro tipo de caractere incorreto, para depois ser possível realizar o cálculo e o aplicativo funcionar da maneira correta.

Nesse teste estou colocando um texto no valor do input de distância, e números no restante, após isso dentro de um try catch assim como no código, do ViewModel tento realizar cálculo, é esperado que caia dentro do catch onde valido o erro usando a variável `numberFormatException` que agora tem o valor true, garantindo que caso qualquer um dos inputs tenha valores diferentes de números, o cálculo não seja feito.

```
@Test
fun handleCalculateButtonClickCallHandleCalculate() {

    // Test the handleCalculateButtonClick call HandleCalculate

    val mainActivityViewModel = MainActivityViewModel(Mockito.mock(Application::class.java))

    val distancia = mainActivityViewModel.distancia
    distancia.set("30")

    val preco = mainActivityViewModel.preco
    preco.set("15")

    val autonomia = mainActivityViewModel.autonomia
    autonomia.set("250")

    val spy = spy(mainActivityViewModel)

    spy.handleCalculateButtonClick()

    verify(spy, Mockito.times(1)).handleCalculate()

}
```

No último teste o `handleCalculateButtonClickCallHandleCalculate()` está sendo validado, se após o botão ser clicado e a função `handleCalculateButtonClick()` for chamada pelo Data Binding da classe, essa função vai chamar a função a `handleCalculate()` que de fato vai realizar o cálculo do combustível, como já foi dito.

**Mockito - Spy**

Nesse teste estamos usando alguns recursos interessantes que o Mockito nos oferece, o primeiro deles é o spy, esse é um conceito bem conhecido em testes unitários no geral, quando precisamos observar e copiar o comportamento de um objeto, sendo ele uma classe ou método para utilizar nos testes, usamos o spy, como se estivéssemos realmente espiando o objeto real no código. Nesse caso estamos fazendo o spy de nosso ViewModel e chamando a função `handleCalculateButtonClick()` simulando o clique do botão

**Mockito - Verify**

Como nesse caso está sendo feito o spy do nosso ViewModel podemos usar algumas funções do Mockito para verificar interações de métodos no nosso código, como por exemplo caso o método retornou o que foi esperado, caso o tipo de retorno do método está correto, e por aí vai, essas funções são a `when()` `doReturn()` e também a `verify()` que estamos utilizando nesse teste, após a chamar a função do clique do botão, vamos usar o verify dessa forma:

```
verify(spy, Mockito.times(1)).handleCalculate()
```

Nesse caso a função `verify()` está sendo usada para checar caso a função `handleCalculate()` que está no spy do ViewModel foi chamada uma vez, e é esperado que ela seja, porque a função responsável pelo clique do botão a `handleCalculateButtonClick()` foi chamada antes dela, com isso o objetivo do teste unitário foi concluído.

Com isso acabamos os testes unitários do nosso aplicativo usando o **JUnit** e o **Mockito** em projeto utilizando MVVM

Apesar de esse, ter sido um artigo focado para esse tipo de teste no Android, acredito que foram apresentados diversos conceitos muitos importantes como:

- As vantangens de usar um padrão de arquitetura com o objetivo de deixar seu projeto mais testável
- Porque realizar testes unitários
- A diferença com os testes intrumentados
- Utilizar o Mockito e suas principais funções
- O motivo de mockar objetos em testes
- Como o spy pode te ajudar em seus testes

E o mais importante fazer testes unitários na prática.

Resultado final

![img](https://miro.medium.com/max/60/1*oXJ5aNJBkeuMqC6gkrf8YA.png?q=20)

![img](https://miro.medium.com/max/630/1*oXJ5aNJBkeuMqC6gkrf8YA.png)

O projeto está disponível nesse [repositório](https://github.com/tadeumx1/MyTripMVVMAndroid) no GitHub e qualquer dúvida que tiverem, ou quiserem acrescentar algo, é só deixar um comentário.

Também não esqueça de me acompanhar nas redes sociais, para gente trocar aquela ideia

[matheustadeu.com](https://matheustadeu.com/)

[www.linkedin.com/in/matheus-tadeu/](https://www.linkedin.com/in/matheus-tadeu/)

**Referências**

[Criando testes para seu aplicativo Android - AndroidProNo mundo do desenvolvimento de softwares, sempre há situações em que acontecem coisas que nós não prevemos ou até mesmo…www.androidpro.com.br](https://www.androidpro.com.br/blog/desenvolvimento-android/criando-testes-para-seu-aplicativo-android/)

[JUnit 5 vs JUnit 4 - HowToDoInJavaJUnit 5 aims to adapt java 8 style of coding and to be more robust and flexible than JUnit 4. In this post, JUnit 5 vs…howtodoinjava.com](https://howtodoinjava.com/junit5/junit-5-vs-junit-4/)

[Testes em Android - Parte I: Por onde começar?Fala, Comunidade! Este post é o primeiro de uma série sobre testes em Android. Você aprenderá conceitos essenciais…tasafo.wordpress.com](https://tasafo.wordpress.com/2017/01/26/testes-em-android-parte-i-por-onde-comecar/)

[Unit Testing with JUnit - TutorialIn general it it safe to ignore trivial code. For example, it is typical useless to write tests for getter and setter…www.vogella.com](https://www.vogella.com/tutorials/JUnit/article.html)

[Android testing: Unit testing (Part 1) - Android development and testingToday I would like the series of articles about Android Testing. I'm planning create articles about different type of…alexzh.com](https://alexzh.com/2016/03/24/android-testing-unit-testing/)

[How to Use Mockito in Android - DZone MobileLearn how to integrate the Mockito autmated testing framework with your mobile app and use the mock and spy methods to…dzone.com](https://dzone.com/articles/how-to-use-mockito-in-android)

[Android Testing with JUnit & mockitoTips, study notes, and mini-code samplesmedium.com](https://medium.com/@Shahawi/android-testing-with-junit-mockito-d40b5f6c68a7)

Muito obrigado pela atenção pessoal e espero que tenham gostado.

[Matheus Tadeu](https://medium.com/@tadeumx1?source=post_sidebar--------------------------post_sidebar--------------)

Software Developer at Midway (RCHLO) and a EDM Lover



- [Android](https://medium.com/tag/android)
- [Android Studio](https://medium.com/tag/android-studio)
- [Android App Development](https://medium.com/tag/android-app-development)
- [AndroidDev](https://medium.com/tag/androiddev)
- [Unit Testing](https://medium.com/tag/unit-testing)

## [More from Matheus Tadeu](https://medium.com/@tadeumx1?source=follow_footer-----67104232b878-----------------------------------)



[Published in **Nerdzão/Nerdgirlz**](https://medium.com/nerdzao?source=follow_footer-----67104232b878----0-------------------------------)[·Feb 11, 2019](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?source=follow_footer-----67104232b878----0-------------------------------)[Leitura de QRCode no React Native](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?source=follow_footer-----67104232b878----0-------------------------------)Criando uma aplicação para a leitura de QRCode, integrada com uma WebView e navegador utilizando Linking[![img](https://miro.medium.com/max/630/1*HkfIjUcLoPbI_oUhbFHm3w.jpeg)](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?source=follow_footer-----67104232b878----0-------------------------------)Nos dias hoje, muitos aplicativos utilizam os chamados QRCode de diversas formas: anúncios, propagandas, campanhas de marketing, e até para obter mais informações sobre monumentos e obras em espaços públicos ou museus.Resumindo, um QRCode é um código de barras bidimensional, que pode ser facilmente escaneado usando a maioria dos…[Read more · 5 min read](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?readmore=1&source=follow_footer-----67104232b878----0-------------------------------)227[2](https://medium.com/nerdzao/leitura-de-qrcode-no-react-native-7bdb82196f6e?responsesOpen=true&source=follow_footer-----67104232b878----0-------------------------------)[Published in **Nerdzão/Nerdgirlz**](https://medium.com/nerdzao?source=follow_footer-----67104232b878----1-------------------------------)[·Jan 7, 2019](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?source=follow_footer-----67104232b878----1-------------------------------)[Utilizando Rotas com a Google Maps API no React Native](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?source=follow_footer-----67104232b878----1-------------------------------)Criando uma aplicação para o cálculo de rotas em mapas e integrando com o Google Maps[![img](https://miro.medium.com/max/630/1*RCI6zOXWkRWKfIUvHtNWjw.png)](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?source=follow_footer-----67104232b878----1-------------------------------)Atualmente não é difícil ver diversos aplicativos utilizando mapas integrados com a Google Maps API com ela podemos, fazer desde aplicativos mais simples que listam lugares, até mais complexos como por exemplo aqueles de carros compartilhados.O último tipo citado usa um recurso interessante disponível na Maps API, o cálculo…[Read more · 7 min read](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?readmore=1&source=follow_footer-----67104232b878----1-------------------------------)261[6](https://medium.com/nerdzao/utilizando-rotas-com-a-google-maps-api-no-react-native-69a05a434ab5?responsesOpen=true&source=follow_footer-----67104232b878----1-------------------------------)[Dec 10, 2018](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?source=follow_footer-----67104232b878----2-------------------------------)[Utilizando Mapas no React Native](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?source=follow_footer-----67104232b878----2-------------------------------)Criando uma aplicação com mapa nativo da Google Maps API[![img](https://miro.medium.com/max/630/1*nzkBi3V8EHiu9CjsfwQHyA.png)](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?source=follow_footer-----67104232b878----2-------------------------------)Hoje em dia não é difícil ver diversos aplicativos utilizando mapas integrados com a Google Maps API com ela podemos, fazer desde aplicativos mais simples que listam lugares, até mais complexos como por exemplo aqueles de carros compartilhados.Irei fazer uma série de “artigos” mostrando como podemos usar as mais…[Read more · 8 min read](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?readmore=1&source=follow_footer-----67104232b878----2-------------------------------)192[2](https://medium.com/@tadeumx1/utilizando-mapas-no-react-native-817c4f4de6f7?responsesOpen=true&source=follow_footer-----67104232b878----2-------------------------------)https://policy.medium.com/medium-terms-of-service-9db0094a1e0f?source=post_page-----67104232b878-----------------------------------)