# Testando seu código Java com o Mockito framework

[![Silas Candiolli](https://miro.medium.com/fit/c/96/96/1*HOic839bjnQsoqfu5-VrRg.jpeg)](https://medium.com/@candiolli?source=post_page-----8bea7287460a-----------------------------------)  -  [Silas Candiolli](https://medium.com/@candiolli?source=post_page-----8bea7287460a-----------------------------------)  -  [Nov 12, 2020](https://medium.com/cwi-software/testando-seu-código-java-com-o-mockito-framework-8bea7287460a?source=post_page-----8bea7287460a-----------------------------------) · 4 min read



![img](https://miro.medium.com/max/1400/1*Geliad9bjwlnh2moys_YrA.jpeg)

[Engadget](https://www.engadget.com/2019-07-30-facebook-fact-checker-more-work-is-needed-to-curb-fake-news.html)

Utilizo o Mockito faz alguns anos, e considero uma ferramenta muito poderosa. Eu vejo que seria muito complicado criar testes sem ele. Mas nem sempre foi facil utiliza-lo, não por causa do Mockito, mas sim por minha causa. Pois **pensar orientado a testes é dificil** no começo.

De forma prática, quero trazer exemplos de utilização do Mockito em casos reais do meu dia a dia, e mostrar como ele pode nos ajudar a testar codigo complexos.

# O que é o Mockito?

O Mockito é um framework de testes unitários e o seu principal objetivo é instanciar classes e controlar o comportamento dos métodos. Isso é chamado de *mock,* na tradução livre quer dizer *zombar,* e talvez seja mesmo o termo que melhor o define. Pois ao *mockar* a dependencia de uma classe, eu faço com que a classe que estou testando pense estar invocando o metodo realmente, mas de fato não está. Conforme o desenho abaixo tenta explicar.

![img](https://miro.medium.com/max/60/1*Y5OEPlXdLblECPh3jRjoTw.png?q=20)

![img](https://miro.medium.com/max/630/1*Y5OEPlXdLblECPh3jRjoTw.png)

Fluxo quando chamar o metodo mockado

# Configurando

A instalação do Mockito no seu projeto é muito simples, assim como sua utilização. Seguindo o *how to* do [site](https://site.mockito.org/#how) é bem facil de fazer.

Após o Mockito estar nas dependencias do seu projeto, ja é possível anotar suas classes e criar *mocks.* E ai você tem algumas formas de testar seus metodos, que podem variar conforme a sua implementação.

Para os exemplos a seguir utilizei as seguintes bibliotecas:

- Java 11
- Mockito 3.6.0
- JUnit 5.4.2
- Lombok 1.18.16

# Resumo

- Mock: cria uma instancia de uma classe, porém Mockada. Se você chamar um metodo ele não irá chamar o metodo real, a não ser que você queira.
- Spy: cria uma instancia de uma classe, que você pode mockar ou chamar os metodos reais. É uma alternativa ao *InjectMocks,* quando é preciso mockar metodos da propria classe que esta sendo testada.
- InjectMocks: criar uma intancia e injeta as dependências necessárias que estão anotadas com *@Mock.*
- Verify: verifica a quantidade de vezes e quais parametros utilizados para acessar um determinado metodo.
- When: Após um mock ser criado, você pode direcionar um retorno para um metodo dado um paremetro de entrada.
- Given: Mesmo propósito que o *when*, porém é utilizado para BDD. Fazendo parte do BDDMockito.

# Praticando

Nesse ponto quero desmostrar a utilização do *Mock/@Mock.* Com esse metodo, é possível instanciar uma classe dependente da classe que voce esta testando, e mockar seus metodos. Isso é importante para, **testar a unidade.** Pois conseguimos isolar o comportamento de um metodo, por isso são chamados de testes unitários.

Quando criamos testes é possível perceber o quão complexo ficou nosso código. **Geralmente, se existes muitas dependencias em uma classe, significa que ela poderia ser quebrada em mais de uma. O mesmo vale para os metodos.**

A divisão de camadas e pacotes de um software existe para diminuir o acoplamento e manter a coesão, fazendo com que as classes e metodos tenham uma unica responsabilidade. Isso torna a leitura e manutenção do código mais simples.

**1. Mock | When**

Nesse exemplo abaixo, criei um *mock()* da classe *CustomerRegister* para testar o comportamento do metodo *validateRealCpf* . Evidentemente, eu terei um resultado positivo, independente do valor que eu passar para ser validado. Isso ocorre porque eu utilizei o *when().*

<iframe src="https://medium.com/media/6c51a91ef885f44ff538959756f08675" allowfullscreen="" frameborder="0" height="193" width="680" title="" class="t u v jt aj" scrolling="auto" style="box-sizing: inherit; position: absolute; top: 0px; left: 0px; width: 680px; height: 192.986px;"></iframe>

Agora, se eu chamar o metodo real, utilizando o *thenCallRealMethod()* do Mockito, o teste falha. Porque o CPF informado é inválido, e o meu teste passou pelo metodo *validateRealCpf()* de fato.

<iframe src="https://medium.com/media/bb8cb6de547033d1a88d3513c3a17d72" allowfullscreen="" frameborder="0" height="193" width="680" title="" class="t u v jt aj" scrolling="auto" style="box-sizing: inherit; position: absolute; top: 0px; left: 0px; width: 680px; height: 192.986px;"></iframe>

**2. InjectMocks**

Eu posso usar o *mock()* em outros contextos pouco mais complexos, como para obter um resultado positivo do *repository.save(),* independente do que este receba como parametro de entrada. No exemplo abaixo utilizei as anotações *@InjectMock*s, *@Mock* e *@BeforeEach* conforme codigo abaixo:

<iframe src="https://medium.com/media/cdec746ce27aee224d5bf6302d3f2fe0" allowfullscreen="" frameborder="0" height="721" width="680" title="" class="t u v jt aj" scrolling="auto" style="box-sizing: inherit; position: absolute; top: 0px; left: 0px; width: 680px; height: 720.99px;"></iframe>

**3. Spy**

No exemplo seguinte, farei um teste utilizando a função S*py()/@Spy,* que possibilita *mockar* a classe que está sendo testada. Algo que você não consegue fazer utilizando somente o *@InjectMocks.* Vejamos o exemplo abaixo:

<iframe src="https://medium.com/media/442f45dd7b881d63408204877a594b9c" allowfullscreen="" frameborder="0" height="788" width="680" title="" class="t u v jt aj" scrolling="auto" style="box-sizing: inherit; position: absolute; top: 0px; left: 0px; width: 680px; height: 787.986px;"></iframe>

**3. Verify**

No exemplo abaixo, vou explorar alguns casos de uso do *verify().*

É possível fazer verificar por quantidade de interação:

```
verify(customerRegister, times(1)).register(vo);
```

Verificar quando não houver interação:

```
verifyNoInteractions(repository);
```

Verificar quando não houver outras interações além das que eu ja verifiquei, utilizar o *verifyNoMoreInteractions(),* por exemplo:

<iframe src="https://medium.com/media/8ae82646d126040247e059682bb7ad7a" allowfullscreen="" frameborder="0" height="413" width="680" title="" class="t u v jt aj" scrolling="auto" style="box-sizing: inherit; position: absolute; top: 0px; left: 0px; width: 680px; height: 412.986px;"></iframe>

# Conclusão

Para concluir, eu gostaria de ressaltar a importancia desse framework para o nosso dia a dia. Todos sabemos que é necessário testar, e o Mockito é uma ótima ferramenta para isso, pois é a possibilidade de isolar comportamentos e testar pequenas partes é uma grande estratégia para garantir a qualidade.

O projeto utilizado nesse artigo esta [no GitHub](https://github.com/candiolli/five-stars-ecommerce/tree/master/five-stars-customer). Qualquer dúvida e feedback sobre o artigo, estou a disposição.

# Referências

[Mockito framework siteMockito is served to you by Szczepan Faber and friends. First engineers who were using Mockito in production were…site.mockito.org](https://site.mockito.org/)

[CWI Software](https://medium.com/cwi-software?source=post_sidebar--------------------------post_sidebar--------------)

Desenvolvemos soluções e sistemas de TI com base nas…