https://cio.com.br/tendencias/)

# Da teoria à prática: tudo que você precisa saber sobre microsserviços

## A maneira como microsserviços são implementados os torna uma base natural para aplicativos modernos baseados em nuvem

***\*Josh Fruhlinger, Infoworld\****

25/10/2019 às 8h50

![img](https://cio.com.br/wp-content/uploads/2019/10/o-que-sao-microsservic%CC%A7os.jpg)

Foto: Thinkstock

 https://cio.com.br/tendencias/da-teoria-a-pratica-tudo-que-voce-precisa-saber-sobre-microsservicos/

[Facebook](https://cio.com.br/#facebook)[LinkedIn](https://cio.com.br/#linkedin)[Twitter](https://cio.com.br/#twitter)[WhatsApp](https://cio.com.br/#whatsapp)[Flipboard](https://cio.com.br/#flipboard)[Email](https://cio.com.br/#email)



Quase todo sistema de computador executa várias tarefas usando recursos compartilhados, e uma das questões da programação de computadores é a proximidade com a qual os bits de código que executam essas tarefas devem estar ligados. Uma resposta cada vez mais popular é o conceito de **microsserviço** - um pequeno pedaço de funcionalidade que interage com outros microsserviços para criar um sistema maior.



Embora a ideia básica de ter esses componentes não seja nova, a maneira como os microsserviços são implementados os torna uma base natural para os aplicativos modernos baseados em nuvem. Os microsserviços também se encaixam na filosofia devops, que incentiva rápida e continuamente a implantação de novas funcionalidades.

## O que são microsserviços?



O "micro" em microsserviços implica que essas são pequenas aplicações. Às vezes isso é verdade, mas a melhor maneira de pensar sobre o assunto é que eles devem ter apenas o tamanho necessário para executar uma ação específica ou resolver um problema específico. Esse problema deve ser conceitual, não técnico. Como a Microsoft coloca: "Os microsserviços devem ser projetados com base nos recursos de negócios, e não em camadas horizontais, como acesso a dados ou mensagens". Eles se comunicam com outros microsserviços e usuários externos por meio de APIs relativamente estáveis para criar um aplicativo maior.



Assim, a funcionalidade interna de um microsserviço pode ser aprimorada ou radicalmente atualizada sem afetar o restante do sistema. Isso, por sua vez, está relacionado à maneira como as lojas de devops procuram operar: se as funções específicas de um aplicativo maior são segmentadas em partes de código independentes, é mais fácil viver o mantra de devops de CI/CD (integração contínua e entrega contínua) . Além disso, APIs bem definidas facilitam o teste automático dos microsserviços.

## Arquitetura de microsserviços vs. arquitetura monolítica



Você ouvirá frequentemente os microsserviços mencionados em termos de uma “arquitetura de microsserviços”. Esse termo abrange não apenas os microsserviços, mas os componentes para gerenciamento e descoberta de serviços, além de um gateway de API que lida com a comunicação entre os microsserviços e o mundo exterior.



Uma "aplicação monolítica" é o oposto do que são microsserviços. É um retrônimo para um aplicativo em que todo o código está em um grande arquivo executável binário. Como o TechTarget explica, um aplicativo monolítico é mais difícil de escalar e mais difícil de melhorar. Mas, por ser construído como um único aplicativo coeso, não requer tanto gerenciamento quanto uma arquitetura de microsserviços.

## Conceitos limitados: como definir um microsserviço



Vamos voltar por um momento ao nosso pensamento anterior de que os microsserviços devem executar uma ação específica. É fácil dizer, mas, na prática, a funcionalidade é muitas vezes entrelaçada, e desenhar divisões é mais difícil do que parece. A análise de domínio e o design orientado ao domínio são as abordagens teóricas que ajudarão você a separar sua tarefa geral em problemas individuais que um microsserviço pode resolver. Nesse processo, descrito em uma série esclarecedora de postagens da Microsoft, você cria um modelo abstrato do domínio de negócios e descobre os contextos limitados, que agrupam a funcionalidade que interage com o mundo de uma maneira específica.



Por exemplo, você pode ter um contexto limitado para remessa e outro para contas. Um objeto físico do mundo real teria um preço e um local para onde precisa ir, é claro, mas os contextos limitados representam maneiras específicas pelas quais seu aplicativo pensa e interage com esses objetos. Cada microsserviço deve existir inteiramente em um único contexto limitado, embora alguns contextos limitados possam abranger mais de um microsserviço.

## Microsserviços x arquitetura orientada a serviços x serviços da Web



Nesse ponto, se você é um profissional de TI que está no mercado há algum tempo, pode pensar que muito disso parece familiar. A ideia de pequenos programas individuais trabalhando juntos pode lembrá-lo de SOA (arquitetura orientada a serviços) e de serviços da Web, duas palavras-chave dos inebriantes dias da Web 2.0 dos anos 2000. Enquanto, em certo sentido, não há realmente nada de novo sob o sol, há distinções importantes entre esses conceitos e microsserviços. O Datamation apresenta um bom detalhamento das diferenças, mas aqui está uma versão curta para você:



Em uma arquitetura orientada a serviços, os componentes individuais são fortemente acoplados, geralmente compartilhando ativos como armazenamento e se comunicam por meio de um software especializado. Os microsserviços são mais independentes, compartilham menos recursos e se comunicam por meio de protocolos mais leves. Vale a pena notar que os microsserviços surgiram do meio SOA e, às vezes, são considerados um tipo de SOA, ou um sucessor do conceito.



Um serviço da Web é um conjunto de funcionalidades voltado para o público que outros aplicativos podem acessar via Web; provavelmente o exemplo mais prevalente é o Google Maps, onde o site de um restaurante, por exemplo, pode ser incorporado para fornecer orientações aos clientes. Essa é uma conexão muito mais flexível do que você veria em uma arquitetura de microsserviços.

## Comunicação de microsserviços



Os microsserviços devem ter como objetivo usar métodos de comunicação básicos e bem estabelecidos, em vez de integração complexa e rígida. Como observado, isso é outra coisa que distingue microsserviços de SOA.



Em geral, a comunicação entre microsserviços deve ser assíncrona. Vale destacar, no entanto, que ainda é bom usar protocolos de comunicação síncrona como HTTP, embora protocolos assíncronos como AMQP (Advanced Message Queuing Protocol) também sejam comuns em arquiteturas de microsserviços. Esse tipo de acoplamento flexível torna a arquitetura de microsserviços mais flexível diante da falha de componentes ou de partes individuais da rede, o que é um benefício importante.

## Microsserviços, Java e Spring Boot e Spring Cloud



Alguns dos primeiros trabalhos em microsserviços surgiram na comunidade Java, e Martin Fowler foi um dos primeiros defensores. Uma conferência Java de 2012 na Polônia foi palco de uma das apresentações mais importantes sobre o assunto, onde foi recomendada a aplicação dos princípios que orientavam o desenvolvimento dos primeiros aplicativos Unix na década de 1970.



Como resultado desse histórico, existem diversas estruturas Java que permitem a criação de microsserviços. Um dos mais populares é o Spring Boot, projetado especificamente para microsserviços. A inicialização é estendida pelo Spring Cloud, que, como o nome sugere, permite implantar esses serviços na nuvem também. A Pivotal Software, desenvolvedora do Spring, tem um bom tutorial sobre como iniciar o desenvolvimento de microsserviços usando essas estruturas.

## Microsserviços e contêineres: Docker, Kubernetes e mais



A tecnologia subjacente que foi mais longe no sentido de obter microsserviços no mainstream são os contêineres. Um contêiner é semelhante a uma instância de VM, mas, em vez de incluir todo um SO independente, o contêiner é apenas um espaço isolado que utiliza o kernel do sistema operacional host, mas mantém o código em execução dentro dele. Os contêineres são muito menores que as instâncias de VM e são fáceis de implantar rapidamente, localmente ou na nuvem.



O apelo dos contêineres para microsserviços deve ser óbvio: cada microsserviço pode ser executado em seu próprio contêiner, o que reduz significativamente a sobrecarga do gerenciamento de serviços. A maioria das implementações de contêineres possui ferramentas de orquestração complementares que automatizam a implantação, gerenciamento, dimensionamento, rede e disponibilidade de aplicativos baseados em contêiner. É a combinação de microsserviços pequenos e fáceis de criar e contêineres fáceis de implantar que possibilita a filosofia dos devops . Existem várias implementações do conceito de contêiner, mas a mais popular é o Docker, que geralmente é emparelhado com o Kubernetes como plataforma de orquestração.



O Spring, embora popular, está ligado à plataforma Java. Os sistemas baseados em contêiner, por outro lado, são poliglotas: qualquer linguagem de programação suportada pelo sistema operacional pode ser executada em um contêiner, o que oferece mais flexibilidade aos programadores. De fato, uma grande vantagem dos microsserviços é que cada serviço pode ser escrito em qualquer linguagem que faça mais sentido ou com a qual os desenvolvedores se sintam mais confortáveis. Vale destacar que um serviço pode ser completamente reconstruído em uma nova linguagem sem afetar o sistema como um todo, desde que suas APIs permaneçam estáveis. O DZone tem um artigo discutindo os prós e contras do Spring Cloud vs. Kubernetes para microsserviços.

## Microsserviços e nuvem: AWS e Azure



Como observado acima, uma das vantagens do uso de contêineres é que eles podem ser facilmente implantados na nuvem, onde estão disponíveis recursos de computação flexíveis para que você possa maximizar a eficiência do aplicativo. Como você pode imaginar, os principais fornecedores de nuvem pública estão ansiosos para que você use suas plataformas para executar seus aplicativos baseados em microsserviços. Para mais informações, consulte os recursos da Amazon, Microsoft e Google.