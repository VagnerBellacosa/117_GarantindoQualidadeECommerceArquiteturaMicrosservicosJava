# Mocks: Introdução a Automatização de Testes com Mock Object

## Este artigo apresenta uma introdução aos Mocks, quais são as ferramentas mais utilizadas na criação de Mock Object utilizando exemplos práticos e, por fim, faremos uma comparação dos Mocks disponíveis e mais utilizados atualmente.



[Artigos](https://www.devmedia.com.br/artigos/)[Engenharia de Software](https://www.devmedia.com.br/artigos/engenharia-de-software)Mocks: Introdução a Automatização de Testes com Mock Object

O termo "Mock Objects" é utilizado para descrever um caso especial de objetos que imitam objetos reais para teste. Esses Mock Objects atualmente podem ser criados através de frameworks que facilitam bastante a sua criação. Praticamente todas as principais linguagens possuem frameworks disponíveis para a criação de Mock Objects. Os Mock Objects são mais uma forma de objeto de teste.

As ideias e conceitos por trás dos Mock Objects surgiram através de muita experimentação, discussão e colaboração entre diversos desenvolvedores que tinham uma ideia e a evoluíram para algo mais profundo resultando em algo extremamente útil para os desenvolvedores de software.

Mocks Objects são bastante difundidos na comunidade e na literatura de métodos ágeis [Extremme Programming (XP)](https://www.devmedia.com.br/extreme-programming-conceitos-e-praticas/1498), visto que, utilizando o [XP](https://www.devmedia.com.br/introducao-ao-extreme-programming-xp/29249) se faz uso constante de testes através da técnica [Test-Driven Development (TDD)](https://www.devmedia.com.br/test-driven-development-tdd-simples-e-pratico/18533) que prega teste antes da implementação. Com isso, devemos simular alguns objetos no intuito de conseguir testar o código. Ainda assim, os Mock Objects possuem pouca literatura de forma geral e muitas vezes são confundidos com outras coisas como stubs que são objetos que auxiliam testes de ambientes. Os Mock Objects são ainda mais utilizados no Behavior Driven Development (BDD) que se trata de uma variação do TDD e que utilizam testes com Mock Objects.

Existem diversas razões para utilizarmos Mock Objects em nossos sistemas. Nos testes unitários podemos simular o comportamento de objetos reais complexos, principalmente quando estes objetos são difíceis de serem incorporados nos testes de unidade. Um exemplo disso é uma chamada remota que pode ser simulada com Mock Objects. Os Mock Objects também são muito utilizados quando temos objetos que geram resultados variáveis (por exemplo: tempo), objetos com estados difíceis de serem criados ou reproduzidos, objetos lentos como [banco de dados](https://www.devmedia.com.br/cursos/banco-de-dados) que precisam ser inicializados antes do teste, objetos que ainda não existem ou podem ter comportamentos alterados, objetos que necessitem de informações e métodos adicionais exclusivos para os testes, entre outros. Um exemplo de uma situação que poderíamos utilizar Mock Objects é um programa de despertador que faz uma sirene tocar em certo momento. Para testar este comportamento, o teste de unidade deve esperar até que a hora programada chegue, para testar a campainha de forma correta. Se um Mock Object for usado no lugar do objeto real, então ele pode ser programado para simular a hora de programação do despertador. Assim o código do despertador pode ser testado corretamente e sem maior impacto no tempo de desenvolvimento.

Uma das limitações dos Mocks é quando temos um excesso de objetos Mocks como parte de uma suíte de testes, pois quando temos modificações no código é preciso fazer um grande número de modificações nos testes. Manutenções incorretas também podem gerar erros que podem passar despercebidos, estes erros só seriam vistos quando os testes unitários utilizassem instâncias de classes reais.

Outra limitação é que os Mocks não respeitam muito a ideia de baixo acoplamento, ou seja, estamos escrevendo um teste acoplado com a nossa implementação atual do objeto. Dessa forma, se refatorarmos nossa classe os testes com o Mock podem quebrar ou continuar passando, mas não testar mais nada.

No restante do artigo veremos quais ferramentas temos disponíveis para auxiliar os desenvolvedores e testadores na criação de Mocks e faremos uma comparação entre as principais ferramentas de Mock disponíveis atualmente.

### Ferramentas de Auxílio para Criação de Mocks

Os Mocks possuem bibliotecas que ajudam na sua criação. A sintaxe varia de ferramenta para ferramenta, mas no geral todas são bastante agradáveis, simples e possuem uma boa cobertura para testes de diferentes níveis.

Diversas linguagens de programação ou ambientes de desenvolvimento possuem bibliotecas para criar Mocks.

- Para [Java](https://www.devmedia.com.br/cursos/java) temos o JMockit, Mockito, EasyMock, JMock, MockCreator, MockLib e HibernateMock.
- Para plataforma [.NET](https://www.devmedia.com.br/curso/curso-de-asp-net-mvc/1917) temos o NMockLib, Rhino Mocks, NMock e NMock 2 TypeMock.
- Para o Ruby temos o Mocha, RSpec e FlexMock.
- Para [linguagem PHP](https://www.devmedia.com.br/cursos/php) temos o SimpleTest, Yay! Mock, SnapTest e PHPUnit.
- Para o [Delphi](https://www.devmedia.com.br/guia/delphi/38186), Kylix, FreePascal ou Pascal Mock.

Outras linguagens e ambientes de desenvolvimento também possuem bibliotecas para Mocks, basta uma pequena pesquisa para que possamos encontrar uma biblioteca disponível.

Nas sessões abaixo nos focaremos mais nas principais ferramentas de Mock para Java explicando e exemplificando cada uma delas.

### EasyMock

O EasyMock é uma biblioteca que fornece uma forma fácil para usarmos Mock Objects para classes ou interfaces. O EasyMock está disponível pela [licença Apache 2](http://www.apache.org/licenses/LICENSE-2.0.txt). Para utilizar o EasyMock devemos utilizar a versão Java 1.5.0 ou acima.

EasyMock está disponível no repositório central do Maven apenas adicionando a dependência da **Listagem 1.**

```
<dependency>
  <groupId>org.easymock</groupId>
  <artifactId>easymock</artifactId>
  <version>3.2</version>
  <scope>test</scope>
</dependency>
```

**Listagem 1**. Dependência para EasyMock

O download do EasyMock pode feito na área de **Links**. Basta descompactar os arquivos numa pasta e adicionar o Jar do EasyMock no classpath do projeto.

Para ilustrar como funciona o EasyMock e algumas das situações um pouco mais complicadas que podemos resolver utilizando esta ferramenta consideremos o exemplo de um “Processador” que recebe informações de uma “Fonte de Origem”, processa esse dado podendo fazer alguma eventual transformação e, por fim, envia o dado para uma “Fonte de Destino”. Segue na **Listagem 2** um exemplo de uma classe Processador

```
package com.exemplo;

public class Processador  {

  private FonteOrigem fonteOrigem;
  private FonteDestino fonteDestino;


  public Processador(FonteOrigem fonteOrigem, FonteDestino fonteDestino) {
  this.fonteOrigem = fonteOrigem;
  this.fonteDestino = fonteDestino;
  }

  public void processaDados() throws Exception {

  String entrada = null;

  try {

    entrada = fonteOrigem.read();

  } catch (Exception ex) {

    throw new Exception("Ocorreu um problema ao ler
        dados da fonte de origem.");

  }

  if(entrada != null) {

    String saida = transformaDados(entrada);

    try {

      fonteDestino.write(saida);

    } catch (Exception e) {
      throw new Exception("Nao foi possível enviar os dados
            para fonte de destino.");
    }
  }

  }

  private String transformaDados(String entrada) {

  if( "[HoraAtual]".equals(entrada) ) {
    return "hora atual: " + System.currentTimeMillis();
  }

  return entrada;

  }
}
```

**Listagem 2**. Exemplo da classe Processador com as suas dependências

Também precisamos das interfaces “FonteOrigem” e “FonteDestino” que serão utilizadas pela classe Processador. Dessa forma, criamos as duas interfaces, conforme as **Listagens 3** e **4**.

```
package com.exemplo;

public interface FonteOrigem {

  String leDados();

}
```

**Listagem 3**. Exemplo da interface de FonteOrigem

```
package com.exemplo;

public interface FonteDestino {

  void gravaDados(String dados);

}
```

**Listagem 4**. Exemplo da interface FonteDestino

Para exemplificar melhor o estudo de caso vamos imaginar que uma classe FonteOrigem que implementa a interface FonteOrigem criada acima seja responsável por obter dados de um banco de dados e por fim uma classe FonteDestino que implementa a interface FonteDestino acima envie os dados da fonte de origem pela rede usando WebSockets. Como podemos testar somente a classe Processador sem as classes de implementação que ela depende? Para fazer esse teste deveríamos implementar a classe FonteOrigem acrescentando os drivers necessários para acessar o banco de dados, criar os arquivos de configuração, fazer a conexão com o banco de dados, criar a consulta e retorná-la para Processador. Além disso, precisamos também criar a classe FonteDestino. Dessa forma, também teríamos que adicionar os drivers necessários, criar possíveis arquivos de configuração, criar todo o código que faça a movimentação dos dados pela rede, etc. Depois de fazer toda essa implementação ainda poderemos ter problemas, pois o Banco de Dados ou a rede podem não estar disponíveis em um dado momento do teste, ou ainda poderemos ter um teste não muito rápido atrasando o processo de build e desenvolvimento.

Utilizando o EasyMock podemos começar a visualizar os benefícios da sua utilização, pois não precisaremos criar nenhuma classe de dependência que o nosso teste necessite como as classes FonteOrigem e FonteDestino do exemplo. O EasyMock nos permite criar objetos que se passem por FonteOrigem e FonteDestino, mas que não necessitem serem implementados. Assim, temos um emulador dos objetos reais. Segue na **Listagem 5** um exemplo de como poderíamos fazer um teste para Processador utilizando o EasyMock.

```
package com.teste;

import org.easymock.EasyMock;
import org.junit.Before;
import org.junit.Test;

import com.exemplo.FonteDestino;
import com.exemplo.FonteOrigem;
import com.exemplo.Processador;

public class ProcessadorTeste {

  FonteOrigem fonteOrigem = null;
  FonteDestino fonteDestino = null;

  @Before
  public void inicializa() {
    //Criando os Mocks
    fonteOrigem = EasyMock.createMock(FonteOrigem.class);
    fonteDestino = EasyMock.createMock(FonteDestino.class);
  }


  @Test
  public void testProcessaDados()
  {

    EasyMock.expect(fonteOrigem.leDados()).andReturn("DadoTeste");
    fonteDestino.gravaDados("DadoTeste");

    EasyMock.replay(fonteOrigem, fonteDestino);

    //Chamando a implementação
    Processador processador = new Processador(fonteOrigem, fonteDestino);

    try {

      processador.processaDados();

    } catch (Exception e) {
      e.printStackTrace();
    }

    //Testando
    EasyMock.verify(fonteOrigem, fonteDestino);

  }

}
```

**Listagem 5**. Exemplo de como Mockar objetos utilizando EasyMock

No código acima temos a criação dos Mocks através dos comandos createMock(FonteOrigem.class) e createMock(FonteDestino.class). Com o EasyMock podemos criar Mocks a partir de classes ou interfaces. O interessante é sempre lidarmos com interfaces o que também é considerada uma boa prática sempre programar para interfaces, nunca para classes.

Os Mocks gravam tudo o que é feito com o objeto até que invocamos o comando EasyMock.replay(fonteOrigem, fonteDestino) que fará efetivamente a validação. No comando EasyMock.expect(fonteOrigem.leDados()).andReturn("DadoTeste") estamos dizendo ao EasyMock que esperamos uma chamada ao método leDados() de FonteOrigem e que o mesmo retorne a String "DadoTeste". Utilizamos EasyMock.expect sempre que queremos especificar um valor de retorno para o método mockado. Após isso fazemos uma chamada para fonteDestino.gravaDados("DadoTeste").

Por fim, precisamos informar ao EasyMock que já configuramos o comportamento do Mock e que agora o objeto deve se comportar como um objeto "normal". Assim utilizamos o comando EasyMock.replay(fonteOrigem, fonteDestino). Após isso não é mais permitido efetuar chamadas a EasyMock.expect, exceto se utilizarmos um reset em fonteOrigem. Dessa forma, executamos o nosso método normalmente chamando este com as informações necessárias Processador processador = new Processador(fonteOrigem, fonteDestino) e processador.processaDados(). Feito isso, solicitamos ao EasyMock que verifique se os métodos esperados foram chamados através do comando EasyMock.verify(fonteOrigem, fonteDestino) e caso o comportamento esperado não for satisfeito o EasyMock lança uma exceção fazendo o teste unitário falhar.

Executando o teste podemos verificar que o JUnit mostra a barra verde, ou seja, o teste foi executado com sucesso conforme ilustra a **Figura 1**.

![Barra verde sendo apresentado pelo JUnit indicando sucesso no teste](https://arquivo.devmedia.com.br/artigos/Higor_Medeiros/mock/image1.png)**Figura 1**. Barra verde sendo apresentado pelo JUnit indicando sucesso no teste

O EasyMock ainda disponibiliza diversos outros métodos para especificarmos o comportamento dos Mocks permitindo que possamos testar diversos outros cenários. Outro cenário possível é quando desejamos testar o lançamento de exceções. Através do método andThrow podemos especificar exceções. O código da **Listagem 6** mostra um trecho de como poderíamos esperar esse comportamento no EasyMock.

```
@Test
public void testProcessaDadosComExcecaoFonteOrigem()
{

  EasyMock.expect(fonteOrigem.leDados()).andThrow(new Exception
  ("Erro na leitura dos dados da fonte de origem"));

  EasyMock.replay(fonteOrigem, fonteDestino);

  Processador processador = new Processador(fonteOrigem, fonteDestino);

  try {

    processador.processaDados();

  } catch (Exception e) {
    e.printStackTrace();
  }

  EasyMock.verify(fonteOrigem, fonteDestino);
}
```

**Listagem 6**. Exemplo de como testar exceções com EasyMock

Neste código não temos nenhuma chamada a método e nenhum processamento após uma exceção ser lançada, ou seja, se algum método for chamado pelo nosso código, como, por exemplo, a tentativa de escrita de dados na rede após uma leitura com exceção, teremos uma barra vermelha indicando que algo está errado na implementação.

Um exemplo um pouco mais complicado seria testar o comando [HoraAtual]. Nesse caso, podemos notar que quando recebido esse comando o método processaDados envia pela rede o tempo atual em milissegundos. Como podemos imaginar esse tempo será diferente a cada execução do teste. Existem diversas formas de fazer essa verificação, uma delas pode ser através de expressões regulares para validar se foi enviado o tempo para o método de gravação. Assim usamos a expressão regular \d+ onde \d é um digito e + significa uma ou mais vezes. Portanto, \d+ indica um ou mais dígitos, lembrando que precisamos de outra contra barra na frente para fazer um escape. Segue na **Listagem 7** um exemplo.

```
@Test
public void testProcessaDadosComComandoTempo()
{
  EasyMock.expect(fonteOrigem.leDados()).andReturn("[HoraAtual]");
  fonteDestino.gravaDados(EasyMock.matches( "hora atual: \\d+" ) );

  EasyMock.replay(fonteOrigem, fonteDestino);

  Processador processador = new Processador(fonteOrigem, fonteDestino);

  try {

    processador.processaDados();

  } catch (Exception e) {
    e.printStackTrace();
  }


  EasyMock.verify(fonteOrigem, fonteDestino);
}
```

**Listagem 7**. Exemplo mais complexo com dados dinâmicos utilizando EasyMock

Este é um bom ponto de partida para entendermos como os Mocks funcionam, especialmente o EasyMock que tem uma leitura bem simples através da sua DSL. Além disso, EasyMock tem uma variedade bem vasta de métodos que facilitam testes de diferentes níveis de dificuldade.

### JMock

JMock é uma biblioteca para Mock Objects que ajuda os desenvolvedores a projetar e testar interações entre os objetos. A biblioteca JMock permite fazermos de forma fácil e rápida a definição de Mock Objects, também permite que possamos fazer de forma mais precisa a especificação das interações entre os objetos reduzindo a fragilidade dos testes, além disso o JMock trabalha bem com autocomplemento, refatorações e é considerado fácil de estender.

O download do JMock está disponível na área de **Links**. Para instalar o JMock basta descompactar os arquivos e colocar os JARs jmock-2.6.0.jar, hamcrest-core-1.3.jar e hamcrest-library-1.3.jar no classpath do projeto.

Na **Listagem 8** será demonstrado o mesmo exemplo anterior, porém agora utilizando JMock.

```
package com.teste;

import org.jmock.Expectations;
import org.jmock.Mockery;
import org.junit.Before;
import org.junit.Test;

import com.exemplo.FonteDestino;
import com.exemplo.FonteOrigem;
import com.exemplo.Processador;

public class ProcessadorTeste {

  Mockery context = new Mockery();

  FonteOrigem fonteOrigem = null;
  FonteDestino fonteDestino = null;

  @Before
  public void inicializa() {
    fonteOrigem = context.mock(FonteOrigem.class);
    fonteDestino = context.mock(FonteDestino.class);
  }


  @Test
  public void testProcessaDados()
  {

    context.checking(new Expectations() {{
        oneOf(fonteOrigem).leDados();
          will(returnValue("DadoTeste"));
        oneOf(fonteDestino).gravaDados("DadoTeste");
    }});


    Processador processador = new Processador(fonteOrigem, fonteDestino);

    try {

      processador.processaDados();

    } catch (Exception e) {
      e.printStackTrace();
    }

    context.assertIsSatisfied();
   }

}
```

**Listagem 8**. Exemplo testando a classe Processador e suas dependências utilizando JMock

Como podemos verificar no exemplo acima o JMock define as expectations, que são responsáveis por especificar os métodos que nós esperamos que sejam chamados durante a execução do teste. Segue na **Listagem 9** o trecho de código.

```
context.checking(new Expectations() {{
  oneOf(fonteOrigem).leDados();
    will(returnValue("DadoTeste"));
  oneOf(fonteDestino).gravaDados("DadoTeste");
}});
```

**Listagem 9**. Exemplo de como utilizar expectations com JMock

No trecho de código acima espera-se que os métodos leDados() e gravaDados() sejam chamados. Além disso, especificamos o valor do método leDados() que deverá ser retornado.

Após o código de teste ser finalizado nosso teste deve verificar se o Mock Processador foi chamado como esperado. Se não for chamado como esperado ele irá falhar e mostrará uma barra vermelha. Para fazer essa verificação utilizamos o comando context.assertIsSatisfied() assim como EasyMock.verify(fonteOrigem, fonteDestino).

O JMock também possui diversos outros métodos que nos ajudam a fazer testes mais complexos como will(throwException(expectedException)) para lidar com exceções esperadas, expectations para retorno void de métodos, checagem de parâmetros, ignorar chamadas de métodos e muito mais.

### Mockito

Mockito é mais um framework de código aberto para testes. O Mockito está sob a licença MIT License. O Mockito difere um pouco dos outros frameworks porque ele tenta eliminar o padrão expect-run-verify que é seguido por grande parte dos frameworks como vimos anteriormente. Assim ele não estabelece expectativas antecipadamente, e com isso temos um acoplamento reduzido ou minimizado, um código de teste mais fácil de ler e modificar.

O link do download do Mockito pode ser realizado na área de Links. Após isso basta descompactar os arquivos e colocar o Jar mockito-all-1.9.5.jar no classpath do projeto.

Vamos utilizar o mesmo exemplo anterior, porém agora utilizando Mockito. Segue na **Listagem 10** o código de exemplo em Mockito.

```
package com.teste;

import org.junit.Before;
import org.junit.Test;
import org.mockito.Mock;
import org.mockito.Mockito;
import org.mockito.MockitoAnnotations;

import com.exemplo.FonteDestino;
import com.exemplo.FonteOrigem;
import com.exemplo.Processador;

public class ProcessadorTeste {

  @Mock
  FonteOrigem fonteOrigem = null;
  @Mock
  FonteDestino fonteDestino = null;

  @Before
  public void inicializa() {
    MockitoAnnotations.initMocks(this);
  }


  @Test
  public void testProcessaDados()
  {

    Mockito.when(fonteOrigem.leDados()).thenReturn("DadoTeste");


    Processador processador = new Processador(fonteOrigem, fonteDestino);

    try {

      processador.processaDados();

    } catch (Exception e) {
      e.printStackTrace();
    }

    Mockito.verify(fonteOrigem, Mockito.times(1)).leDados();
    Mockito.verify(fonteDestino, Mockito.times(1)).gravaDados("DadoTeste");

   }

}
```

**Listagem 10**. Exemplo testando a classe Processador e suas dependências utilizando Mockito

A sintaxe do Mockito é preferível em relação a outros Mocks como o JMock. Podemos verificar algumas diferenças como a presença do comando MockitoAnnotations.initMocks(this) que inicializa os Mocks anotados com @Mock. O comando Mockito.when(fonteOrigem.leDados()).thenReturn("DadoTeste") é utilizado para ensinar ao nosso objeto Mock o que ele deve fazer em certas situações. O when basicamente determina qual método esperamos que seja chamado no futuro e com quais parâmetros. O thenReturn diz qual será o valor devolvido quando o método do comando when for chamado.

O Mockito ainda possui diversas outras funcionalidades como Matchers que podem ser usados no lugar de parâmetros, Mockito.doThrow semelhante ao when mas utilizado quando queremos que a invocação do método lance uma exceção, Mockito.verify(mock) para garantirmos que o objeto de teste interagiu com o nosso Mock que ainda pode ter variações como Mockito.verify(mock, Mockito.never()) para especificar quantas vezes o método foi chamado, Mockito.verify(mock, Mockito.atLeast(numero)) para especificar se o método foi chamado pelo menos um certo número de vezes, Mockito.verify(mock, Mockito.times(numero)) para especificar o número exato de chamadas que ocorreu ou ainda Mockito.verifyZeroInteractions para garantirmos que não aconteceu nenhuma interação com o Mock. Além disso, há diversas outras funcionalidades mais complexas suportadas pelo Mockito para garantir qualquer nível de teste.

### Comparando as Ferramentas

Existem diversas opiniões e comparações em relação aos diversos Mocks disponíveis para a plataforma Java. De forma geral, o Mockito é considerado mais agradável, simples e claro do que os outros projetos. JMock e EasyMock possuem uma curva de aprendizado um pouco maior em relação ao Mockito, porém o EasyMock tem um suporte bastante completo para Mock Objects. A sintaxe mínima do Mockito é muito bem projetada para suportar os casos mais comuns, embora coisas mais complicadas são fáceis de entender. Uma desvantagem do Mockito é que ele não suporta o Mock de métodos estáticos, precisando combinar Mockito com JMockit, e também não oferece suporte para Android. Um dos destaques do EasyMock é que ele é considerado bastante fácil de entender, mas um dos seus problemas é que algumas coisas são muito repetitivas. O Mockito removeu esse problema do EasyMock e tem uma sintaxe mais clara, logo nota-se que a legibilidade foi um dos principais pontos pretendidos no projeto visto que os desenvolvedores irão gastar bastante tempo lendo e dando manutenção no código existente. Outra característica bastante elogiada do Mockito é que as interfaces e classes de implementação são tratadas da mesma forma, ao contrário do EasyMock onde ainda é preciso lembrar (e verificar) para usar uma extensão de classe EasyMock. O Mockito atinge o ponto ideal, sendo fácil de escrever e ler, e consegue lidar com a maioria das situações. Uma escolha interessante seria usar Mockito com PowerMock que também permite uma extensão para o Mockito. Mockito também oferece a opção de stubbing methods, combinar argumentos (como anyInt() e anyString()), verificar o número de invocações (times(3), atLeastOnce(), never()), e muito mais.

O PowerMock é outro framework para Mock Objects que tem como característica estender o EasyMock e o Mockito suportando Mock de métodos estáticos, final e mesmos métodos privados. A ideia por trás do PowerMock não se destina a substituir outros frameworks, ao contrário, pode ser usado em situações complicadas quando outros frameworks não permitem o Mock. PowerMock também contém outros recursos úteis, como suprimir inicializadores estáticos e construtores. PowerMock é utilizado para teste de unidade em aplicações Android usando Java nativo no PC, evitando usar emuladores lentos. Tudo que foi esquecido no Mockito está coberto pelo PowerMock.

O JMockit por ser um projeto ainda novo ainda possui pouca documentação e suporte. O JMockit usa o [asm](http://asm.objectweb.org/index.html) para dinamicamente redefinir o bytecode da classe, isso permite que possamos Mockar todos os métodos inclusive estáticos, privados, construtores e inicializadores estáticos.

Existem também uma corrente de desenvolvedores que preferem JMock devido a capacidade de configurarmos expectations. Isto é completamente diferente de verificar se um método chamado foi encontrado em algumas bibliotecas Mockadas. Usando JMock podemos escrever expectations muito sofisticados.

Nas próximas sessões compararemos o jMock e o EasyMock e depois faremos uma comparação mais geral entre diversos Object Mocks.

### Comparando jMock e EasyMock

O JMock concentra-se em especificar explicitamente o comportamento dos Mocks utilizando uma DSL (Domain-Specific Language) especializada embutida no código Java. Por sua vez o EasyMock tem uma abordagem de gravação/reprodução (record/replay). Ou seja, primeiro preparamos o Mock, fazendo a chamada de método esperada. Então alteramos o Mock para o modo de repetição antes de exercitar o SUT (System Under Test). Especificar o comportamento é o mesmo que efetuarmos chamadas de métodos regulares sobre um objeto Java.

EasyMock permite criar Mocks individuais dentro do nosso método de teste utilizando poucas funcionalidades do framework conforme podemos verificar no código da **Listagem 11**.

```
import junit.framework.TestCase;
import static org.easymock.EasyMock.*;

public class EasyMockTeste extends TestCase {
  public void testAlgo() {
    AlgumaInterface mock = createMock(AlgumaInterface.class);
    // Programamos o mock aqui
    replay(mock);
    // Setup do SUT
    verify(mock);
  }
}
```

**Listagem 11**. Exemplo de criação de Mocks utilizando EasyMock

No JMock, sempre precisamos de, pelo menos, um objeto de contexto ou estender uma superclasse JMock conforme veremos mais adiante.

Podemos controlar múltiplos Mocks juntos, isto é feito utilizando um objeto especial para criar e agrupar os Mocks. A diferença neste caso é que o EasyMock chama isso de control e o JMock chama isto de context. Usamos o control/context para validar o grupo de Mocks como uma unidade.

O método mock() do JMock e o método createMock do EasyMock podem ter um parâmetro opcional String que é usado para nomear o Mock. Isto é necessário para distinguir dois Mocks do mesmo tipo. Estes nomes também são usados para referenciar os Mocks nas mensagens de falhas, então podemos usá-lo para fazer essas mensagens mais expressivas identificando claramente o Mock com as expectations incompatíveis.

No código da **Listagem 12** temos um campo control e um context criados no setup(). A verificação está em runTeste(). Nota-se que EasyMock.replay() e EasyMock.verify() esperam um vararg, assim podemos passar a lista completa de Mocks.

```
import junit.framework.TestCase;
import org.easymock.EasyMock;
import org.easymock.IMocksControl;

public class MultiplosEasyMock extends TestCase {
  private IMocksControl control;

  protected void setUp() throws Exception {
    super.setUp();
    control = EasyMock.createControl();
  }

  protected void runTest() throws Throwable {
    super.runTest();
    control.verify();
  }

  public void testAlgumaCoisa() {
    SimplesInterface mockSome = control.createMock(SimplesInterface.class);
    OutraInterface mockOutra = control.createMock(OutraInterface.class);
    // Programamos os mocks aqui
    control.replay();

    // Setup do SUT
  }
}
```

**Listagem 12**. Exemplo de como criar mais de um Mock com EasyMock

No exemplo da **Listagem 13** temos o mesmo exemplo, porém utilizando JMock.

```
import junit.framework.TestCase;
import org.jmock.Mockery;

public class MultiploJMock extends TestCase {
  private Mockery context;

  protected void setUp() throws Exception {
    super.setUp();
    context = new Mockery();
  }

  protected void runTest() throws Throwable {
    super.runTest();
    context.assertIsSatisfied();
  }

  public void testSome() {
    AlgumaInterface mock = context.mock(AlgumaInterface.class);
    OutraInterface mockOutra = context.mock(OutraInterface.class);
    // Programamos os mocks aqui

    // Setup do SUT
  }
}
```

**Listagem 13**. Exemplo de como criar mais de um Mock com JMock

Quando usamos JMock, podemos estender MockObjectTestCase para herdar o contexto automaticamente. Não interagimos com o contexto diretamente, mas podemos utilizar métodos utilitários de MockObjectTestCase com nomes que delegam ao contexto encapsulado correspondente.

EasyMock não tem um equivalente, mas podemos escrever nossa própria classe base e esconder o control dentro dela o que resulta em muito mais trabalho.

<iframe width="560" height="315" src="https://www.youtube.com/embed/aHtFVKm5l5Q" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="outline: none; -webkit-tap-highlight-color: transparent; max-width: 100%; margin: auto; height: 455.062px; width: 809px;"></iframe>

Confira: [Curso de ASP.NET MVC](https://www.devmedia.com.br/curso/curso-de-asp-net-mvc/1917)

Tanto jMock quanto EasyMock apenas mockam interfaces por padrão. Para mockar classes será necessária uma configuração diferente. Ambos permitem mockar classes abstratas ou concretas, mas não classes final. Ambos também não permitem mockar métodos final. Por sorte, em ambos os casos, o mock de classe é um super conjunto de um mock de interface, por isso, se configurarmos o teste para mockar classe, podemos mockar interfaces no mesmo teste também. Os criadores preferem que os desenvolvedores codifiquem para interfaces ao invés de implementações, uma boa prática que sempre deveria ser seguida. Segue na **Listagem 14** um exemplo com EasyMock de como mockar uma classe.

```
import junit.framework.TestCase;
import static org.easymock.classextension.EasyMock.*;

public class Class_EasyMock extends TestCase {
  public void testSome() {
    AlgumaClass mock = createMock(AlgumaClass.class);
    // Programamos os mocks aqui
    replay(mock);

    // Setup do SUT

    verify(mock);
  }
}
```

**Listagem 14**. Exemplo de como Mockar uma classe utilizando EasyMock

Na **Listagem 15** segue o exemplo de como podemos mockar uma classe com JMock.

```
import org.jmock.integration.junit3.MockObjectTestCase;
import org.jmock.lib.legacy.ClassImposteriser;

public class Class_jMock extends MockObjectTestCase {
  protected void setUp() throws Exception {
    super.setUp();
    setImposteriser(ClassImposteriser.INSTANCE);
  }

  public void testExemplo() {
    AlgumaClasse mock = mock(AlgumaClasse.class);
    // Programamos os mocks aqui

    // Setup do SUT
  }
}
```

**Listagem 15**. Exemplo de como Mockar uma classe utilizando JMock

EasyMock implica apenas que alteremos o import para import static org.easymock.classextension.EasyMock.*. JMock por sua vez usa um Imposteriser para criar os Mocks. MockObjectTestCase usa um setUp que funciona apenas para interfaces por padrão, portanto temos que sobrescrever no nosso método setUp() se precisarmos mockar classes.

Nas **Listagens 16** e **17** temos um exemplo de como esperar um retorno de valor de um método em ambos os mocks mocando Map.class.

```
import junit.framework.TestCase;
import static org.easymock.EasyMock.*;
import java.util.Map;

public class CacheTesteEasyMock extends TestCase {
  public void testMetodoComRetornoDeValor() {
    int valorEsperado = 42;

    Map armazenaMock = createMock(Map.class);
    expect(armazenaMock.size()).andReturn(valorEsperado);
    replay(armazenaMock);

    Cache sut = new Cache(armazenaMock);
    Object valorAtual = sut.size();
    assertSame(valorEsperado, valorAtual);

    verify(armazenaMock);
  }
}
```

**Listagem 16**. Exemplo de como esperar retorno de métodos com EasyMock

```
import org.jmock.Expectations;
import org.jmock.integration.junit3.MockObjectTestCase;
import java.util.Map;

public class CacheTesteJMock extends MockObjectTestCase {
  public void testMetodoComValorDeRetornoLancaUmaExcecao () {
    final Exception excecaoEsperada = new RuntimeException();

    final Map armazenaMock = mock(Map.class);

    checking(new Expectations() {{
      one (armazenaMock).size();
      will(throwException(excecaoEsperada));
    }});

    Cache sut = new Cache(armazenaMock);
    try {
      sut.size();
      fail("Should have thrown the exception");
    } catch (RuntimeException excecaoAtual) {
      assertSame(excecaoEsperada, excecaoAtual);
    }
  }
}
```

**Listagem 17**. Exemplo de como esperar retorno de métodos com valores e com exceções com JMock

Para testar exceções o código no JMock utilizamos o trecho da **Listagem 18**.

```
checking(new Expectations() {{
  one (armazenaMock).size();
  will(throwException(excecaoEsperada));
}});
```

**Listagem 18**. Exemplo de como testar exceções com JMock

O EasyMock é bastante parecido, conforme segue o trecho da **Listagem 19**.

```
expect(query.list()).andThrow(
  new HibernateException("Algo terrivel aconteceu."));
```

**Listagem 19**. Exemplo de como testar exceções com EasyMock

Com EasyMock devemos usar o expectLastCall() quando lidamos com métodos void para configurar as expectations.

Podemos notar que ambos possuem praticamente as mesmas funcionalidades. Algumas pequenas funcionalidades são suportadas pelo JMock e não são suportadas pelo EasyMock e vice-versa. No entanto, o que muda mesmo é a leitura e a legibilidade do código.

### Comparando Diversos Mocks

Nesta sessão faremos uma comparação das funcionalidades dos três principais Mocks. Todos os recursos considerados abaixo fazem uma diferença notável para os desenvolvedores que criam testes com Mocks e por isso eles foram considerados.

| Característica                                               | EasyMock | jMock | Mockito |
| ------------------------------------------------------------ | -------- | ----- | ------- |
| Especificar número de invocações esperadas                   | x        | x     | x       |
| Gravar Expectations                                          | x        | x     | -       |
| Verificação Explicita                                        | -        | -     | x       |
| Mockagem Parcial                                             | x        | -     | x       |
| Sem chamada de método para alterar do modo de gravação para repetição | -        | -     | x       |
| Nenhum código extra para verificação implícita               | -        | -     | -       |
| Sem código extra para preparar o teste                       | x        | x     | x       |
| Não há necessidade de usar a anotação @RunWith ou classe base de teste | x        | x     | x       |
| Sintaxe consistente entre métodos voide não void             | -        | x     | -       |
| Argumentos do tipo matchers para alguns parâmetros apenas, não todos. | -        | -     | -       |
| Argumentos Matching mais fáceis de usar baseado em propriedades de valores de objetos. | x        | -     | x       |
| Mock sem cascata                                             | -        | -     | x       |
| Suporte para Mockar múltiplas interfaces                     | -        | -     | x       |
| Suporte para Mockar tipos de anotações                       | -        | x     | x       |
| Expectations parcialmente ordenadas                          | -        | x     | -       |
| Mockagem de construtores e métodos finais/static/native/private | -        | -     | -       |
| Mockagem de objetos “new-ed”                                 | -        | -     | -       |
| Suporte para Mockar tipos Enum                               | -        | -     | -       |
| Auto injeção de Mocks                                        | -        | -     | x       |
| Mocks declarativos para a classe de teste                    | -        | -     | x       |
| Mocks declarativos para métodos de teste                     | -        | -     | -       |
| Campos especiais para argumentos matching do tipo "any"      | -        | -     | -       |
| Uso de um campo especial para especificar o resultado da invocação | -        | -     | -       |
| Uso de campos especiais para especificar restrições de contagem de invocações. | -        | -     | -       |
| Expectations com mensagens de erro customizadas.             | -        | -     | -       |
| Mockagem sob demanda de classes de implementação não especificadas. | -        | -     | -       |
| Captura de instâncias criadas pelo código sob teste          | -        | -     | -       |
| Gravação e verificação das expectativas em laços             | -        | -     | -       |
| Suporte para tipos de retorno covariantes                    | -        | -     | -       |
| Único arquivo jar no class path é suficiente para usar a API. | -        | -     | x       |

**Tabela 1**. Comparação de algumas funcionalidades suportadas pelos principais Mocks

Como podemos verificar a maioria das funcionalidades são suportadas pelo Mockito, que é o mais completo entre eles. No entanto, grande parte das funcionalidades é suportada pelos três Mocks ou por uma combinação de dois deles o que implica em uma boa cobertura de funcionalidades dos principais Mocks disponíveis.

Podemos concluir que os Mocks nos permitem criar objetos de um determinado tipo (classe ou interface), para podermos isolar a classe a ser testada, com isso podemos focar somente na classe ou em um método da classe. Existem diversos Mocks disponíveis com características semelhantes, mas que diferem na legibilidade e na leitura do código. Utilizando Mocks também podemos abstrair a complexidade das dependências das classes permitindo um teste melhor e mais focado na classe. Porém, Mocks em excesso também podem atrapalhar, pois simular todas as dependências pode tornar o teste muito complexo e difícil de ser entendido. Os testes com muitos Mocks também ocultam problemas na colaboração entre objetos, sendo necessário também realizarmos testes de integração.

------

#### Referências Bibliográficas

- Meszaro, G. (2007) “XUnit Test Patterns”. Editora Addison Wesley.
- Fowler, M. “Mocks Aren't Stubs”
- Freeman, S. A brief History of Mock Objects

------

#### Links

- [Download do EasyMock](http://easymock.org/getting-started.html)
- [Documentação do EasyMock](http://easymock.org/user-guide.html)
- [Download do JMock](http://jmock.org/download)
- [JMock Getting Started](http://jmock.org/getting-started.html)
- [Documentação do Mockito](https://code.google.com/archive/p/mockito/downloads)

[![Um bate papo sobre Teste Unitário](https://www.devmedia.com.br/arquivos/noticias/devcast/devcast_um-bate-papo-sobre-teste-unitario_40173.png)Um bate papo sobre Teste UnitárioVídeo](https://www.devmedia.com.br/um-bate-papo-sobre-teste-unitario/40176)

[![Code Smells](https://www.devmedia.com.br/arquivos/noticias/devcast/devcast_um-bate-papo-sobre-code-smells_39636.png)Code SmellsVídeo](https://www.devmedia.com.br/code-smells-conheca-antes-que-seja-tarde/39636)

[![Definições Iniciais sobre Validação, Verificação e Testes](https://arquivo.devmedia.com.br/cursos/imagem/curso_309.jpg)Verificação e TestesCurso](https://www.devmedia.com.br/curso/definicoes-iniciais-sobre-validacao-verificacao-e-testes/309)

AnotarMarcar como concluído