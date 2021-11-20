# Conceitos básicos sobre Mockito

[![Thiago Alexandre Lenz](https://miro.medium.com/fit/c/96/96/1*zvk2vcreYDVVkGxHqhiBJA.jpeg)](https://medium.com/@thiagolenz?source=post_page-----73b931ce0c2c-----------------------------------)

[Thiago Alexandre Lenz](https://medium.com/@thiagolenz?source=post_page-----73b931ce0c2c-----------------------------------)Follow

[Oct 22, 2019](https://inside.contabilizei.com.br/conceitos-basicos-sobre-mockito-73b931ce0c2c?source=post_page-----73b931ce0c2c-----------------------------------) · 6 min read













![img](https://miro.medium.com/max/1400/1*7w64vyBXihVBrjNBBOIF9g.png)

Dois assuntos que não são novos mas vem ganhando força atualmente são: a utilização de TDD e testes unitários. Muitas pessoas idealizam e defendem, mas quando vão colocar na prática acabam esbarrando nas dificuldades de se isolar o domínio e responsabilidades a serem testadas.

Quando se fala em isolamento, estamos nos referindo a “mockar” ou esconder o comportamento de classes que são chamadas internamente em um trecho de código a ser testado, sem a necessidade de alterar o comportamento padrão, ou seja, não pode ser alterado nada do código a ser testado em função do teste, isso deve ser de forma transparente.

Esse artigo vai apresentar algumas das funcionalidades básicas do Mockito, um framework Java para auxiliar os testes unitários. Não serão tratados temas referentes a TDD, apenas exemplos fictícios de código utilizando esse framework.

# Exemplo 1

> Um serviço que faz uma validação de campos obrigatórios, e se satisfatório salva o registro em um repositório, caso contrário lança uma Exception.

Abaixo foi declarado uma classe ***PessoaService\*** que faz a regra que será testada:

![Classe PessoaService](https://miro.medium.com/max/60/1*yTFT1-Yw3g-nLNYy6xOE4w.png?q=20)

![Classe PessoaService]()

Classe PessoaService

O Teste unitário da classe:

![img](https://miro.medium.com/max/60/1*rTNVLQ5dCCnyfYjLT9jPRA.png?q=20)

![img]()

Teste unitário da classe PessoaService

Para que os testes possam rodar com o Mockito a classe de teste deve estar configurada para tal, isso é feito através da anotação ***@ RunWith\*** que faz referência a classe ***MockitoJUnitRunner.class\****.*

```
@RunWith(MockitoJUnitRunner.class)
public class PessoaServiceTest
```

Para entender mais sobre Runners do JUnit [clique aqui](https://www.concrete.com.br/2018/05/28/o-mundo-magico-do-junit-runners)

Em seguida vem os objetos a serem mockados, no caso ***PessoaRepository\***, através da anotação ***@ Mock\***. O Mockito vai criar uma cópia da estrutura dessa classe com uma implementação vazia e com retornos padrões em todos os métodos. Veja que não é necessário iniciar o objeto. O Mock pode ser feito tanto com classes concretas, abstratas e interfaces.

```
@Mock
private PessoaRepository pessoaRepository;
```

Agora vem a parte interessante, a classe que será testada. A declaração dessa classe é feita com a anotação ***@ InjectMocks\***. O Mockito vai criar uma instância real dessa classe e injetar todos os objetos ***@ Mock\*** que foram declarados na classe de teste.

```
@InjectMocks
private PessoaService pessoaService;
```

Com esses passos acima, já é possível rodar o teste da classe sem causar nenhum erro de ***NullPointer\***, pois todas as dependências foram devidamente injetadas.

> Um teste unitário bem escrito realiza verificações necessárias para garantir que resultado executado seja válido de acordo com as regras, caso contrário é apenas um teste *ByPass* (passou por aqui).

A verificação feita garante que o serviço ***PessoaService\*** ao final da validação, realizou uma chamada ao método *save* da classe ***PessoaRepository\*.** Isto é feito através do metodo ***verify\****(objeto, numero de chamadas).metodo(parametro)*:

```
verify(pessoaRepository, times(1)).save(pessoa);
```

# Exemplo 2

> Um serviço que faz uma consulta em um repositório que retorna uma lista de objetos Vendas de um vendedor. Soma o valor dos comissão de todas as vendas, e devolve um objeto TotalizadorComissao.

Considerando a seguinte classe de Serviço:

![img](https://miro.medium.com/max/60/1*DOo6rBz4tZlUytXLRt3muQ.png?q=20)

![img]()

Classe de serviço para gerar calcular comissão

Agora a classe de Teste:

![img](https://miro.medium.com/max/60/1*LBvI9ppxa6c6VsubBMDstw.png?q=20)

![img]()

Teste unitário da classe de gerador de Totalizador de Comissão

Seguindo o exemplo anterior, a classe de teste tem as configurações de execução, os ***Mocks\*** e o ***InjectMocks\***. A primeira diferença, é que agora é criado uma lista de vendas. Em seguida chama-se o método ***when\*** para utilizar essa lista. Esse comando abaixo determina que **quando o método findByCpfAndPeriodo for chamado com os parâmetros cpf e período, então retorne essa lista do cenário**.

```
List<Venda> vendas = Arrays.asList(
        createVenda(15, 150),
        createVenda(10, 100)
);
when(vendaRepository
        .findByCpfAndPeriodo(cpf, periodo))
        .thenReturn(vendas);
```

Isso significa que: quando o código real do serviço chamar o objeto Mockado do repositório, será retornado a lista de objetos de vendas de cada teste. Através disso é possível simular chamadas a recursos externos a classe, como acesso a um banco de dados por exemplo, sem se preocupar como funcionará essa consulta, não é responsabilidade desse teste.

A sintaxe do ***when\*** é essa:

```
when(objeto.metodo(params).then(retorno)
```

Na parte de *método(params)* a sintaxe implícita é essa abaixo, através do comando ***eq()\***:

```
when(objeto.metodo(eq(valor)).then(retorno)
```

Na linha acima essa configuração só vai ser válida para quando os valores passados sejam exatamente iguais aos configurados. Mas é possível utilizar variações, como o ***any().\*** Nesse caso, a configuração é mais abrangente, vale para qualquer valor de parâmetro.:

```
when(objeto.metodo(any()).then(retorno)
```

Porém, quando houver mais de um parâmetro, não é possível utilizar da forma abaixo, um erro será lançado e não vai ficar muito evidente. Será necessário utilizar o comando eq(valor).

```
// errado
when(objeto.metodo(valorA, any()).then(retorno)// certo 
when(objeto.metodo(eq(valorA), any()).then(retorno)
```

# Exemplo 3

> Um serviço que recebe uma entrada de entidade, converte para um DTO e em seguida chama uma classe que fará uma chamada REST para outro Sistema.

Abaixo é definido uma Classe Service responsável pela emissão de uma Venda em um sistema ERP. Essa classe monta um objeto DTO e chama um proxy, que é responsável por fazer a comunicação de baixo nível.

![img](https://miro.medium.com/max/60/1*_IT7BWTkXwk-mPCm7JdL1Q.png?q=20)

![img]()

Emissor de Venda Service

Abaixo a classe de Teste. Existem dois cenários: Teste para emitir com sucesso, e teste para verificar quando o proxy retornar uma exception.

![img](https://miro.medium.com/max/60/1*b2QkiohEeG-3k0zKvEWHkQ.png?q=20)

![img]()

Emissor de Venda Test

Esse terceiro exemplo possui exatamente a mesma estrutura dos anteriores, com adição de dois novos recursos ***Captor\*** e ***doThrow\***.

## Captor

O ***Captor\*** é um recurso para capturar valores de métodos mockados. Com isso é possível fazer ***asserts\*** mais detalhados, aprofundando o nível de verificação.

Para utilizar o ***Captor\*** no teste é necessário declarar uma variável com a anotação ***@ Captor\***:

```
@Captor
private ArgumentCaptor<VendaDTO> captor;
```

Agora é necessário chamar o método ***captor.capture()\*** dentro de uma chamada de ***verify()\*** conforme o exemplo abaixo:

```
verify(sistemaERPProxyService).emitir(captor.capture());
```

E para recuperar o valor capturado utiliza-se o método ***captor.getValue()\*** para objeto, ou ***getAllValues()\*** para recuperar uma lista de objetos.

```
VendaDTO value = captor.getValue();
```

## DoThrow

Testar *exceptions* é sempre um desafio, por muitas vezes é deixado de lado. Além de cobrir todos os cenários na implementação, também é necessário simular as diversas exceções em testes unitários.

Para aprimorar ainda mais o teste, é necessário que as camadas lancem as *exceptions* corretas, encapsulando outras exceções lançadas em camadas de mais baixo nível. Conforme o exemplo abaixo, quando for capturada uma exception verificada da classe ***SistemaERPProxyService\***, a mesma é encapsulada em um uma exception chamada ***EmissorVendaException:\***

```
try {
    sistemaERPProxyService.emitir(vendaDTO);
} catch (SistemaERPException e) {
    throw new EmissorVendaException(e);
}
```

Certo, e como testar isso? Através da funcionalidade ***doThrow\***. Primeiro ponto, no método de teste definimos que uma exception do tipo ***EmissorVendaException\*** deverá ser lançada no nosso cenário. Já dentro do método é declarado um objeto ***Venda\*** para o teste. Em seguida é feita a configuração para ser lançada a exception através da chamada: ***doThrow(exception).when(objeto).metodo(params)\***. Agora quando for chamado o método ***emissorVendaService.emitir(venda)\*** uma exception do tipo ***EmissorVendaException\*** será lançado.

```
@Test(expected = EmissorVendaException.class)
public void testErroEmitirVenda() throws EmissorVendaException, SistemaERPException {
    Venda venda = createVenda(0, 120);

    doThrow(new SistemaERPException())
            .when(sistemaERPProxyService).emitir(any());

    emissorVendaService.emitir(venda);
}
```

# Bônus

Uma dúvida que sempre fica no ar é: **O que é Stub e o que é Mock? Qual a diferença?** Esse [link](https://stackoverflow.com/questions/3459287/whats-the-difference-between-a-mock-stub?source=post_page-----e3f948f6d211----------------------) tem uma boa resposta para isso. Em resumo ***Mock\*** é mais voltado para teste de comportamento, com esse ciclo de vida:

```
initialize -> set expectations -> exercise -> verify
```

Já o ***Stub\*** é mais reduzido, ele tem foco voltado para teste de estado de objeto, com esse ciclo de vida:

```
initialize -> exercise -> verify
```

# Finalizando

Esse artigo foi para dar uma visão geral de algumas funcionalidades do Mockito. Foi apresentado que é possível fazer testes independente do framework adotado nas classes concretas, sem a necessidade de criar adaptações para funcionar o teste. Ainda tem bastante coisa a ser explorada na parte de *verify(), verifyZeroInteractions(), answer(), never(),* mocks parciais, métodos *void*, *@ Rule*, *spy()* e por ai vai.

Outras dicas, para deixar o código dos testes mais limpo e facilitar a leitura:

- Descreva bem o objetivo do teste no nome do método
- Utilize *import* *static* de métodos para deixar o código menos verboso

Espero que tenha sido útil para motivar as pessoas a finalmente implementar TDD de verdade. Comece sempre pelo básico, que com o tempo estará escrevendo testes bem avançados e de fácil manutenção.

Caso tenha alguma dúvida ou sugestão deixe nos comentários.

O código desses exemplos está disponível nesse [link ](https://gist.github.com/thiagolenz/47557bf4382aefb97b4535764b3b9d50)com os gists.