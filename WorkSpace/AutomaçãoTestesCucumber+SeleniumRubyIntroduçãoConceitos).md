# Automação de Testes: Cucumber + Selenium em Ruby (Introdução e conceitos)

[![Rafael Berçam](https://miro.medium.com/fit/c/56/56/0*Hr3awBUoc6lYwuQ9.)](https://medium.com/@rafaelberam?source=post_page-----2bfa28793980-----------------------------------)

[Rafael Berçam](https://medium.com/@rafaelberam?source=post_page-----2bfa28793980-----------------------------------)

[Dec 19, 2017·11 min read](https://medium.com/@rafaelberam/automação-de-testes-cucumber-selenium-em-ruby-introdução-e-conceitos-2bfa28793980?source=post_page-----2bfa28793980-----------------------------------)



Muito se fala sobre testes automatizados e sua importância dentro do contexto empresarial, por diminuir os custos relacionados ao tempo de execução de tarefas demoradas como testes de regressão e tarefas repetitivas. Porém ainda há uma resistência em colocar em produção essas técnicas automação, sendo ou por falta de conhecimento ou mão de obra especializada.

Pensando nisso, o texto abaixo introduz os principais assuntos relacionados à automação de testes de uma maneira simplificada e de fácil aprendizado.

# Automação de Testes: Conceitos

Testes funcionais são testes realizados de acordo com a funcionalidade correspondente, ou seja, são testados os comportamentos da ferramenta dentre todos os cenários existentes de acordo com o resultado esperado a fim de contemplar todas as partes que podem apresentar falhas no presente momento e também futuramente.

Já a automação de testes, é o processo da escrita de um programa para executar esses testes funcionais!

A principal vantagem de se automatizar os testes esta relacionada a economia de tempo e recursos durante a execução dos testes além da possibilidade de executar os mesmos testes repetidas vezes.

Então, por que automatizar os testes? A importância da automatização dos testes esta diretamente relacionada a qualidade final do produto, pois a execução de todos os testes funcionais que existe no sistema antes da sua entrega garante uma menor incidência de erros e falhas no programa.

Então quer dizer que eu tenho que só fazer testes automatizados? Não, muita calma! Testes manuais não são substituídos pelos testes automatizados, os testes manuais são imprescindíveis no processo de desenvolvimento da aplicação durante o ciclo de desenvolvimento da funcionalidade. Hoje como a maior parte das empresas de tecnologias estão optando por processos cada vez mais ágeis e o primeiro contato do Analista de Teste com a aplicação, muito das vezes, ela ainda não esta finalizada e outros conceitos de teste são aplicados durante esse curto período de uma sprint como:

- Testes que envolvam tarefas mais intelectuais e que exijam análise e pensamento lógico;
- Testes de Usabilidade
- Tarefas dinâmicas
- Testes em sistemas de curto ciclo de vida

Já os testes automatizados são aplicadas em outro contexto:

- Quando envolver tarefas repetitivas;
- Aplicações com longos ciclos de vida
- Testes que devem ser feitos com maior frequência

Afinal, qual é o melhor? Não podemos simplesmente escolher uma dessas abordagens, pois tanto o teste manual quanto o automatizado são extensões da tarefa da área de testes. Todos os dois possuem pontos fortes e fracos e acaba que um completa o outro nas atividades do Teste de Software!

# Selenium e suas ferramentas

O Selenium é um conjunto de diferentes ferramentas de software cada uma com uma abordagem diferente para o suporte à automação de testes, dentre elas, nesse post em específico, vamos abordar o Selenium WebDriver e uma IDE muito fácil e simples de usar que se chama Katalon.

# Katalon

O Katalon é uma ferramenta de prototipagem para a criação de scripts de teste. É um plugin do Chrome e Firefox e fornece uma interface fácil de usar para o desenvolvimento de testes automatizados. Ele se baseia na gravação das iterações com o navegador guardando os elementos da página em um identificador, também chamado de “Target” e grava qual é o comando realizado para esse identificador, como eventos de ‘click’, preenchimento de campos, seleção de campos dentre outros.

![img](https://miro.medium.com/max/60/1*u28KxtvpXWHk1ez6Eng34Q.png?q=20)

![img]()

Tela do Katalon IDE para o Chrome

Nessa IDE podemos então interagir com a aplicação quando acionamos o comando [Record] e ao final clicamos no botão [Stop] para ele parar de gravar as ações.

![img](https://miro.medium.com/max/60/1*HIbcRKHSKbvtX8zFl1-SAg.png?q=20)

![img]()

Katalon gravando uma interação com o Navegador

Essa ferramente irá nos auxiliar na elaboração dos testes automatizados pois ela consegue exportar esses diálogos com o navegador para as frameworks mais populares, dentre elas o Ruby (WebDriver + Rspec)

![img](https://miro.medium.com/max/60/1*h1AHOaH5jnKxObIGW0LyBA.png?q=20)

![img]()

Tela de Exportação do Código Ruby

Como o objetivo desse conteúdo não é o foco no Katalon (que em breve farei um conteúdo a parte) vou deixar um link que mostra todas as suas funcionalidades!

[Documentação Katalon](https://forum.katalon.com/discussion/4056/katalon-automation-recorder-powerful-selenium-ide-to-record-debug-play-tests-in-any-browsers)

# Ruby

![img](https://miro.medium.com/max/792/1*a2lJmavdnzQEvKsUbdGURg.png)

Sim! O Ruby! Como nos exemplos que serão mostrados para a execução dos testes automatizados foi utilizado o Ruby, quero convidar a todos a aprender um pouco (praticamente o básico) sobre essa linguagem formidável! Conseguimos escrever de maneira muito simples os códigos em Ruby para automação de testes.

Te convido a realizar a leitura desses tópicos para podemos alinhar os conhecimentos e se familiarizar com os códigos que vamos escrever!

[Ruby em Vinte Minutos](https://www.ruby-lang.org/pt/documentation/quickstart/)
[Ruby a Partir de Outras Linguagens](https://www.ruby-lang.org/pt/documentation/ruby-from-other-languages/)

E com o decorrer do tempo todos os documentos sobre o Ruby estão aqui no link abaixo.

[Documentação Ruby](https://www.ruby-lang.org/pt/documentation/)

# Selenium WebDriver

Começaremos aqui a conhecer o território de onde vamos iniciar a automação de testes. O Selenium WebDriver é a principal ferramenta de automação de testes dentro do pacote do Selenium, isso se dá pelo poder de interagir com o navegador através de comandos específicos e fazer o reuso dentro da escrita do nosso programa de automação.

Para podermos usar dentro do Ruby, vamos fazer a instalação da Gem do selenium WebDriver.

Como assim Gem?
Uma “RubyGem” ou simplesmente “Gem” é uma biblioteca, um conjunto de arquivos Ruby reusáveis, etiquetada com um nome e uma versão (via um arquivo chamado de “gemspec”).

**Instalando a Gem no Ruby**

Através do Prompt de comando (CMD) basta digitar o comando ‘gem install selenium-webdriver’ e teclar [Enter] que a gem do Selenium será instalada.

![img](https://miro.medium.com/max/1134/1*LHDYkssJ6_VPFsoC73j2Hw.png)

Recomendo baixar o Cmder, que é um programa similar ao CMD do Windows porém a facilidade de copiar os códigos e colar são mais simples. Então segue o link

[Cmder Download](http://cmder.net/)

Estou utilizando também o Sublime Text 2 para escrever os códigos em Ruby

[Sublime Download](https://www.sublimetext.com/2)

Feito isso o nosso Ruby já entende o contexto do Selenium Webdriver! Mas antes de rodar qualquer programa precisamos selecionar qual será o driver que vamos executar.
Eu estou usando o ChromeDriver que esta disponível nesse endereço:

[ChromeDriver Download](https://sites.google.com/a/chromium.org/chromedriver/downloads)

Após baixar, salve o arquivo e descompacte o seu conteúdo em uma pasta de sua preferência, mas lembre-se do caminho dessa pasta para poder referenciar no código Ruby o endereço do driver.

Vamos agora escrever um pequeno teste.

![img](https://miro.medium.com/max/60/1*Te8l5ypmckU7cTa93kk4DA.png?q=20)

![img]()

Teste do Selenium WebDriver em Ruby

Neste pequeno programa o Selenium Webdriver é iniciado abrindo a página do Google e aguardando por 10 segundos antes de fechar. Escreva o conteúdo desse programa em um arquivo e salve com a extensão .rb (Ex: **teste_driver.rb**)

Para executar o programa, vá até o Cmder e abra a pasta contida o programa e digite ‘**ruby teste_driver.rb**’

![img](https://miro.medium.com/max/60/1*ZEUsGS2IXVsiuwVv0iYNyw.png?q=20)

![img]()

Executando o programa driver_teste.rb no Cmder

Após executar, o Chromedriver aciona o Google Chrome passando o endereço do comando ‘get’ do selenium e direcionando para a página.

![img](https://miro.medium.com/max/60/1*ypg1eB41OWY8noLmeQHwAw.png?q=20)

![img]()

Chrome sendo executado pelo Selenium Webdriver

Quando o Chrome é executado aparece uma mensagem em seu cabeçalho informando que ele esta sendo controlado por um software de teste automatizado, e após 10 segundos o Webdriver é encerrado.

Pronto! Temos o mais básico para executar o Selenium Webdriver e poder dialogar com o navegador, fazendo com que ele execute os comandos necessários para navegar por um sistema, coletando dados e executando as tarefas.

Neste mesmo exemplo, vaamos incrementar nosso programa para ele realizar uma pesquisa no Google por Testes Automatizados com Selenium Webdriver.

![img](https://miro.medium.com/max/60/1*yl12DJL1s8va9nQrkoWm9A.png?q=20)

![img]()

Programa agora pesquisando no Google

Agora o nosso programa realiza a busca do campo na página pelo seu ‘id’ e envia os dados para realizar a pesquisa.

vamos entender como funciona esse comando

![img](https://miro.medium.com/max/60/1*wzoRLyva0X_-rFZcPp4SWg.png?q=20)

![img]()

A variável ‘**@driver**’ inicialmente ao receber nosso WebDriver passa a ter acesso aos comandos para interagir com o navegador.

O comando ‘**find_element(:id, “lst-ib”)**’ procura na página do Google o ‘WebElement’ correspondente.

![img](https://miro.medium.com/max/60/1*U4mz4y8JqG31Rwr72mKiqA.png?q=20)

![img]()

Elemento id=”lst-ib” sendo exibido

Tendo o ‘WebElement’ do campo em mãos, eu consigo realizar comandos como enviar uma string para preencher o campo de busca usando o ‘**send_keys(“Testes Automatizados com Selenium WebDriver”)**’.

Assim ao final consiguimos usar o mesmo elemento fazendo o comando ‘**submit**’ para acionar o [Enter] e efetuar a pesquisa.

![img](https://miro.medium.com/max/60/1*ckR3gDICNciZE1GquU9aZw.png?q=20)

![img]()

Comando .submit para efetuar a pesquisa

Vamos agora executar o programa e ver o que acontece

![img](https://miro.medium.com/max/60/1*YY7mqQ5W20oerNsvHFiiiw.png?q=20)

![img]()

Campo sendo preenchido pelo comando ‘send_keys’

![img](https://miro.medium.com/max/60/1*mtPyaLakCtMd_VnzolYtHw.png?q=20)

![img]()

Resultado da pesquisa após executar o comando ‘submit’

Muito bem! Nosso programa entende os comandos e consegue interagir com o navegador. Existe uma lista de comandos muito extensa para o Selenium Webdriver e abaixo estão os comandos mais utilizados:

![img](https://miro.medium.com/max/60/1*fnw6rk0xtfLsXohGWw8TNw.png?q=20)

![img]()

Comandos que interagem diretamente com o Driver do Chrome

![img](https://miro.medium.com/max/60/1*W72Z2Fvu4TCQq8UqkZ1XbA.png?q=20)

![img]()

Comandos que interagem diretamente com os WebElements

Recomendo a leitura sobre as principais ligações em Ruby

[Ruby Bindings](https://github.com/SeleniumHQ/selenium/wiki/Ruby-Bindings)

# Cucumber

O Cucumber também é uma ferramenta para automação de testes, ele executa Testes de Aceitação Automatizado escrito em um estilo de Desenvolvimento Orientado a Comportamento (BDD). O Cucumber possui um analisador de linguagem simples chamado Gherkin.

Ele permite que os comportamentos esperados seja especificado em um idioma lógico que os clientes possam entender, e ele já foi utilizado de forma exclusiva para o teste do Ruby como complemento à estrutura BDD Rspec.

Para que possamos utilizar o Cucumber em nossos testes, precisamos instalar a Gem para que o programa em Ruby possa entender o contexto e ter seus comandos reconhecidos. Para isso basta digitar o comando '**gem install cucumber**’ no Cmder e pressionar [Enter].

![img](https://miro.medium.com/max/1268/1*bqm73RdrR_harZzMN-4zXQ.png)

Instalação da Gem do Cucumber

Após a instalação podemos criar um repositório do nosso primeiro projeto do Cucumber, para isso, no Cmder vá até o repositório desejado e digite o comando ‘cucumber — init’

![img](https://miro.medium.com/max/60/1*i2YrlkOo2Y3fwHCTI0lRKw.png?q=20)

![img]()

Criando repositório com comando ‘cucumber — init’

A Estrutura de pastas são:
—| features|
— — |step_definitions|
— — |support |
— — —| env.rb

Essa estrutura é criada a partir da biblioteca do Cucumber no Ruby, mas por convenção, é criado uma terceira pasta com o nome [specifications] para salvar os arquivos escritos em Gherkin com as extensões [.feature]

Dessa forma passa a ter a seguinte estrutura:

— | features|
— — |step_definitions|
— — |support |
— — — | env.rb
— — |specifications|

Agora podemos criar nossa primeira especificação no Cucumber! Essa especificação é escrita em uma linguagem natural que segue a estrutura de programação BDD. O nome dessa linguagem é Gherkin e segue a seguinte estrutura:

![img](https://miro.medium.com/max/60/1*bVk3JRl4Vc4EeMT59AOiPg.png?q=20)

![img]()

Exemplo de escrita da feature em Gherkin

O conjunto de palavas escritas nesse documento existem palavras reservadas que o Cucumber interpreta para execução dos testes:

- [**Funcionalidade**:] indica a funcionalidade a ser testada (Ex: Teste de inclusão de um novo cliente)
- [**Cenário**:] indica o que o cenário irá validar
- [**Dado**] indica uma pré condição para que o seu teste aconteça, caso exista mais de uma a próxima linha deve conter a palavra [**E**]
- [**Quando**] indica a ação do cenário, execução do teste. Quando apresentar mais de uma ação deve conter na próxima linha iniciando com a palavra [**E**]
- [**Então**] indica o resultado que se espera da execução e quando apresentar mais de uma deve usar também a condição [**E**] na próxima linha.

Vamos escrever uma Funcionalidade que vai ter o objetivo de criar uma conta no Facebook. Ficaria dessa forma:

![img](https://miro.medium.com/max/60/1*vJitmABqMdopS2Qw_K_XYQ.png?q=20)

![img]()

feature da Funcionalidade de Criar conta no Facebook

Agora o que precisamos fazer é salvar nossa funcionalidade na pasta [specifications] da estrutura do projeto como ‘**cria_conta.feature**’

![img](https://miro.medium.com/max/60/1*fA8XpxKMe6zGr6lOaJREmA.png?q=20)

![img]()

Pasta specifications como arquivo .feature

Agora pelo Cmder vamos até a pasta [specifications] e vamos rodar o comando ‘**cucumber cria_conta.feature**’

![img](https://miro.medium.com/max/60/1*8HIG25Sm_wSQWXIBv-EHnA.png?q=20)

![img]()

rodando o comando ‘cucumber cria_conta.feature’

Veja que o cucumber entende o conteúdo escrito, ele identificou que existe 1 cenário e 4 passos porém ainda não foram definidos. Abaixo ele mostra uma mensagem dizendo que ‘Você não implementou a definição dos passos’ e mostra quais são os passos pendentes de implementação.

Eu vou copiar diretamente do Cmder o conteúdo abaixo da mensagem “*You can implement step definitions for undefined steps with these snippets:*” e vou criar um novo arquivo na pasta [step_definitions] com mesmo nome do nosso arquivo feature mas com a extensão .rb [**cria_conta.rb**]

![img](https://miro.medium.com/max/60/1*P6MyTOi6u2hefstsGVjwLw.png?q=20)

![img]()

Pasta [step_definitions] com o arquivo cria_conta.rb

Veja que ao salvar o sublime já identifica o código ruby. Agora vamos falar sobre o arquivo que esta na pasta [support] com o nome **env.rb**

Este arquivo irá conter todas as bibliotecas que vamos utilizar para rodar nosso projeto. Nesse caso em específico precisamos declarar apenas as Gems ‘selenium-webdriver’ e ‘cucumber’

![img](https://miro.medium.com/max/60/1*0PKai3xwfvvt5satPbfYfw.png?q=20)

![img]()

Pasta [support] com o arquivo env.rb

Após escrever as bibliotecas que pretendemos utilizar vamos realizar um teste rodando o comando ‘cucumber’ na pasta raiz do projeto, nesse exemplo em específico a pasta é a [Projeto Cucumber]

![img](https://miro.medium.com/max/60/1*aKJFGdBpPKV8mszNLgaNTQ.png?q=20)

![img]()

comando ‘cucumber’ na pasta do projeto

Perceba agora que o cenário passou para pendente e o primeiro passo ficou pendente por não estar descrito os comandos e com isso os próximos 3 passos foram “pulados’.

Vamos agora juntar o Selenium WebDriver no conteúdo do arquivo .rb do nosso teste automatizado.

![img](https://miro.medium.com/max/60/1*ZLCTszw2AMAaZv9wulEsHA.png?q=20)

![img]()

Veja na imagem acima que foram criados os primeiros passos do nosso teste automatizado, onde pedimos para que o WebDriver vá para o endereço do Facebook. Vamos rodar agora o nosso comando ‘**cucumber**’ e ver o que acontece:

![img](https://miro.medium.com/max/60/1*WV-eR4_CMUBcYAC9LRsK4A.png?q=20)

![img]()

WebDrive abrindo a página do Facebook

Veja que o WebDriver foi acionado e a página do Facebook é apresentada mas um detalhe aconteceu na execução do teste olhando o log da execução no Cmder

![img](https://miro.medium.com/max/60/1*qFfpiK1AuIHYmIHQMkxGUg.png?q=20)

![img]()

Log execução do Cucumber no Cmder

Veja que agora um passo ficou com o status ‘Passou” e agora temos um passo pendente e outros 2 foram ‘pulados’ pelo fato do segundo passo ainda não ter sido executado. Então agora já temos um passo funcional onde o passo fala “Dado o site do Facebook” o nosso programa já exibe o mesmo executando o drive. Agora precisamos preencher os outros passos.

![img](https://miro.medium.com/max/60/1*w0Vywq-6mHEttcLJGPqDyg.png?q=20)

![img]()

Preenchendo os passos no arquivo ruby com comandos WebDriver

Após preencher todos os passos vamos executar o comando ‘cucumber’

![img](https://miro.medium.com/max/60/1*_ThtcfeyL-ZokcTykAi5Ew.png?q=20)

![img]()

WebDriver sendo executado a partir do comando ‘cucumber’

Veja na imagem acima que o WebDriver fez o preenchimento dos campos da abertura de conta e clicou em [Abrir uma conta]

![img](https://miro.medium.com/max/60/1*iNwYhvttQ9mhIGBy7LSfSg.png?q=20)

![img]()

Cenário e passos executados com sucesso

Por fim nosso cenário e passos foram executados com sucesso! Dessa forma a partir da escrita da documentação em Gherkin e integrando com meu programa escrito em Ruby fizemos com que o Cucumber executasse os testes e nos mostrasse os resultados.

[Link Pasta Projeto Cucumber](https://drive.google.com/file/d/14d6xnOIrSCntw9cyZKFcbQv5BgGwUJ0Z/view?usp=sharing)

Concluindo, nesse post vimos como é possível preparar o ambiente para usar o Cucumber interagindo com o Selenium WebDriver através do Ruby.

Esse post também foi escrita de uma maneira simples sobre o funcionamento, mas não é totalmente aplicado nos testes automatizados pois temos que ver um ponto muito importante que é o RSpec do Ruby que é um framework de testes unitários onde irá facilitar realizar tarefas como pequenos ‘assertions’ e estruturar melhor os cenários de teste.

Em breve postarei sobre RSpec + Selenium WebDriver assim vamos completar nosso conhecimento!

# Referências

## Ruby

- https://www.ruby-lang.org/pt/documentation/
- https://www.caelum.com.br/apostila-ruby-on-rails/ruby-basico/#3-8-exercicios-strings

## Selenium

- http://docs.seleniumhq.org/docs/
- https://forum.katalon.com/discussion/4056/katalon-automation-recorder-powerful-selenium-ide-to-record-debug-play-tests-in-any-browsers

## Cucumber

- https://cucumber.io/docs
- https://github.com/thiagomarquessp/capybaraforall
- https://github.com/thiagomarquessp/capybara_for_all_p2
- https://github.com/thiagomarquessp/capybara_for_all_p3

## Conceitos

- http://bstqb.org.br/?q=download

# Minhas Redes Sociais

- [LinkedIn](https://www.linkedin.com/in/rafael-berçam-918a4718/)
- [Facebook](https://www.facebook.com/rafael.bercam)
- faelbercam@gmail.com

[Rafael Berçam](https://medium.com/@rafaelberam?source=post_sidebar--------------------------post_sidebar--------------)

Analista de Testes / QA

- [Cucumber](https://medium.com/tag/cucumber)
- [Selenium Webdriver](https://medium.com/tag/selenium-webdriver)
- [Automação De Testes](https://medium.com/tag/automação-de-testes)
- [Teste](https://medium.com/tag/teste)
- [Testers](https://medium.com/tag/testers)

## [More from Rafael Berçam](https://medium.com/@rafaelberam?source=follow_footer-----2bfa28793980-----------------------------------)

Follow



Analista de Testes / QA

