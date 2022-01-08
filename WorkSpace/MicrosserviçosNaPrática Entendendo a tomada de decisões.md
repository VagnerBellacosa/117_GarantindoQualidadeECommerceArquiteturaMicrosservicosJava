# Microsserviços na prática: Entendendo a tomada de decisões

## Boas-vindas à realidade - Apresentação

<video class="elasticMedia" frameborder="0" controls="" controlslist="nodownload" style="box-sizing: inherit; margin: 0px; padding: 0px; position: absolute; top: 0px; left: 0px; width: 820px; height: 461.25px; border: 0px;"></video>

Olá, pessoal! Sejam muito bem-vindos a Alura! Sou o Vinicius Dias e vou guiar vocês durante esse treinamento, onde vamos falar bastante sobre Microsserviços. Já temos alguns treinamentos sobre microsserviços onde falamos de forma bem extensa sobre vários conceitos teóricos. Só que nesse vídeo vamos continuar focando na teoria, mas mostrando alguns desses conceitos na prática.

Já quero te adiantar que a aplicação que vamos ver não é completa. É uma super simplificação de uma aplicação real. Então o que vamos fazer é pegar alguns exemplos reais e analisar a tomada de decisão para criarmos algum aplicativo utilizando a arquitetura de microsserviços. Nós vamos ver na prática como esses microsserviços estão se comunicando e tarefas de plano de fundo.

Vamos falar sobre a infraestrutura de cada serviço. Vamos falar sobre o processo de *build*. Vamos ver sobre GitHub Actions. Então, vai ter bastante prática! Mas lembrando de dois detalhes: a aplicação não está completa e não vamos focar na parte prática. Não vamos desenvolver aqui. Vamos focar na teoria vendo a parte prática.

Para isso, vamos utilizar um sistema bem simples simulando a Alura. Temos uma parte onde mandamos uma requisição para um microsserviço de marketing. Depois mandamos para um microsserviço de pagamento. Um processamento é feito de forma demorada.

Depois o microsserviço acadêmico é notificado, ele envia o e-mail e, a partir disso, o microsserviço acadêmico já com os dados dele, consegue permitir o *login* onde você consegue ver uma lista de cursos e marcar esses cursos como assistidos.

Tudo isso com muita comunicação assíncrona, tarefas de planos de fundo. Enfim, bastante coisas específicas de microsserviços. Espero que durante esse treinamento você tire bastante proveito. Como falei, já que a aplicação não está completa, vou deixar bastantes desafios para vocês. A cada capítulo desse treinamento alguns desafios vão ficar.

Não precisa se preocupar em anotar tudo porque no final eu deixo vários desses desafios. Recapitulo alguns e deixo outros desafios. Por que isso? Na prática a teoria é outra. É muito importante vermos e entendermos a teoria e mais importante ainda é vermos essa teoria aplicada - como vamos ver hoje.

Mas também é importante que você pratique sem supervisão, que você pratique por conta própria, que você pratique de forma que você se permita errar, que você se permita implementar de formas diferentes e que você converse com outras pessoas que também estejam aprendendo. Para isso, você pode utilizar o fórum da Alura.

Então se você ficar com alguma dúvida e tiver alguma questão sobre os desafios, se quiser compartilhar alguma decisão sua, não hesite. O nosso fórum está repleto de pessoas! Eu tento interagir sempre que possível, mas quando não consigo nós temos várias pessoas, como já disse - sejam alunos, moderadores ou instrutores. Com certeza a interação lá vai ser muito rica para você, assim como sempre foi para mim como aluno também.

Mas chega de falação! Vamos partir direito para o próximo vídeo, onde vamos entender esse projeto, ver ele na prática e começar a dar uma olhada em como funciona realmente uma aplicação utilizando a arquitetura de microsserviços.

## Boas-vindas à realidade - Conhecendo o projeto

<video class="elasticMedia" frameborder="0" controls="" controlslist="nodownload" style="box-sizing: inherit; margin: 0px; padding: 0px; position: absolute; top: 0px; left: 0px; width: 820px; height: 461.25px; border: 0px;"></video>

Pessoal, bem-vindos de volta! Então vamos dar uma olhada bem rápida em como a nossa aplicação funciona. Vamos ver na prática como ela funciona, como interagimos com ela e depois vamos conhecer um pouco de como ela foi implementada.

Então vou realizar o passo a passo, vou realizar todo o fluxo da aplicação. Depois, conforme o treinamento vai passando eu vou explicando como cada parte é implementada. Então, vamos nessa! A primeira coisa que vamos fazer é preencher os dados pessoais para nos matricularmos. Aqui já te adianto, essa primeira parte da tela vai enviar os dados para um microsserviço. Então, vamos lá!

O nome completo vai ser "Vinicius Dias" e esse vai ser o e-mail. Beleza, vou para o próximo. Já enviamos os dados para um microsserviço, só que agora precisamos mandar para um microsserviço de pagamentos. Então vamos preencher todos os dados que o microsserviços de pagamento precisa.

Vou colocar um CPF qualquer. O titular do cartão vai ser eu mesmo, então deixe-me digitar certo. Beleza, é um cartão fictício. Acho que digitei número de mais. Já temos validações. Deu para você ver. Tem o código de segurança. Beleza!

Quando fizer isso, o que vai acontecer? Esses dados vão ser enviados para o microsserviço de pagamento. Mas repare que ele já nos exibe que o pedido foi efetuado e que o pagamento está sendo processado.

Então uma tarefa de plano de fundo está rodando. Isso vai levar cerca de 3 segundos. É uma tarefa fictícia, então já programei um tempo. Depois desse tempo vai chegar um e-mail na caixa de entrada. Já, já eu vou te mostrar o e-mail.

Agora que provavelmente já passaram esses 30 segundos e sei que posso ir na minha página de *login* usar aquele e-mail e a senha que eu sei que o microsserviço criou. A partir disso, se tudo der certo, já posso fazer o *login*.

E está lá! Tenho acesso ao microsserviço acadêmico. Ele permite que eu entre ou não e me mostra os cursos disponíveis. A partir desses cursos eu posso marcar algum desses como assistido. Então nós já temos uma aplicação desenvolvida com três microsserviços e vamos entender quais são os componentes que fazem parte de cada um desses microsserviços.

Como disse na introdução, essa aplicação não está completa em nenhum sentido. Então nesse treinamento você vai ter vários desafios, mas aqui você já vê que é uma aplicação, de certa forma, funcional. Ela roda, pelo menos de alguma forma.

Mas beleza, agora que passamos o olho e entendemos como o projeto funciona, vamos entender em um desenho quais são os microsserviços e os componentes de cada microsserviço disponíveis nesse projeto. Te vejo no próximo vídeo!

## Boas-vindas à realidade - Conhecendo cada componente

<video class="elasticMedia" frameborder="0" controls="" controlslist="nodownload" style="box-sizing: inherit; margin: 0px; padding: 0px; position: absolute; top: 0px; left: 0px; width: 820px; height: 461.25px; border: 0px;"></video>

E aí pessoal, bem-vindos de volta! Vamos entender quais são os microsserviços que compõem a nossa aplicação e, dentro de cada microsserviço, quais são os seus componentes. Primeiro, nós temos um *front-end* que foi feito com Angular. Obviamente poderia ter sido feito com qualquer outra tecnologia, mas eu fiz com Angular.

E aqui o Angular se comunica diretamente apenas com o API Gateway. Poderíamos ter feito *backend for frontend* para organizarmos as coisas e garantirmos alguns acessos. Mas enfim, eu utilizei somente o API Gateway para simplificar. Esse API Gateway se comunica com três APIs, ele tem a configuração para redirecionar os *requests* para três APIs.

Uma de marketing, que é a primeira API que consumimos. Então aquela primeira tela de dados pessoais se chama API de Marketing. Lá nós criamos os detalhes com nome e e-mail para criarmos um *lead* no marketing. Para que isso serve?

Imagine que o aluno não completa a matrícula dele, vamos ter o nome e e-mail dele para no futuro mandarmos campanhas, promoções, perguntarmos o motivo por ele não ter terminado a matrícula etc. Então já armazenamos um dado importante desse aluno.

Repare que ambos, API e o consumidor de filas (que vamos falar posteriormente), estão no mesmo projeto. Esse projeto foi feito com Node TypeScript e o servidor web é o Express. Já temos uma tecnologia utilizando o microsserviço de marketing.

Depois preenchemos as informações financeiras e isso chega no nosso microsserviço de financeiro. Repare que aqui também ambos a tarefa de *background* (de plano de fundo) e a API estão no mesmo projeto. Isso porque utilizamos a mesma tecnologia e temos um microsserviço feito em PHP e o servidor é Swoole. O Swoole dá algumas facilidades para termos tarefas de plano de fundo. Por isso essa tecnologia foi utilizada.

Repare que o banco de dados de marketing é um MongoDB, já o banco de dados do financeiro é um banco relacional. Aqui estou utilizando SQLite só pela simplicidade mesmo, mas poderia ser qualquer outro - Oracle, MySQL, PostgreSQL, SQLServer. Enfim, só estou utilizando SQLite para manter esses dados em memória rapidamente e sem complicar mais.

Então, o que acontece? Quando recebemos esses dados na API financeira, ele faz o processamento, recebe os dados e manda para uma tarefa de plano de fundo. Essa tarefa de plano de fundo, no microsserviço financeiro, vai realizar o processamento do pagamento. Aqui poderíamos verificar se os dados do cartão são realmente daquele titular, verificar detalhes de fraude, enviar o pedido para o Gateway de pagamentos e para algum serviço externo etc.

Depois que isso é feito, o microsserviço de financeiro manda uma mensagem através da mensageria, através do RabbitMQ. O que esse RabbitMQ é? É basicamente um meio de campo. É um *software* que fica no meio de várias aplicações recebendo mensagens e essas mensagens são consumidas por outras pessoas. Basicamente, ele é um carteiro.

Então o nosso financeiro manda uma mensagem para ele. Vamos ter o microsserviço acadêmico ouvindo essa mensagem e esperando essa carta do microsserviço financeiro. Quando essa carta chega, o nosso microsserviço acadêmico faz o quê? Ele pega o e-mail e o nome desse cliente que o financeiro criou e cria um aluno no banco de dados Postgre. Ele vai criar um aluno e gerar uma senha para ele.

E a partir dessa senha gerada ele manda um e-mail para o aluno falando: "a sua matrícula está pronta. É só acessar essa URL que você está pronto para utilizar nosso serviço". Ao mesmo tempo em que isso acontece, o nosso marketing também recebe essa carta. O que o marketing faz? Ele muda o *status* daquele *lead* de alguém que está interessado em comprar nossos cursos, para alguém que já virou um de nossos alunos.

Dessa forma, essa rotina que é feita no plano de fundo gera uma mensagem que é consumida por dois serviços diferentes. Vamos ver na prática posteriormente como isso é implementado, mas basicamente é assim que isso acontece.

Ainda nessa API do microsserviço acadêmico, o que nós temos? O consumidor de filas criou o nosso aluno no banco de dados e a nossa API tem os detalhes de autenticação desse aluno e também tem os detalhes dos cursos que estão disponíveis para ele fazer. Então se marcarmos um curso como assistido, é no banco de dados acadêmico que essa alteração vai ser refletida.

Claro que deveríamos mandar essa informação para a mensageria para algum futuro microsserviço de gamificação talvez ler e dar pontos para esse aluno, para o nosso serviço de marketing saber quantos cursos esse aluno já fez e para um outro microsserviço de métricas, talvez de *business intelligence*.

Então, dessa forma funciona a comunicação das nossas APIs, dos nossos microsserviços. Repare que em nenhum momento eu utilizei comunicação direta entre alguma das APIs ou dos microsserviços. Toda a comunicação no nosso processo está sendo feita de forma assíncrona. A única comunicação síncrona é entre o nosso *front-end* e os nossos microsserviços, ou seja, o *frontend* espera o retorno das APIs.

Agora, as APIs, as tarefas de plano de fundo ou os consumidores de filas, não se importam com a resposta; eles só mandam mensagens. Basicamente, esse é nosso desenho de como está implementado o nosso sistema. No próximo vídeo eu vou te ajudar a trazer esse sistema para o seu computador para você rodar esse sistema, testar e ver se ele realmente está funcionando - ou ver se eu só coloquei um monte de *mocks* aqui.

Então te espero no próximo vídeo, para nós subirmos esse sistema e você testar na prática tudo isso que eu falei!

## Sobre o curso Microsserviços na prática: Entendendo a tomada de decisões

O [curso Microsserviços na prática: Entendendo a tomada de decisões](https://www.alura.com.br/curso-online-Microsservicos-pratica-tomada-decisoes) possui **123 minutos de vídeos**, em um total de **48 atividades**. Gostou? Conheça nossos outros **[cursos de Builds](https://www.alura.com.br/cursos-online-devops/build)** em **[DevOps](https://www.alura.com.br/cursos-online-devops)**, ou leia nossos [artigos de DevOps](https://www.alura.com.br/artigos/devops).

Matricule-se e comece a estudar com a gente hoje! Conheça outros tópicos abordados durante o curso:

- Boas-vindas à realidade
- O início de tudo
- Infraestrutura
- Build e Deploy
- Um pouco de código
- Front-end

## Aprenda Builds acessando integralmente esse e outros cursos, comece hoje!

#### PLUS

- Acesso a TODOS os cursos da plataforma

  

- Alura Challenges

  

- Alura Cases

  

- Certificado

  

- Alura Língua (incluindo curso Inglês para Devs)

  

12X

**R$85**

à vista R$1.020

[MATRICULE-SE](https://www.alura.com.br/compra/plus/)

#### PRO

- Acesso a TODOS os cursos da plataforma

  

- Alura Challenges

  

- Alura Cases

  

- Certificado

  

- Alura Língua (incluindo curso Inglês para Devs)

  

- https://www.guj.com.br/)