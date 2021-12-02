# 4 Melhores Frameworks de Testes E2E (End to End)

[ALOISIO ALMEIDA](https://devporai.com.br/author/aloisio-almeida/) MAIO 17, 2021 [LEAVE A COMMENT](https://devporai.com.br/4-melhores-frameworks-de-testes-e2e-end-to-end/#respond)

![4 Melhores Frameworks de Testes E2E](https://devporai.com.br/wp-content/uploads/2021/05/Automation-Testing-Frameworks-and-Tools-740x414.png)

Com tantas ferramentas e frameworks disponíveis para testes automatizados fica realmente difícil escolher com qual começar, então para ajudar você que ta começando hoje eu vou apresentar os 4 Melhores Frameworks de Testes E2E na minha opinião.

Mas antes de falarmos dos frameworks primeiro precisamos relembrar o que são testes E2E.

## O que são testes E2E?

Testes E2E ou em bom português, testes de ponta a ponta.

São testes que buscam fazer uma simulação mais próxima do comportamento do usuário da aplicação.

Para que os frameworks de testes consigam simular o comportamento do usuário eles usam uma serie de recurso baseados em seletores.

Esses seletores podem tanto HTML quanto CSS.

A partir desses seletores, ou `xpath` o framework vai conseguir identificar o componente em tela e então realizar uma ação ou fazer uma comparação de testes.

Geralmente esses testes não costumam cobrir todos os fluxos do sistema.

Então fique atento, não é porque são testes de ponta a ponta que eles vão cobrir todo o sistema.

Isso ocorre pois construir e executar esses testes é relativamente demorado.

Então as equipes acabam cobrindo somente os fluxos principais do usuário.

Caso queira saber mais sobre como são avaliados os custos de um teste e quais são os tipos de testes mais comuns então confira nosso post sobre a pirâmide de testes [aqui](https://devporai.com.br/piramide-de-testes/).

Mas sem mais delongas vamos a lista dos Melhores Frameworks de Testes E2E.

## 4 Melhores Frameworks de Testes E2E – Lista

### Selenium

![Selenium - 4 Melhores Frameworks de Testes E2E](https://devporai.com.br/wp-content/uploads/2021/05/68747470733a2f2f73656c656e69756d2e6465762f696d616765732f73656c656e69756d5f6c6f676f5f7371756172655f677265656e2e706e67-980x1024.png)Selenium – 4 Melhores Frameworks de Testes E2E

O Selenium foi criado originalmente como ferramenta interna da ThoughtWorks.

Mas se popularizou realmente após a junção do projeto Selenium com o projeto WebDriver.

Criando assim o framework que conhecemos hoje, o Selenium WebDriver ou Selenium 2.0.

Hoje o Selenium é de longe o framework mais comum para construção de testes E2E.

O framework tem uma série de ferramentas para a execução dos testes.

Além disso o framework permite que os testes sejam escritos em várias linguagens como C# e Java por exemplo.

Como o core do Selenium é o WebDriver então ele é ideal para a criação de testes para diversos navegadores, uma vez que a interface do WebDriver deve seguir [a especificação da W3C](https://www.w3.org/TR/webdriver/).

### Cypress

![Cypress - Selenium - 4 Melhores Frameworks de Testes E2E](https://devporai.com.br/wp-content/uploads/2021/05/cypress-io-logo-social-share-8fb8a1db3cdc0b289fad927694ecb415-1024x536.png)Cypress – Selenium – 4 Melhores Frameworks de Testes E2E

Por mais que o Selenium seja o framework mais usado e que venha sendo evoluído ele ainda apresenta alguns problemas.

Sendo os principais acerca da performance dos testes.

É bem comum encontrar rotinas de testes demoram várias horas e que demandam de máquinas potentes para a sua execução.

E a proposta do Cypress é justamente melhorar esse e outros problemas do Selenium.

Feito em Node.js o Cypress busca melhorar a vida de Analistas de testes e desenvolvedores.

Para isso ele trás uma série de recursos internos, entre os principais estão:

Espera automática, estrutura própria para debug e recursos avançados de logs.

Realmente é bem simples debugar e ver os logs dos testes.

E não posso deixar de destacar a espera automática, pois uma das coisas mais chatas em construir testes E2E é colocar diversos `wait `no código.

### Puppeteer

![Puppeteer - Cypress - Selenium - 4 Melhores Frameworks de Testes E2E](https://devporai.com.br/wp-content/uploads/2021/05/logo.png)Puppeteer – Cypress – Selenium – 4 Melhores Frameworks de Testes E2E

O puppeteer diferente dos frameworks citados não tem o foco em testes.

Mas ele oferece uma API completa para o controle headless do Chrome e do Chromium.

A biblioteca foi feita em node e tem muitas ferramentas que os outros frameworks não tem.

Entre as principais estão: testar extensões do Chrome e a possibilidade de adicionar dezenas de bibliotecas adicionais, como a biblioteca de stealth por exemplo.

Se você quiser saber mais sobre o puppeteer eu recomendo que você dê uma lida no [github do projeto](https://github.com/puppeteer/puppeteer).

### TestCafe

![TestCafe - Puppeteer - Cypress - Selenium - 4 Melhores Frameworks de Testes E2E](https://devporai.com.br/wp-content/uploads/2021/05/Test-Cafe-Studio.png)TestCafe – Puppeteer – Cypress – Selenium – 4 Melhores Frameworks de Testes E2E

Uma opção boa para quem não quer ter que trabalhar com WebDriver o TestCafe também oferece um conjunto completo de automação para a criação de testes E2E.

Além disso o TestCafe tem também uma IDE chamada TestCafe Studio.

A IDE facilita e muito a criação dos testes usando o TestCafe.

## 4 Melhores Frameworks de Testes E2E – Conclusão

Eu apresentei os 4 frameworks que eu considero os melhores, mas tenho certeza que existem diversos outros.

Mas uma coisa que todos tem e comum e você precisa saber bem é usar os seletores, tanto os de CSS tanto os de xpath.

E para te ajudar a entender mais sobre seletores eu recomendo que veja o post sobre aprender CSS com jogos, pois nele apresentamos alguns jogos focados só em seletores.

