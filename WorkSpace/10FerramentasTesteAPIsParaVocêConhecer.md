# 10 Ferramentas de Teste de APIs para você conhecer



- [![img](https://cdn.infoq.com/statics_s2_20211214-0231/images/profiles/f52bFIS3ts3hKLTN2nvDeB1RXifNGhUN.jpg)](https://www.infoq.com/br/profile/Alice-Alder/)[Alice Alder](https://www.infoq.com/br/profile/Alice-Alder/)

  A humble tester. Loves exploratory testing.

- [Mariana Lopes](https://www.infoq.com/br/profile/Mariana-Lopes/)

O teste de APIs é um tipo de teste de software focado em determinar se as APIs desenvolvidas vão de encontro às expectativas relativamente à funcionalidade, confiabilidade, performance e segurança da aplicação.

Segundo o [Google Trends](https://trends.google.com/trends/explore?date=today 5-y&q=api testing), o interesse em termos relacionados ao teste de APIs vem aumentando nos últimos anos. Um estudo da Smartbear em 2017, feito com mais de 5.000 profissionais do desenvolvimento de software, mostrou que o número testes de APIs automatizados atinge mais de 50% dos testes existentes, e esses números tendem a crescer 30% nos próximos dois anos. Das pessoas participantes do estudo, 80% disseram ser responsáveis pelos testes de APIs.

Ter o processo, ferramenta e solução certas para a automação de testes de APIs são questões mais críticas do que nunca. Com as tendências atuais, testar APIs é mais do que uma solução de controle de qualidade: é um componente crucial no sucesso do desenvolvimento com entrega contínua (CI) e deploy contínuo (CD).

Este artigo fornece um sumário de 10 ferramentas de teste automatizados de APIs, abrangendo soluções *open-source* e comerciais que equipas de testes podem utilizar para suprir as suas necessidades.

![img](https://imgopt.infoq.com/fit-in/1200x2400/filters:quality(80)/filters:no_upscale()/articles/10-ferramentas-teste-api/pt/resources/23image2-1532546249498.png)

 

## 1. SoapUI

 

SoapUI é uma ferramenta de testes funcionais, dedicada ao teste de APIs, permitindo testar com facilidade APIs REST e SOAP, além de Web Services. Ao utilizar o SoapUI, é possível ter acesso ao código-fonte e criar novas funcionalidades de acordo com as suas necessidades, além de usufruir dos benefícios já existentes:

- Criar testes fácil e rapidamente, utilizando recursos *drag and drop.*
- Criar códigos customizados rapidamente código com Groovy.
- Criar testes poderosos, orientados a dados. Os dados podem ser carregados de ficheiros, bancos de dados ou Excel, sendo possível simular como consumidores interagem com as APIs.
- Criar cenários complexos, com suporte a testes assíncronos.
- Reutilizar scripts: dados de testes e questões de segurança podem ser reutilizadas para diversos casos de teste funcionais em apenas alguns passos.

**Website:** [www.soapui.org](https://www.soapui.org/) | **Preço:** Gratuito - USD 659 / ano

 

## 2. Postman

 

Criado originalmente um plugin do browser Chrome, agora o Postman também está disponível em versões nativas para Windows e Mac. O Postman é uma boa escolha para testes de APIs para quem não quer lidar com códigos integrados, utilizado a mesma linguagem de programação utilizada para o desenvolvimento das APIs. Principais benefícios:

- Cliente REST de fácil utilização, com uma rica interface
- Pode ser utilizado para automação de testes e também para a realização de testes exploratórios
- Pode ser executado em Mac, Windows, Linux e Chrome Apps
- Tem diversas integrações, como suporte para formatos Swagger e RAML
- Não força o time de testes a ter que aprender uma nova linguagem de programação
- Permite aos utilizadores facilmente partilhar o seu conhecimento com as equipas pois podem empacotar todos os pedidos e respostas esperadas e depois enviar para os seus colegas

**Website:** [www.getpostman.com](https://www.getpostman.com/) | **Preço:** Gratuito - USD 21 / usuário / mês

 

## 3. Katalon Studio

 

Katalon Studio é uma ferramenta de automação de testes que fornece um ambiente comum para criar e executar testes funcionais de UI, API e Web services, além de aplicativos móveis. O Katalon Studio suporta requisições SOAP e RESTful, com diversos tipos de comandos (GET, POST, PUT, DELETE) com possibilidade de parametrização. Principais destaques:

- Suporta testes combinados de UI e verificação por API
- Suporta testes de requisições SOAP e RESTful
- Compatível com uma das mais poderosas bibliotecas de validações, o AssertJ, permitindo criar validações fluentes, seguindo a prática de BDD
- Suporta abordagens orientadas a dados
- Pode ser utilizado para testes automatizados e exploratórios
- Amigável para pessoas com conhecimentos em desenvolvimento de software e pessoas sem tais conhecimentos.

**Website:** [www.katalon.com](https://www.katalon.com/) | **Preço:** Gratuito

 

## 4. Tricentis Tosca

 

Tricentis Tosca é uma plataforma de testes contínuos voltada para práticas Agile e DevOps. Principais benefícios:

- Suporta diversos protocolos, dentre eles: HTTP(s) JMS, AMQP, Rabbit MQ, TIBCO EMS, SOAP, REST, IBM MQ,NET TCP
- Potencializa a reutilização e facilita a manutenção, com automatização baseada em modelos
- Testes de APIs podem ser utilizados em aplicativos móveis, diversos browsers, aplicações empacotadas, e outras possibilidades
- Reduz o tempo de testes de regressão

**Website:** [www.tricentis.com](https://www.tricentis.com/software-testing-tools/) | **Preço:** Informação não disponibilizada

 

## 5. Apigee

 

Apigee é uma ferramenta de teste de APIs *cross-cloud*, que permite a quem utiliza medir e testar a performance de APIs, sendo possível a utilização de outros editores como o Swagger. O Apigee foi feito sob medida para negócios digitais e APIs orientadas a aplicativos móveis, ricas em dados e aplicações que os sustentam. Principais benefícios:

- É uma ferramenta criada em JavaScript
- Permite lidar com o monitoramento de design, implementação e escala de APIs
- Identifica gargalos de performance validando o tráfego das APIs, taxas de erro e tempos de resposta
- Cria facilmente proxies de API a partir da especificação Open API, fazendo o deploy desses proxies na nuve
- Possibilidade de implantação local, na nuvem ou em modelo híbrido com uma única base de código
- PCI, HIPAA, SOC2, e PII para aplicações e APIs

**Website:** [apigee.com/api-management](https://apigee.com/api-management/) | **Preço:** Avaliação gratuita - USD 2.500 / mês

 

## 6. JMeter

 

O JMeter é uma ferramenta *open-source* e largamente utilizada para testes de APIs funcionais, embora tenha sido criada, inicialmente, para testes de carga. Principais benefícios:

- Permite a repetição de resultados de testes
- Trabalha automaticamente com arquivos CSV, permitindo à equipe criar valores únicos de parâmetros para os testes de APIs rapidamente
- É possível incluir os testes de APIs em uma pipeline de integração contínua, graças à integração entre o JMeter e o Jenkins
- Pode ser utilizado para testes de performance de recursos estáticos e dinâmicos

**Website:** [jmeter.apache.org](https://jmeter.apache.org/) | **Preço:** Gratuito *(open-source)*

 

## 7. Rest-Assured

 

Rest-Assured é uma linguagem específica baseada em Java, que torna os testes de serviços REST mais simples. É uma ferramenta *open-source* e seus principais benefícios são:

- Tem um conjunto de funcionalidades já desenvolvidas, o que significa que quem utiliza não precisa criar códigos do zero
- Integra com o framework de automatização Serenity, possibilitando a combinação de testes UI e REST num único framework, que gera relatórios muito bons
- Suporte a sintaxe BDD: Given / When / Then
- Quem utiliza a ferramenta não precisa ter grandes conhecimentos sobre HTTP

**Website:** [rest-assured.io](http://rest-assured.io/) | **Preço:** Gratuito *(open-source)*

 

## 8. Assertible

 

Assertible é uma ferramenta de testes de APIs que se concentra na automação e na confiabilidade dos testes. Principais benefícios:

- Suporte para automatizar testes de API integrados aos passos da integração contínua e ao pipeline de entrega
- Suporte para executar testes a APIs após a realização de deploy, além de integração com ferramentas amplamente utilizadas como GitHub, Slack, e Zapier
- Suporta validação de respostas HTTP incluindo a validação do Schema JSON e verificação de integridade de dados JSON Path

**Website:** [assertible.com](https://assertible.com/) | **Preço:** Gratuito - USD 500 / mês

 

## 9. Karate DSL

 

Karate DSL é uma nova ferramenta de testes a APIs que ajuda a criar cenários para testes BDD baseados em APIs, de forma simples e sem escrever definições de passos. Essas definições foram criadas pela Karate DSL para que fosse possível iniciar os testes de APIs rapidamente. Principais benefícios:

- Construída baseado no Cucumber - JVM
- Pode executar um teste e gerar relatórios como qualquer projeto Java padrão
- Os testes podem ser escritos sem qualquer conhecimento de Java, permitindo a escrita de testes até para pessoas que não possuem conhecimento em programação
- Suporta alterações de configuração de acordo com ambientes de execução, e possui um sistema de execução multi-threads paralelas

**Website:** [github.com/intuit/karate](https://github.com/intuit/karate) | **Preço:** Gratuito *(open-source)*

 

## 10. Não existe a ferramenta perfeita

 

Apesar de impactante, essa frase é verdadeira. A lista acima lista boas soluções existentes no mercado para quem planeja começar ou aprimorar os testes automatizados em APIs. No entanto, como a maioria das soluções de desenvolvimento de software, encontrar a ferramenta perfeita é quase impossível.

Algumas pessoas podem achar que as funcionalidades das soluções comerciais, como Postman e Tricentis Tosca por exemplo, são excelentes, mas os custos para se ter tais ferramentas serão o fator bloqueante. Soluções *open-source*, como o JMeter, Rest-Assured e Karate DSL, não tem no preço um fator bloqueante, mas exigem recursos e esforço para utilizar as soluções corretamente. Por sua vez, ferramentas que parecem estar equilibradas entre custo e outros fatores, como Katalon Studio e Postman, podem ter outros inconvenientes para tipos específicos de projetos, sendo esses fatores que também precisam ser levados em consideração.

![img](https://imgopt.infoq.com/fit-in/1200x2400/filters:quality(80)/filters:no_upscale()/articles/10-ferramentas-teste-api/pt/resources/26image1-1532546250171.png)

Teste de APIs é uma forte tendência dentro do universo de automação de testes. Por esse motivo, mais ferramentas serão desenvolvidas para atender o aumento das demandas dos times de desenvolvimento de software. Encontrar a ferramenta perfeita continua a ser difícil, mas atualmente é possível encontrar mais opções do que existiam há tempos atrás.

Um bom caminho a ser traçado é de considerar as necessidades de um projeto, os prós e contras de cada uma das ferramentas e realizar uma prova de conceito com um grupo menor de ferramentas candidatas. Com base nos resultados das POCs criadas, será mais fácil entender os fatores críticos para um determinado cenário e refinar a busca para a melhor solução em um determinado contexto.

Artigo originalmente publicado em https://medium.com/@alicealdaine/top-10-api-testing-tools-rest-soap-services-5395cb03cfa9

##  

## Referências

· [Software Testing Trends for 2018 and Beyond](https://dzone.com/articles/software-testing-trends-for-2018-and-beyond)

· ["API Testing" Interest over time](https://trends.google.com/trends/explore?date=today 5-y&q=api testing) by Google Trends

· [API Testing Market by Component Vertical and Region - Global Forecast to 2022](https://www.researchandmarkets.com/publication/mpv2iah/4393652)

#### Conteúdo publicado no tópico [Arquitetura](https://www.infoq.com/br/architecture/)

##### Tópicos Relacionados:

 

- DESENVOLVIMENTO
- ARQUITETURA E DESIGN
- REST
- API
- ARQUITETUR
- SOA
- TESTES 
- MENSAGERIA
- WEB SERVICES 
- SOAP
- TESTES AUTOMATIZADOS
- ARQUITETURA CORPORATIVA
- WEB API

- #### CONTEÚDO EDITORIAL RELACIONADO

  - ##### [Adquira leads qualificados no mercado de desenvolvimento de software com a eMag InfoQ](https://www.infoq.com/br/news/2021/12/emag-sponsor/?itm_source=infoq&itm_medium=related_content_link&itm_campaign=relatedContent_articles_clk)

  - ##### [O último conteúdo do InfoQ Brasil](https://www.infoq.com/br/news/2021/02/ultimo-conteudo-do-infoq-brasil/?itm_source=infoq&itm_medium=related_content_link&itm_campaign=relatedContent_articles_clk)

  - ##### [O fim do Privacy Shield pode levar a um desastre para os provedores de nuvem em hiperescala](https://www.infoq.com/br/articles/privacy-shield-hyperscale-clouds/?itm_source=infoq&itm_medium=related_content_link&itm_campaign=relatedContent_articles_clk)

  - ##### [Entendendo Os Valores e Princípios Ágeis](https://www.infoq.com/br/minibooks/valores-principios-ageis/?itm_source=infoq&itm_medium=related_content_link&itm_campaign=relatedContent_articles_clk)

  - ##### [Somente empresas ágeis sobrevivem ao ambiente de negócios em constante mudança](https://www.infoq.com/br/articles/agile-survive-change/?itm_source=infoq&itm_medium=related_content_link&itm_campaign=relatedContent_articles_clk)

### CONTEÚDO RELACIONADO

- ##### [Adquira leads qualificados no mercado de desenvolvimento de software com a eMag InfoQ](https://www.infoq.com/br/news/2021/12/emag-sponsor/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=news_link&itm_content=link_text)

  14 DEZ 2021

- ##### [O último conteúdo do InfoQ Brasil](https://www.infoq.com/br/news/2021/02/ultimo-conteudo-do-infoq-brasil/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=news_link&itm_content=link_text)

  01 FEV 2021

- ##### [O fim do Privacy Shield pode levar a um desastre para os provedores de nuvem em hiperescala](https://www.infoq.com/br/articles/privacy-shield-hyperscale-clouds/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_text)

  28 JAN 2021

  [![O fim do Privacy Shield pode levar a um desastre para os provedores de nuvem em hiperescala](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/articles/privacy-shield-hyperscale-clouds/pt/smallimage/privacy-shield-hyperscale-clouds-s-1602019588203.jpeg)](https://www.infoq.com/br/articles/privacy-shield-hyperscale-clouds?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_image)

- Icon

  ##### [Entendendo Os Valores e Princípios Ágeis](https://www.infoq.com/br/minibooks/valores-principios-ageis/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=minibooks_link&itm_content=link_text)

  27 JAN 2021

  [![Entendendo Os Valores e Princípios Ágeis](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/minibooks/valores-principios-ageis/pt/smallimage/Agile-Manifesto-cover-s-1553351724445-1611705580472.jpg)](https://www.infoq.com/br/minibooks/valores-principios-ageis?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=minibooks_link&itm_content=link_image)

- ##### [Somente empresas ágeis sobrevivem ao ambiente de negócios em constante mudança](https://www.infoq.com/br/articles/agile-survive-change/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_text)

  26 JAN 2021

  [![Somente empresas ágeis sobrevivem ao ambiente de negócios em constante mudança](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/articles/agile-survive-change/pt/smallimage/agile-survive-change-s-1602517443986.jpeg)](https://www.infoq.com/br/articles/agile-survive-change?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_image)

- ##### [O Deno ama WebAssembly](https://www.infoq.com/br/articles/deno-loves-webassembly/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_text)

  19 JAN 2021

  [![O Deno ama WebAssembly](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/articles/deno-loves-webassembly/pt/smallimage/webassembly-s-1594649297194.jpg)](https://www.infoq.com/br/articles/deno-loves-webassembly?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_image)

- ##### [COVID-19 e Mineração de Redes Sociais - Habilitando Cargas de Trabalho de Aprendizado de Máquina com Big Data](https://www.infoq.com/br/articles/covid-social-media-machine-learning/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_text)

  14 JAN 2021

  [![COVID-19 e Mineração de Redes Sociais - Habilitando Cargas de Trabalho de Aprendizado de Máquina com Big Data](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/articles/covid-social-media-machine-learning/pt/smallimage/covid-social-media-machine-learning-s-1601562448288.jpeg)](https://www.infoq.com/br/articles/covid-social-media-machine-learning?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_image)

- ##### [Da Cloud ao Cloudlets: Seria uma nova abordagem para processamento de dados?](https://www.infoq.com/br/articles/cloud-to-cloudlets-data-processing/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_text)

  04 JAN 2021

  [![Da Cloud ao Cloudlets: Seria uma nova abordagem para processamento de dados?](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/articles/cloud-to-cloudlets-data-processing/pt/smallimage/cloud-to-cloudlets-data-processing-s-1601399656392.jpeg)](https://www.infoq.com/br/articles/cloud-to-cloudlets-data-processing?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_image)

- ##### [A inteligência artificial estaria mais próxima do bom senso?](https://www.infoq.com/br/articles/AI-Closer-Common-Sense/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_text)

  30 DEZ 2020

  [![A inteligência artificial estaria mais próxima do bom senso?](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/articles/AI-Closer-Common-Sense/pt/smallimage/AI-Closer-Common-Sense-s-1602793883610.jpeg)](https://www.infoq.com/br/articles/AI-Closer-Common-Sense?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_image)

- ##### [APIs em tempo real no contexto do Apache Kafka](https://www.infoq.com/br/articles/real-time-api-kafka/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_text)

  29 DEZ 2020

  [![APIs em tempo real no contexto do Apache Kafka](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/articles/real-time-api-kafka/pt/smallimage/real-time-api-kafka-s-1602600487985.jpeg)](https://www.infoq.com/br/articles/real-time-api-kafka?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_image)

- ##### [Bate papo sobre o livro Gamificação Infinita](https://www.infoq.com/br/articles/book-review-infinite-gamification/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_text)

  28 DEZ 2020

  [![Bate papo sobre o livro Gamificação Infinita](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/articles/book-review-infinite-gamification/pt/smallimage/the-infinite-gamification-s-1601969529743.jpeg)](https://www.infoq.com/br/articles/book-review-infinite-gamification?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_image)

### CONTEÚDO RELACIONADO

- ##### [Trabalho remoto: Boas práticas e recursos úteis](https://www.infoq.com/br/articles/working-remotely-resources/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_text)

  23 DEZ 2020

  [![Trabalho remoto: Boas práticas e recursos úteis](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/articles/working-remotely-resources/pt/smallimage/working-remotely-resources-s-1587052679254.jpg)](https://www.infoq.com/br/articles/working-remotely-resources?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_image)

- ##### [Bate papo sobre o Livro Liderando com o Senso Incomum](https://www.infoq.com/br/articles/book-review-leading-uncommon-sense/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_text)

  22 DEZ 2020

  [![Bate papo sobre o Livro Liderando com o Senso Incomum](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/articles/book-review-leading-uncommon-sense/pt/smallimage/leading-uncommon-sense-s-1602705665083.jpeg)](https://www.infoq.com/br/articles/book-review-leading-uncommon-sense?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_image)

- ##### [Desafios na avaliação postural humana em aplicativos de condicionamento físico baseados em IA](https://www.infoq.com/br/articles/human-pose-estimation-ai-powered-fitness-apps/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_text)

  21 DEZ 2020

  [![Desafios na avaliação postural humana em aplicativos de condicionamento físico baseados em IA](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/articles/human-pose-estimation-ai-powered-fitness-apps/pt/smallimage/human-pose-estimation-ai-powered-fitness-apps-s-1602698421552.jpeg)](https://www.infoq.com/br/articles/human-pose-estimation-ai-powered-fitness-apps?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_image)

- ##### [Apache Arrow e Java: Transferência de Big Data na velocidade da luz](https://www.infoq.com/br/articles/apache-arrow-java/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_text)

  18 DEZ 2020

  [![Apache Arrow e Java: Transferência de Big Data na velocidade da luz](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/articles/apache-arrow-java/pt/smallimage/arrow-s-1590010308987.jpg)](https://www.infoq.com/br/articles/apache-arrow-java?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_image)

- ##### [Bate papo sobre o livro “De pé sobre os ombros: Um guia para líderes na transformação digital"](https://www.infoq.com/br/articles/book-review-leaders-guide-digital-transformation/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_text)

  17 DEZ 2020

  [![Bate papo sobre o livro “De pé sobre os ombros: Um guia para líderes na transformação digital"](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/articles/book-review-leaders-guide-digital-transformation/pt/smallimage/digital-transformation-s-1595505972427.jpg)](https://www.infoq.com/br/articles/book-review-leaders-guide-digital-transformation?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_image)

- ##### [Sete duras lições aprendidas na migração de um monólito para microservices](https://www.infoq.com/br/articles/lessons-learned-monolith-microservices/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_text)

  16 DEZ 2020

  [![Sete duras lições aprendidas na migração de um monólito para microservices](https://imgopt.infoq.com/fit-in/50x50/filters:quality(80)/articles/lessons-learned-monolith-microservices/pt/smallimage/Lessons-Learned-Migrating-a-Monolith-to-Microservices-logo-small-1602847857985.jpg)](https://www.infoq.com/br/articles/lessons-learned-monolith-microservices?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=articles_link&itm_content=link_image)

### CONTEÚDO RELACIONADO



- https://www.infoq.com/br/articles/10-ferramentas-teste-api/#)

- [DESENVOLVIMENTO](https://www.infoq.com/br/development/)

  - ##### [Crank, o novo framework frontend com renderização assíncrona integrada - Bate papo com Brian Kim](https://www.infoq.com/br/articles/crank-frontend-framework-asynchronous-rendering/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

  - ##### [Blockchain Empresarial: Jornada de uma rede multi-organização à produção](https://www.infoq.com/br/presentations/blockchain-empresarial-jornada-de-uma-rede/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

  - ##### [PHP 7 - Melhorias na biblioteca padrão](https://www.infoq.com/br/articles/php7-function-improvements/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

- [ARQUITETURA E DESIGN](https://www.infoq.com/br/architecture-design/)

  - ##### [O último conteúdo do InfoQ Brasil](https://www.infoq.com/br/news/2021/02/ultimo-conteudo-do-infoq-brasil/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

  - ##### [APIs em tempo real no contexto do Apache Kafka](https://www.infoq.com/br/articles/real-time-api-kafka/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

  - ##### [Sete duras lições aprendidas na migração de um monólito para microservices](https://www.infoq.com/br/articles/lessons-learned-monolith-microservices/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

- [CULTURA E MÉTODOS](https://www.infoq.com/br/culture-methods/)

  - ##### [Adquira leads qualificados no mercado de desenvolvimento de software com a eMag InfoQ](https://www.infoq.com/br/news/2021/12/emag-sponsor/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

  - ##### [Entendendo Os Valores e Princípios Ágeis](https://www.infoq.com/br/minibooks/valores-principios-ageis/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

  - ##### [Somente empresas ágeis sobrevivem ao ambiente de negócios em constante mudança](https://www.infoq.com/br/articles/agile-survive-change/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

- [IA, ML E ENGENHARIA DE DADOS](https://www.infoq.com/br/ai-ml-data-eng/)

  - ##### [COVID-19 e Mineração de Redes Sociais - Habilitando Cargas de Trabalho de Aprendizado de Máquina com Big Data](https://www.infoq.com/br/articles/covid-social-media-machine-learning/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

  - ##### [A inteligência artificial estaria mais próxima do bom senso?](https://www.infoq.com/br/articles/AI-Closer-Common-Sense/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

  - ##### [Desafios na avaliação postural humana em aplicativos de condicionamento físico baseados em IA](https://www.infoq.com/br/articles/human-pose-estimation-ai-powered-fitness-apps/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

- [DEVOPS](https://www.infoq.com/br/devops/)

  - ##### [Bate papo sobre o livro “De pé sobre os ombros: Um guia para líderes na transformação digital"](https://www.infoq.com/br/articles/book-review-leaders-guide-digital-transformation/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

  - ##### [Arquitetura de Microservices Multi-Runtime](https://www.infoq.com/br/articles/multi-runtime-microservice-architecture/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

  - ##### [Armadilhas de design NoSQL com Java](https://www.infoq.com/br/articles/armadilhas-design-nosql-com-java/?itm_source=infoq&itm_campaign=footer_links&itm_medium=footer_links_article_page)

