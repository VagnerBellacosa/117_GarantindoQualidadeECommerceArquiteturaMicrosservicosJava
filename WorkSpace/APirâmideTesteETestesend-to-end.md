[
![gtsw](https://miro.medium.com/max/480/1*JfJziuJZNG0lRFdzFmAJ_g.png)](https://medium.com/gtsw?source=post_page-----38f77ad3d137-----------------------------------)



# A Pirâmide de teste e os Testes end-to-end

[![Anne Caroline Rocha](https://miro.medium.com/fit/c/96/96/2*i7BK0dWhtbfGogcc5ZsPeA.png)](https://medium.com/@anne_caroline?source=post_page-----38f77ad3d137-----------------------------------) - [Anne Caroline Rocha](https://medium.com/@anne_caroline?source=post_page-----38f77ad3d137-----------------------------------)  -  [Jan 25](https://medium.com/gtsw/a-pirâmide-de-teste-e-os-testes-end-to-end-38f77ad3d137?source=post_page-----38f77ad3d137-----------------------------------) · 

![O que são testes End-to-end (E2E)? A pirâmide de teste mostra testes E2E vertical e horizontal.](https://miro.medium.com/max/1400/1*qPbVQboT4oNl7NlZUNXFXg.png)

Pirâmide de Teste e Testes E2E. [Fonte: Andrejs](https://stackoverflow.com/questions/19378183/difference-between-system-testing-and-end-to-end-testing)

Testes “end-to-end” (E2E testing) são uma maneira de realizar testes atravessando todas as camadas da arquitetura de um sistema. **Os testes são realizados do início ao fim**, por exemplo, em uma arquitetura de sistema MVC (Model-View-Controller) os testes são realizados na camada de apresentação (view), validadando regras de negócio tratadas pelo controlador (controller) chegando até o modelo (model), onde os dados podem ser gravados e lidos a partir de um banco de dados.

No entanto, **essa definição de E2E não parece muito diferente dos testes de sistema**, que são testes que tratam o sistema como uma caixa-preta, cujos dados são passados em uma tela do sistema e o usuário recebe uma resposta na mesma interface do sistema.

Se observarmos a pirâmide de teste acima, nós percebemos que os testes E2E podem ser classificados como horizontal e vertical.

- **E2E horizontal:** quando os testes são realizado em um mesmo nível de teste, considerando todos os fluxos do sistema. Tem como objetivo verificar se os componentes daquela camada, fazem o que deveriam fazer em um determinado contexto.
- **E2E vertical:** quando os testes são realizados em vários níveis de teste. Dessa forma é possível identificar problemas nas diferentes camadas do sistema, desde o nível unitário até a integração de todos os componentes. Nesse caso o objetivo é verificar se cada camada do sistema funciona independentemente.

Através da pirâmide de teste, podemos observar que há diferenças conceituais entre testes E2E e testes de sistema.

## **Testes Funcionais**

1. O teste é limitado a uma única parte do código ou sistema.
2. Garante que o software testado atende aos critérios de aceitação.
3. Testa a maneira como um único usuário se envolve com o sistema.
4. Valida o resultado de cada teste para entradas e saídas.

## Testes End-to-End (E2E)

1. O teste cruza vários sistemas e grupos de usuários.
2. Garante que um sistema, ou parte dele, continue funcionando após alterações serem feitas.
3. Testa a maneira como vários usuários interagem no sistema.
4. Valida se cada etapa do processo foi concluída.

## Pirâmide de Teste

Um ponto importante a se observar na Pirâmide de Teste é a sua forma, denotando a **proporção de testes que devem ser realizados em cada nível** de teste. Assim, os testes unitários devem ser realizados em maior quantidade, em seguida os testes de integração e por fim os testes de sistema.

Isso se deve ao fato que os testes que estão na base da pirâmide (testes unitários) possuem um custo de criação, execução e automação bem menor que os testes do topo da pirâmide. Além disso, em um cenário em que testes unitários e de integração são criados de forma efetiva, vários cenários de testes e regras de negócio podem ser validadas nesses níveis mais baixos. Com isso, é possível **reduzir o número de testes de sistema** (manuais e/ou automáticos) para os cenários de teste que já foram testados anteriormente em outros níveis.

Se quiser saber mais sobre pirâmide de teste, recomendo o artigo de Martin Fowler: https://martinfowler.com/bliki/TestPyramid.html

## Ferramentas para E2E vertical

**Testes de sistema (UI):**

- [Selenium](https://www.selenium.dev/): realiza testes automáticos através da interface web de uma aplicação, independente da linguagem de programação que ela foi construída. Possui diferentes linguagens de programação, como python, java, ruby, etc. Tem fácil instalação, pois permite realizar testes através de um plugin para o navegador, utilizando o Selenium IDE, sem a necessidade de conhecimentos de programação.
- [Cypress](https://www.cypress.io/): também realiza testes automáticos através da interface web de uma aplicação. Não depende da linguagem de programação utilizada no desenvolvimento. Os testes são construídos em JavaScript e requer a instalação do NodeJs, ou seja, conhecimentos de programação.

**Testes de integração para APIs Rest**

- [Cypress](https://www.cypress.io/): permite realizar testes em API Rest. Os testes são escritos em JavaScript. Além disso, os testes podem ser agregados ao código do sistema, mas eles são executados de forma independente, sem nenhum vínculo às classes do sistema desenvolvido.

**Testes unitários**

- [JUnit](https://junit.org/junit5/): testes unitários padrão para a linguagem Java.
- [Mocha](https://mochajs.org/): testes unitários bastante utilizado por programadores JavaScript.
- [Jest](https://jestjs.io/): testes unitários desenvolvidos pelo Facebook e é bastante utilizado por programadores React.

Há outras ferramentas que podem ser utilizadas para outras finalidades. Gostei bastante do material desse blog abaixo: https://talkingabouttesting.com/2018/10/05/um-review-pessoal-de-ferramentas-para-testes-automatizados-no-mundo-javascript-parte-1/

Basicamente, a regra básica para garantir uma maior qualidade nos sistemas é comece a testar o mais cedo, se possível antes mesmo de criar a primeira linha de código. Separe os testes em diferentes níveis, para que cada tipo de teste detecte os possíveis erros de acordo com os objetivos de cada um. Não perca tempo testando o que já foi testado nos níveis anteriores.

***Anne Caroline Rocha\*** *é autora do blog* [***Grupo de Testadores de Software\***](http://gtsw.blogspot.com/)*. Atua na área de Qualidade de Software desde 2007, gerenciando equipes e ministrando aulas. Em 2020, escreveu o ebook “*[***Investir ou não em teste de software?\***](https://bit.ly/319ys0P)*” e ainda este ano pretende lançar seu primeiro livro “*[***Simplificando Testes de Software\***](https://bit.ly/3hUPK8v)*”, que aborda o tema utilizando uma linguagem simples e didática, para ajudar quem está começando na área.*

*Ela acredita que compartilhar conhecimentos é a chave para um mundo melhor.*

[gtsw](https://medium.com/gtsw?source=post_sidebar--------------------------post_sidebar--------------) - Grupo de Testadores de Software



- [Pirâmide De Testes](https://medium.com/gtsw/tagged/pirâmide-de-testes)
- [Teste End To End](https://medium.com/gtsw/tagged/teste-end-to-end)
- [Testes De Sistema](https://medium.com/gtsw/tagged/testes-de-sistema)
- [Ferramentas De Teste](https://medium.com/gtsw/tagged/ferramentas-de-teste)
- [Teoria Em Testes](https://medium.com/gtsw/tagged/teoria-em-testes)

