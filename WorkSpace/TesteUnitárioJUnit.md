[pode ajudar sua carreira.](https://www.devmedia.com.br/teste-unitario-com-junit/41235#modulo-mvp)

# Teste unitário com JUnit

## JUnit é uma API de código aberto para a criação de testes unitários em Java, bem como outras linguagem compatíveis com a JVM.

- 

[Artigos](https://www.devmedia.com.br/artigos/)[Java](https://www.devmedia.com.br/artigos/java)Teste unitário com JUnit

JUnit é uma API de código aberto para a criação de testes unitários em Java, bem como outras linguagem compatíveis com a JVM. Um dos seus principais projetistas, o cientista Erich Gamma, conhecido pelo livro Design Patterns: Elements of Reusable Object-Oriented Software, citou como a motivação por trás do JUnit permitir a criação de testes que são fáceis de escrever e executar. Aqui falamos sobre como começar nesta ferramenta.

### Visão geral

Escrever testes é a forma mais básica de garantir a qualidade do código. Ainda nos primeiros passos na programação costuma-se introduzir no código pequenos trechos de teste para verificar se o programa se comporta como esperado, em um dado momento da sua execução, mesmo sem usar nenhuma técnica para isso. Um exemplo é quando criamos uma classe com um método main() em um lugar qualquer do projeto, apenas para verificar se alguma funcionalidade do sistema está correta.

```
public static void main(String[] args) {
    ProdutoRepositorio repositorio = new ProdutoRepositorio();
    Produto produto = new Produto("Aparelho de barbear", 39.9, ...);
    repositorio.salvar(produto);
}
```

A medida que ganhamos experiência, principalmente quando começamos a lidar com sistemas maiores, é natural sentir falta de uma metodologia de testes que permita medir a cobertura do código testado, tornando fácil criar os cenários nos quais as falhas serão percebidas. Os testes unitários suprem essas e outras carências no processo de teste de código.

Supondo que com o código anterior desejamos validar se um produto que é cadastrado duas vezes com o mesmo nome faz o programa falhar, poderíamos escrever o seguinte teste para comprovar o lançamento de uma exceção.

```
@Test
public void testaAGravacaoDeUmProdutoJaCadastrado() {
    ProdutoRepositorio repositorio = new ProdutoRepositorio();
    Produto produto = new Produto("Aparelho de barbear", 39.9, ...);

    assertThrows(repositorio.salvar(produto), ProdutoComNomeJaCadastradoException.class) ;
}
```

Geralmente, escrevemos testes unitários com o auxílio de alguma API, que fornece as anotações e métodos que precisamos para isso. O programador Java conta com uma das primeiras criadas para esse fim e que influenciou o surgimento de muitas outras, o JUnit. Com ele, a partir de anotações e algumas declarações, conseguimos avaliar classes e métodos para saber se eles apresentam o comportamento desejado. Com o JUnit, também evitamos aquela prática tão comum de criar um método main() em qualquer lugar do projeto, apenas para saber se um certo trecho código está correto.

### Instalação

O primeiro pré-requisito para executar testes com o JUnit é ter em seu ambiente de desenvolvimento o Java versão 8 ou superior. Quanto a instalação, as duas principais ferramentas de gerenciamento de dependências em projetos Java atualmente são o Maven, predominante em projetos para a web, e o Gradle, padrão no Android. Aqui falaremos sobre como instalar o JUnit 5 em ambos os gerenciadores de dependência.

#### maven

Uma das formas mais fáceis de instalar o JUnit é através do seu repositório no maven. Para isso, em seu projeto localize o arquivo pom.xml, que é criado pela IDE no diretório raiz na maioria dos casos, e adicione nele as seguintes dependências:

```
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.3.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-params</artifactId>
        <version>5.3.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

Note que usamos acima o escopo de teste na declaração da dependência. Isso indica que os pacotes junit-jupiter-api e junit-jupiter-params serão necessários apenas durante as etapas de compilação e execução dos testes.

#### gradle

Caso você esteja utilizando o Gradle e o JUnit ainda não esteja disponível em seu ambiente de desenvolvimento, sua instalação pode ser feita da seguinte forma:

```
repositories {
    mavenCentral()
}

dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter-api:5.3.0'
    testImplementation 'org.junit.jupiter:junit-jupiter-params:5.3.0'
}

test {
    useJUnitPlatform()
}
```

Embora o JUnit possa ser instalado manualmente em um projeto Android, na maioria das vezes isso não é necessário, pois o Android Studio já adiciona o suporte aos testes unitários no projeto.

### Configuração

Para executar os testes com o JUnit precisamos de um motor de execução, que pode ser obtido pelo JAR junit-jupiter-engine, a qual também está disponível no repositório central do maven. A partir da sua versão 2016.2, o Intellij IDEA passou a integrar suporte a execução de testes dessa maneira, trazendo para o projeto os JARs necessários para isso. Contudo, apenas em versões posteriores isso passou a feito baseado na versão do JUnit utilizado pelo projeto, aquela informada no pom.xml. Portanto, caso você esteja trabalhando em uma versão da API diferente daquela hospedada pela IDE erros estranhos podem ser percebidos durante a execução dos testes.

Uma forma de evitar essa situação é adicionando manualmente os JARs que devem estar disponíveis em tempo de execução, sendo eles o junit-platform-launcher, junit-jupiter-engine e junit-vintage-engine. Em caso de problemas, veja abaixo como fazer essas configurações no maven e gradle.

#### maven

```
<dependency>
    <groupId>org.junit.platform</groupId>
    <artifactId>junit-platform-launcher</artifactId>
    <version>1.3.0</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-engine</artifactId>
    <version>5.3.0</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.junit.vintage</groupId>
    <artifactId>junit-vintage-engine</artifactId>
    <version>5.3.0</version>
    <scope>test</scope>
</dependency>
```

#### gradle

```
testRuntime("org.junit.platform:junit-platform-launcher:1.3.0")
testRuntime("org.junit.jupiter:junit-jupiter-engine:5.3.0")
testRuntime("org.junit.vintage:junit-vintage-engine:5.3.0")
```

No Intellij IDEA, quando criamos um projeto do maven, em sua estrutura é adicionada a pasta test. É dentro dela que criamos os pacotes e as classes de teste do projeto.

### Escrevendo testes

Escrever uma classe de teste consiste em utilizar alguns métodos e anotações da API do JUnit, criando assim pequenos cenários nos quais identificamos se o comportamento de uma unidade de trabalho corresponde ao esperado. Aqui você será apresentado a exemplo reais de teste de software, sendo introduzido passo a passo nos testes unitários com JUnit.

### Visão geral

Em geral, boa parte dos códigos de teste serão criados para implementar algum ou todos os passos a seguir:

- Reunir um conjunto de objetos e iniciá-los, se necessário
- Fazer com esses objetos executem suas tarefas de acordo com um contexto
- Assegurar que um resultado é aquele esperado

O código abaixo age conforme especificado acima, passando por cada um dos três passos, onde assegurar o resultado esperado é papel desempenhado pelo método estático assertEquals.

```
class Junit5Exemplo {

    @Test
    void meuPrimeiroTeste() {
        assertEquals(2, 1 + 1);
    }
}
```

Ao longo desta documentação veremos outros exemplos de como utilizar os métodos estáticos da classe Assertions, os quais são parte importante do processo de escrita de testes.

### Na prática

#### Exemplo 1

A primeira anotação a ser utilizada para criar testes unitários é @Test, que informa ao JUnit quais são os métodos de teste de uma classe. Para o JUnit o nome do método não importa, pois desde de que ele seja anotado dessa maneira ele será identificado como um método de teste.

**Nota:** Um método anotado com @Test não deve retornar um valor.

Considere que estamos trabalhando no módulo de vendas em um projeto de software e que como regra de negócio um produto jamais possa ser ativado se seu preço for menor ou igual a zero. O código que implementa essa regra poderia se parecer com este:

```
public class ProdutoValidador {

    public void validar(Produto produto) {
        if (produto.getPreco() <= 0 && (produto.getStatus() == null || produto.getStatus() == ProdutoStatus.ATIVO)) {
            throw new ProdutoAtivadoSemPrecoException();
        }
    }
}
```

Agora, para assegurar a consistência dessa validação podemos escrever uma classe de teste e verificar se quando o produto possui preço zero e estado ativo a exceção correspondente será lançada. Embora seja este o modificador que usamos abaixo, um método ou classe de teste não precisa ser público.

```
public class ProdutoValidadorTest {

    @Test
    @DisplayName("Verifica se um produto está ativo e possui um preço válido")
    public void verificaSeProdutoAtivoSemPrecoLancaExcecao() {
        Produto produto = new Produto("Aparelho de Barbear", 10, ProdutoStatus.ATIVO);

        ProdutoValidador validador = new ProdutoValidador();
        assertThrows(ProdutoAtivadoSemPrecoException.class, () -> validador.validar(produto));
    }
}
```

Nesse cenário construído para falha é o método assertThrows() quem verifica se obtivemos êxito em fazer com que validar() falhe. Assim como este, existem muitos outros métodos conhecidos como Assertions, cada um deles escrito para assegurar o retorno de um valor específico.

#### Exemplo 2

Algumas vezes precisamos utilizar um conjunto de valores nos testes, a fim de verificar em que cenários eles serão concluídos com êxito ou falha. Considere que estamos desenvolvendo uma classe de validação de e-mail que será utilizada por diversos sistemas conectados a um conjunto de APIs. Existem diversas situações em que um e-mail poderá ser considerado inválido, podendo um teste parametrizados ajudar a identifica-los.

```
public class EmailValidadorTest {

    @ParameterizedTest
    @ValueSource(strings = {"", "mail", "mail@mail", "mail@mail.com"})
    public void verificaSeEmailEValido(String email) {
        assertTrue(Email.validar(email));
    }
}
```

Para escrever um teste parametrizado devemos utilizar a anotação @ParameterizedTest em conjunto de @ValueSource, assim como exemplificamos abaixo. Nesse caso, ao executarmos os testes o método verificaSeEmailEValido() será chamado uma vez para cada parâmetro especificado em @ValueSource. Uma vez que apenas o último valor corresponde a um e-mail válido, os três primeiros casos resultarão em falha.

#### Exemplo 3

JUnit provê uma forma de executarmos um teste diversas vezes anotando-o com a anotação @RepeatedTest, a qual recebe o número repetições desejado. Cada execução de um método anotado dessa maneira é performada como se estivéssemos utilizando a anotação @Test.

Imagine que desejamos verificar se um segundo salvamento de um produto que possui os mesmos dados de algum anteriormente presente no banco de dados, nome, preço, enfim, lança uma exceção indicando uma duplicidade no cadastro.

```
public class ProdutoRepositorioTest {

    @RepeatedTest(2)
    public void cadastrar() {
        ...
        assertThrows(ProdutoDuplicadoException.class, repositorio.grava(produto));
    }
}
```

Nesse contexto, é provável que na primeira execução este método passe, mas que ele falhe em sua segunda chamada.

#### Exemplo 4

Uma novidade no JUnit 5 são os testes dinâmicos, que nos permitem criar casos de teste em tempo de execução, compostos por um nome e um Executable, dentro de um método de fabricação de testes. Com esse recurso podemos usar os dados em uma coleção como fonte para a criação de diferentes contextos de falha, criando um teste para cada um de seus itens dinamicamente, de forma que eles sejam executados pelo JUnit através de Iterator. Abaixo temos um exemplo onde relacionamos os endereços e CEPs em duas listas diferentes, passando cada endereço por serviço que deve retornar o CEP correspondente.

```
@TestFactory
public Collection<DynamicTest> testaSeOCepParaUmEnderecoFoiEncontrado() {
    List<String> enderecos =
            new ArrayList<>(Arrays.asList("Rua dos Andrades N 435", ...));

    List<String> ceps =
            new ArrayList<>(Arrays.asList("22343234"...));

    Collection<DynamicTest> dynamicTests = new ArrayList<>();

    for (int i = 0; i < enderecos.size(); i++) {
        String endereco = enderecos.get(i);
        String cep = ceps.get(i);

        Executable executable = () -> assertEquals(cep, Correios.cep(endereco));
        String titulo = "Testando endereco " + endereco;
        DynamicTest dynamicTest = DynamicTest.dynamicTest(titulo, executable);

        dynamicTests.add(dynamicTest);
    }

    return dynamicTests;
}
```

Para item na lista, o objeto Executable, quando executado, fará uma requisição através do serviço Correios, que deve retornar o CEP que corresponde ao item de mesma posição na coleção de CEPs. Note que este código apenas cria casos de teste, mas ele mesmo não os executa. Por conta disso, um método criado dessa maneira deve ser anotado com @TestFactory e retornar uma coleção de objetos do tipo DynamicTest, que serão um a um executados pelo JUnit.

É muito comum vermos testes dinâmicos serem escritos utilizando expressões lambda. Portanto, segue abaixo uma outra versão do código acima, refeito dessa maneira.

```
@TestFactory
public Iterator<DynamicTest> testaSeOCepParaUmEnderecoFoiEncontrado() {
    List<String> enderecos =
            new ArrayList<>(Arrays.asList("Rua dos Andrades N 435", ...));

    List<String> ceps =
            new ArrayList<>(Arrays.asList("22343234"...));

    return enderecos.stream().map(endereco ->
            DynamicTest.dynamicTest("Testando endereco " + endereco, () -> {
                        int indice = enderecos.indexOf(endereco);
                        assertEquals(ceps.get(indice), Correios.cep(endereco));
                    }
            )).iterator();
}
```

#### Exemplo 5

Podemos também usar testes dinâmicos para lidar com cenários diferentes de falha para um certo grupo de objetos. No caso abaixo desejamos validar se um objeto inválido gera uma exceção para cada uma das formas de iniciá-lo a partir de um dos seus construtores.

```
@TestFactory
public Collection<DynamicTest> testaSeUmUsuarioComDadosInvalidosLancaUmaExcecao() {
    List<Usuario> usuarios = new ArrayList<Usuario>() {{
        add(new Usuario(null, null));
        add(new Usuario(null, ""));
        add(new Usuario("", null));
        add(new Usuario("", ""));
    }};

    Collection<DynamicTest> dynamicTests = new ArrayList<>();

    usuarios.stream().map(usuario ->
            DynamicTest.dynamicTest("Testando usuario " + usuario.getNickname() + " " + usuario.getPassword(), () -> {
                        assertThrows(UsuarioInvalidoException.class, UsuarioValidador.validar(usuario));
                    }
            )).iterator();

    return dynamicTests;
}
```

### Executando classes de teste no Intellij IDEA

Assim como demonstra a imagem abaixo, é possível clicar sobre a pasta test/java e no menu de contexto será apresentada a opção Run 'All Tests', disponível também no atalho Ctrl+Shift+F10.

![Opção para executar todos os testes](https://arquivo.devmedia.com.br/exemplo/EstevaoDias/DocumentacaoJUnit/runAllTests.png)

**Figura 1**. Opção para executar todos os testes

Com isso, serão executados todos os testes escritos nas classes que estão nesta pasta. Não se preocupe em como o JUnit identifica uma classe de teste nesse momento, pois veremos isso em detalhes na próxima seção. Ao concluir a execução dos testes o Intellij IDEA apresentará a seguinte janela:

![Opção para executar todos os testes](https://arquivo.devmedia.com.br/exemplo/EstevaoDias/DocumentacaoJUnit/runAllTests4.jpg)

**Figura 2**. Teste sendo executado com sucesso.

Ao executar esse teste ele será concluído com sucesso, pois nessas condições a classe ProdutoValidador lançará uma exceção no método validar(), conforme apresenta a imagem acima.

### Ambiente

Uma vez que cada teste deve ser executado de forma isolada e independente, a fim de garantir que eles não sofram com a ausência de dependências ou a sobra de instâncias de objetos usados em testes anteriores, é importante que saibamos utilizar os mecanismos disponíveis para a criação e destruição de ambientes isolados de teste, assunto tratado nesta seção da documentação.

### Visão geral

Grandes aplicações costumam executar seus testes de forma autônoma, em um processo que pode durar horas até que todo o sistema esteja coberto por eles. Nesse contexto, é importante que cada teste na pilha possa ser executado sem nenhuma conexão com o anterior como uma garantia de que a falha em um determinado teste não comprometerá a confiabilidade dos seguintes. De outra forma, pode ser necessário rastrear a origem problemas como testes que falham dependendo da ordem em que são executados, o que pode facilmente consumir algumas horas do programador.

Assim, podemos concluir que um teste confiável deve:

- Iniciar objetos e dependências
- Executar as ações necessárias para a avaliação de um resultado
- Remover objetos e dependências da memória

Uma alternativa para evitar esse e outros cenários caóticos onde haja alguma interdependência entre dois ou mais testes o JUnit oferece dois mecanismos, @BeforeEach e @AfterEach. @BeforeEach, o método da classe que é executado antes de cada teste, nos permite inicializar objetos ou realizar qualquer tarefa relacionada a preparação de um ambiente adequado para que os objetos reunidos em um contexto executem as suas ações de forma consistente e isolada. @AfterEach desfaz esse ambiente, removendo da memória caches, fechando streams ou quaisquer outros dados que poderiam comprometer a confiabilidade do próximo teste.

Tanto @BeforeEach quanto @AfterEach podem ser utilizados com as anotações @Test, @RepeatedTest, @ParameterizedTest ou @TestFactory.

### Na prática

#### Exemplo 1

Embora seja um recurso útil, devemos evitar utilizar as anotações @BeforeEach e @AfterEach quando forem desnecessárias, uma vez que elas podem tornar a leitura do código mais difícil, visto que para acompanhar o que ele faz o programador deverá dividir a sua atenção entre alguns métodos. Abaixo vemos um caso no qual utilizar essas anotações é algo dispensável e indevido.

```
class TestaDeValidadeDoArquivoDeLog {

    private Logger logger;

    @BeforeEach
    public void setUp() {
        logger = // Inicia o log
    }

    @Test
    public void testaSeOArquivoDeLogEValido() {
        ...
        assertTrue("Arquivo de log invalido", logger.validaArquivoDeLog("20181110.log"));
        ...
    }

    @AfterEach
    public void tearDown() {
        logger = null; // Instrução desnecessária
    }
}
```

Uma outra versão do código acima pode ser obtida da seguinte forma:

```
class TestaDeValidadeDoArquivoDeLog {

    private Logger logger;

    @Test
    public void testaSeOArquivoDeLogEValido() {
        logger = criaLoggerParaTeste();
        ...
        assertTrue("Arquivo de log invalido", logger.validaArquivoDeLog("20181110.log"));
        ...
    }

    public Logger criaLoggerParaTeste() {
        return Logger.getLogger(getClass().getCanonicalName());
    }
}
```

Nesta nova versão do código a cada vez que precisamos de uma nova instância de Logger solicitamos ao método de fábrica que gere uma nova, dessa forma descartando a anterior.

#### Exemplo 2

De acordo com Osherove, uma das aplicações justificáveis para esse mecanismo é o desfazimento de estados globais, geralmente associados a objetos estáticos, como singletons. De acordo com ele, se necessitamos iniciar ou destruir objetos específicos desta forma estamos nos aproximando de testes de integração, o que não deveria ser uma preocupação nesse momento, sendo implementado em um próximo projeto de testes.

Para ilustrar esse cenário, considere que estamos escrevendo um código de testes no qual necessitamos utilizar alguns objetos estáticos, criados a partir de um Singleton. Uma vez que esses objetos não serão removidos da memória ou recriados automaticamente após encerrado o escopo dos métodos de teste, passa a ser necessário tratar a memória de alguma outra forma. No exemplo a seguir reiniciamos esses objetos globais com as anotações @BeforeEach e @AfterEach, destruindo qualquer resquício de dado que poderia comprometer os próximos testes que utilizam os mesmos.

```
class TestaCadastroDeUsuarioJaCadastrado {

    private EntityManager em;

    @Test
    public void testaSeOArquivoDeLogEValido() {
        em = JpaUtil.getEntityManager();
        ...
        assertThrows(EmailJaCadastradoException.class, em.persist(usuario));
        ...
        em.close();
    }

    @AfterEach
    public void tearDown() {
        em = null;
    }
}
```

Perceba que tarefas de rotina, como a inicialização do EntityManager e o fechamento da sessão são realizadas em um mesmo contexto, dentro do método de teste. Outras ações, como a destruição desse objeto e quaisquer informações vinculadas ou mantidas por ele ficam ao encargo da API, que chamará, após cada um dos testes, o método para destruição do ambiente de teste.

### Assertions

A classe Assertions é uma coleção de métodos que afirmam se certas condições comuns em testes correspondem ao esperado.

### Visão geral

Os métodos estáticos da classe Assertions são parte importante dos casos de teste e avaliam se certas condições, decisivas para determinar o sucesso ou falha do teste, geram um resultado esperado. Geralmente esses métodos lançam uma exceção do tipo AssertionFailedError.

```
import static org.junit.jupiter.api.Assertions.*;
...
assertEquals(2026.43, funcionario.getSalarioLiquido());
assertEquals(2026.43, funcionario.getSalarioLiquido(), "Comparação de salário líquido após descontos");
...
```

Tem se tornado uma convenção entre os desenvolvedores usar import static em lugar de utilizar o nome da classe para acessar os seus métodos estáticos. Para isso podemos utilizar a seguinte declaração:

### Principais métodos da classe Assertions

#### assertTrue

Requer que a condição booleana seja verdadeira.

```
public static void assertTrue(boolean condition)
public static void assertTrue(boolean condition,
    Supplier<String> messageSupplier)
public static void assertTrue(BooleanSupplier booleanSupplier)
public static void assertTrue(BooleanSupplier booleanSupplier,
    String message)
public static void assertTrue(boolean condition,
    String message)
public static void assertTrue(BooleanSupplier booleanSupplier,
    Supplier<String> messageSupplier)
```

#### assertFalse

Requer que a condição booleana seja falsa.

```
public static void assertFalse(boolean condition)
public static void assertFalse(boolean condition,
    String message)
public static void assertFalse(boolean condition,
    Supplier<String> messageSupplier)
public static void assertFalse(BooleanSupplier booleanSupplier)
public static void assertFalse(BooleanSupplier booleanSupplier,
    String message)
public static void assertFalse(BooleanSupplier booleanSupplier,
    Supplier<String> messageSupplier)
```

#### assertNull

Requer que o valor informado como parâmetro seja nulo.

```
public static void assertNull(Object actual)
public static void assertNull(Object actual,
    String message)
public static void assertNull(Object actual,
    Supplier<String> messageSupplier)
```

#### assertNotNull

Requer que o valor informado como parâmetro não seja nulo.

```
public static void assertNotNull(Object actual)
public static void assertNull(Object actual,
    String message)
public static void assertNotNull(Object actual,
    String message)
public static void assertNotNull(Object actual,
    Supplier<String> messageSupplier)
```

#### assertEquals

Requer que ambos os valores passados como parâmetro sejam verdadeiros.

```
public static void assertEquals(short expected,
    short actual)
public static void assertEquals(short expected,
    short actual, String message)
public static void assertEquals(short expected,
    short actual, Supplier<String> messageSupplier)
public static void assertEquals(byte expected,
    byte actual)
public static void assertEquals(byte expected,
    byte actual, String message)
public static void assertEquals(byte expected,
    byte actual, Supplier<String> messageSupplier)
public static void assertEquals(int expected,
    int actual)
public static void assertEquals(int expected,
    int actual, String message)
public static void assertEquals(int expected,
    int actual, Supplier<String> messageSupplier)
public static void assertEquals(long expected,
    long actual)
public static void assertEquals(long expected,
    long actual, String message)
public static void assertEquals(long expected,
    long actual, Supplier<String> messageSupplier)
public static void assertEquals(char expected,
    char actual)
public static void assertEquals(char expected,
    char actual, String message)
public static void assertEquals(char expected,
    char actual, Supplier<String> messageSupplier)
public static void assertEquals(float expected,
    float actual)
public static void assertEquals(float expected,
    float actual, String message)
public static void assertEquals(float expected,
    float actual, Supplier<String> messageSupplier)
public static void assertEquals(float expected,
    float actual, float delta)
public static void assertEquals(float expected,
    float actual, float delta, String message)
public static void assertEquals(float expected,
    float actual, float delta, Supplier<String> messageSupplier)
public static void assertEquals(double expected,
    double actual)
public static void assertEquals(double expected,
    double actual, String message)
public static void assertEquals(double expected,
    double actual, Supplier<String> messageSupplier)
public static void assertEquals(double expected,
    double actual, double delta)
public static void assertEquals(double expected,
    double actual, double delta, String message)
public static void assertEquals(double expected,
    double actual, double delta, Supplier<String> messageSupplier)
public static void assertEquals(Object expected,
    Object actual)
public static void assertEquals(Object expected,
    Object actual, String message)
public static void assertEquals(Object expected,
    Object actual, Supplier<String> messageSupplier)
```

#### assertArrayEquals

Requer que ambos os vetores sejam iguais.

```
public static void assertArrayEquals(boolean[] expected,
    boolean[] actual)
public static void assertArrayEquals(boolean[] expected,
    boolean[] actual, String message)
public static void assertArrayEquals(boolean[] expected,
    boolean[] actual, Supplier<String> messageSupplier)
public static void assertArrayEquals(char[] expected,
    char[] actual)
public static void assertArrayEquals(char[] expected,
    char[] actual, String message)
public static void assertArrayEquals(char[] expected,
    char[] actual, Supplier<String> messageSupplier)
public static void assertArrayEquals(byte[] expected,
    byte[] actual)
public static void assertArrayEquals(byte[] expected,
    byte[] actual, String message)
public static void assertArrayEquals(byte[] expected,
    byte[] actual, Supplier<String> messageSupplier)
public static void assertArrayEquals(short[] expected,
    short[] actual)
public static void assertArrayEquals(short[] expected,
    short[] actual, String message)
public static void assertArrayEquals(short[] expected,
    short[] actual, Supplier<String> messageSupplier)
public static void assertArrayEquals(int[] expected,
    int[] actual)
public static void assertArrayEquals(int[] expected,
    int[] actual, String message)
public static void assertArrayEquals(int[] expected,
    int[] actual, Supplier<String> messageSupplier)
public static void assertArrayEquals(long[] expected,
    long[] actual)
public static void assertArrayEquals(long[] expected,
    long[] actual, String message)
public static void assertArrayEquals(long[] expected,
    long[] actual, Supplier<String> messageSupplier)
public static void assertArrayEquals(float[] expected,
    float[] actual)
public static void assertArrayEquals(float[] expected,
    float[] actual, String message)
public static void assertArrayEquals(float[] expected,
    float[] actual, Supplier<String> messageSupplier)
public static void assertArrayEquals(float[] expected,
    float[] actual, float delta)
public static void assertArrayEquals(float[] expected,
    float[] actual, float delta, String message)
public static void assertArrayEquals(float[] expected,
    float[] actual, float delta, Supplier<String> messageSupplier)
public static void assertArrayEquals(double[] expected,
    double[] actual)
public static void assertArrayEquals(double[] expected,
    double[] actual, String message)
public static void assertArrayEquals(double[] expected,
    double[] actual, Supplier<String> messageSupplier)
public static void assertArrayEquals(double[] expected,
    double[] actual, double delta)
public static void assertArrayEquals(double[] expected,
    double[] actual, double delta, String message)
public static void assertArrayEquals(double[] expected,
    double[] actual, double delta, Supplier<String> messageSupplier)
public static void assertArrayEquals(Object[] expected,
    Object[] actual)
public static void assertArrayEquals(Object[] expected,
    Object[] actual, String message)
public static void assertArrayEquals(Object[] expected,
    Object[] actual, Supplier<String> messageSupplier)
```

#### assertIterableEquals

Requer que todos os objetos do tipo Iterable passados como parâmetro sejam iguais.

```
public static void assertIterableEquals(Iterable<?> expected,
    Iterable<?> actual)
public static void assertIterableEquals(Iterable<?> expected,
    Iterable<?> actual, String message)
public static void assertIterableEquals(Iterable<?> expected,
    Iterable<?> actual, Supplier<String> messageSupplier)
```

#### assertLinesMatch

Requer que ambas as listas de strings sejam iguais.

```
public static void assertLinesMatch(List<String> expectedLines,
    List<String> actualLines)
```

#### assertNotEquals

Requer que ambos os valores passados como parâmetro sejam iguais.

```
public static void assertNotEquals(Object unexpected,
    Object actual)
public static void assertNotEquals(Object unexpected,
    Object actual, String message)
public static void assertNotEquals(Object unexpected,
    Object actual, Supplier<String> messageSupplier)
```

#### assertSame

Requer que ambos os parâmetros se refiram ao mesmo objeto.

```
public static void assertSame(Object expected,
    Object actual)
public static void assertSame(Object expected,
    Object actual, String message)
public static void assertSame(Object expected,
    Object actual, Supplier<String> messageSupplier)
```

#### assertNotSame

Requer que ambos os parâmetros se refiram a objetos diferentes.

```
public static void assertNotSame(Object unexpected,
    Object actual)
public static void assertNotSame(Object unexpected,
    Object actual, String message)
public static void assertNotSame(Object unexpected,
    Object actual, Supplier<String> messageSupplier)
```

#### assertAll

Requer que todos os objetos do tipo Executable passados como parâmetro não lançam exceções.

```
public static void assertAll(Executable... executables)
    throws MultipleFailuresError
public static void assertAll(Stream<Executable> executables)
    throws MultipleFailuresError
public static void assertAll(String heading, Executable... executables)
    throws MultipleFailuresError
public static void assertAll(String heading, Stream<Executable> executables)
    throws MultipleFailuresError
```

#### assertThrows

Requer que a execução do objeto do tipo Executable passado como parâmetro lance um exceção do tipo esperado.

```
public static <T extends Throwable> T assertThrows(Class<T> expectedType,
    Executable executable)
public static <T extends Throwable> T assertThrows(Class<T> expectedType,
    Executable executable, String message)
public static <T extends Throwable> T assertThrows(Class<T> expectedType,
    Executable executable, Supplier<String> messageSupplier)
```

#### assertTimeout

Requer que uma execução se complete antes do tempo estimado.

```
public static void assertTimeout(Duration timeout,
    Executable executable)
public static void assertTimeout(Duration timeout,
    Executable executable, String message)
public static void assertTimeout(Duration timeout,
    Executable executable, Supplier<String> messageSupplier)
public static <T> T assertTimeout(Duration timeout,
    ThrowingSupplier<T> supplier)
public static <T> T assertTimeout(Duration timeout,
    ThrowingSupplier<T> supplier, String message)
public static <T> T assertTimeout(Duration timeout,
    ThrowingSupplier<T> supplier, Supplier<String> messageSupplier)
```

#### assertTimeoutPreemptively

Requer que uma execução se complete após do tempo estimado.

```
public static void assertTimeoutPreemptively(Duration timeout,
    Executable executable)
public static void assertTimeoutPreemptively(Duration timeout,
    Executable executable, String message)
public static void assertTimeoutPreemptively(Duration timeout,
    Executable executable, Supplier<String> messageSupplier)
public static <T> T assertTimeoutPreemptively(Duration timeout,
    ThrowingSupplier<T> supplier)
public static <T> T assertTimeoutPreemptively(Duration timeout,
    ThrowingSupplier<T> supplier, String message)
public static <T> T assertTimeoutPreemptively(Duration timeout,
    ThrowingSupplier<T> supplier, Supplier<String> messageSupplier)
```

AnotarMarcar como concluído