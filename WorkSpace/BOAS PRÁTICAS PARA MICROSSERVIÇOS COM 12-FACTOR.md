# BOAS PRÁTICAS PARA MICROSSERVIÇOS COM 12-FACTOR



[Desenvolvimento de Software](https://softdesign.com.br/categoria/desenvolvimento-de-software)

**por [Ricardo Camelo](https://softdesign.com.br/blog/author/ricardo-camelo) em 4 de fevereiro de 2021**

No [artigo anterior](https://softdesign.com.br/blog/monolitos-servicos-e-microsservicos-impactos-nos-negocios/) desta série, explicamos o que são microsserviços, quais suas vantagens e desvantagens, e também destacamos quando você deve utilizá-los. Depois dessa leitura, se você acredita que microsserviços são uma boa escolha para o seu produto, então continue com este artigo, e descubra boas práticas para seguir na adoção da arquitetura: a 12-factor.

#### **Um checklist de 12 passos**

A referência mais conhecida de boas práticas para desenvolvimento de serviços é a chamada [12-Factor](https://softdesign.com.br/blog/the-twelve-factor-app/). Criada por Adam Wiggins, co-fundador do [Heroku](https://www.heroku.com/), ela é apresentada como “uma metodologia para construção de software como serviço”, tendo sido criada com base na experiência vivida na própria empresa, onde mais de 9 milhões de serviços estão implantados (*deployed*).

Na verdade, o 12-factor funciona como um *checklist* de boas práticas, que passam por tópicos como gestão de configuração, arquitetura interna, DevOps e gerenciamento do ciclo de vida dos serviços.

#### **Os 12 fatores são:**

**Base de código:** o código da aplicação deve estar em um sistema de controle de versão (como Git, por exemplo). A base de código deve ser capaz de gerar múltiplas implantações (para ambientes de teste, homologação e produção, etc.). Diferentes bases de código não devem ter código repetido, as repetições devem ser tratadas como novas aplicações, incluídas através de um sistema de gestão de dependências.

**Dependências:** todas as dependências devem estar declaradas de forma precisa. Uma aplicação nunca deve assumir que as bibliotecas ou ferramentas das quais dependem já estão presentes, ela sempre deve se responsabilizar pela configuração dos seus pré-requisitos.

**Configurações:** as configurações que variam para cada ambiente, como a conexão com serviços externos e suas credenciais, devem estar separadas do código, tratadas como variáveis de ambiente, definidas de forma independente da linguagem ou do sistema operacional em uso.

**Serviços de apoio:** serviços que a aplicação consome para seu funcionamento normal, como bases de dados, sistemas de fila ou mensageria, serviços de envio de e-mail, entre outros, devem ser tratados como recursos conectados, ou seja, devem ter baixo acoplamento. Por exemplo, deve ser possível alterar o apontamento facilmente, sem precisar alterar código e fazer nova publicação.

**Build, release, run:** a transformação da base de código em uma implantação deve ser feita em uma sequência de estágios claramente separados: *build* (construção), *release* (quando o *build* é combinado com as configurações), *run* (quando o processo do app é iniciado para uma release específica).

**Processos:** as aplicações devem ser executadas como um ou mais processos, e esses devem ser *stateless* e *share-nothing*, ou seja, não devem persistir dados além da transação atual, e não devem depender do estado de outros processos para realizar sua transação.

**Port binding:** a aplicação deve ser completamente autocontida, inclusive quanto à forma de receber requisições. Assim, ela não deve depender de um servidor web no seu ambiente, mas sim conter uma dependência para uma biblioteca que permita que a própria aplicação se vincule a uma porta e escute as solicitações.

**Concorrência:** o conceito central são os processos. Uma aplicação deve ser executada através de processos isolados, de maneira que a solução possa ser arquitetada para tratar as cargas diversas de cada uma das suas partes com tipos de processos mais adequados. Assim, é mais fácil escalar cada serviço conforme a necessidade.

**Descartabilidade (disposability):** os processos devem ser projetados para que possam ser iniciados e encerrados a qualquer momento, facilmente. Isso inclui, por exemplo, garantir que o tempo de inicialização seja rápido, e que o processo de encerramento seja suave (*gracefully shut down*).

**Paridade dos ambientes:** desenvolvimento, teste e produção devem ser tão parecidos quanto possível, permitindo a implantação continua (*continuous deployment*). O objetivo é possibilitar múltiplos *deploys* por dia, sem depender de pessoal externo ao time de desenvolvimento.

**Logs:** os dados de log gerados pela aplicação devem ser tratados como uma transmissão (*stream*). A aplicação não pode ser responsável por definir o destino ou armazenar essa *stream*. A *stream* deve ser capturada e tratada de forma diferente em cada ambiente, e isso não deve afetar o código interno da aplicação.

**Processos de manutenção:** processos pontuais de manutenção que eventualmente precisam ser realizados (executar um script, alterar a base de dados, etc.) devem ser executados no mesmo ambiente da aplicação, usando a mesma base de código e as mesmas configurações.

A grande preocupação é oferecer um conjunto de práticas que evitem os problemas comuns enfrentados quando se torna necessário escalar as aplicações. Por isso, aplicações que seguem o 12-factor tendem a ser soluções desacopladas, autocontidas, portáveis, robustas, escaláveis e mais resilientes.

#### **Mudanças culturais**

Note que seguir os 12 fatores exige não só modificação da arquitetura das aplicações, mas também engloba questões que muitas vezes afetam a cultura e a estrutura organizacional. O método pressupõe uma abordagem de entrega contínua e uma filosofia DevOps, onde o time que desenvolve o produto também engloba as habilidades necessárias para sua operação, e onde a automação da infraestrutura permite atingir novas capacidades.

No limite, o método pressupõe uma cultura de produto. Não há um time temporário de projeto, ou silos responsáveis por diferentes atividades. Ao invés disso, um time de produto acompanha todo o ciclo de vida das aplicações necessárias para entregar as capacidades organizacionais pelas quais o time é responsável.

É claro que essa cultura também pode ser adotada com produtos monolíticos, mas a granularidade das arquiteturas de serviços torna mais óbvia uma estrutura organizacional onde a responsabilidade (ou *ownership*) do produto não é desmembrada por etapas de um projeto ou por atividades a realizar, mas sim por capacidades ou domínios do negócio, a mesma lógica de desmembramento usada para definir a fronteiras dos próprios serviços.

[12-factor](https://softdesign.com.br/blog/tag/12-factor)[boas práticas](https://softdesign.com.br/blog/tag/boas-praticas)[microsserviços](https://softdesign.com.br/blog/tag/microsservicos)

Sugestões ou críticas para nosso blog? Entre em contato pelo endereço mkt@softdesign.com.br.

![Foto do autor](https://softdesign.com.br/wp-content/uploads/2020/11/camelo-125x125.jpg)

### Ricardo Camelo

Arquiteto de software, especialista em Java Programming, System Design and Enginering, Enterprise Applications and Web Development.

POSTS RELACIONADOS

[Desenvolvimento de Software](https://softdesign.com.br/categoria/desenvolvimento-de-software)[Negócios Digitais](https://softdesign.com.br/categoria/negocios-digitais)[TOP 5 POSTS SOFTDESIGN 2021](https://softdesign.com.br/blog/top-5-posts-softdesign-2021)**por [Pâmela Seyffert](https://softdesign.com.br/blog/author/pamela-seyffert) em 23 de dezembro de 2021**

Neste ano, publicamos 77 conteúdos em nosso blog. Ao longo desse período, abordamos os mais variados assuntos: métodos ágeis, modelos de startup (Unicórnio, Camelo e Zebra), Design Thinking, Transformação Digital, low-code e no-code, big data e métricas de produto. Ainda, tutoriais de conteúdos técnicos apresentados por nossas pessoas colaboradoras nas edições do SoftDrops e participações…

[continuar lendo![img](https://softdesign.com.br/wp-content/themes/bones/library/images/saiba-mais-news.png)](https://softdesign.com.br/blog/top-5-posts-softdesign-2021)

[Desenvolvimento de Software](https://softdesign.com.br/categoria/desenvolvimento-de-software)[Inovação](https://softdesign.com.br/categoria/inovacao)[Negócios Digitais](https://softdesign.com.br/categoria/negocios-digitais)[TENDÊNCIAS DE TECNOLOGIA PARA 2022](https://softdesign.com.br/blog/tendencias-de-tecnologia-para-2022)**por [Pâmela Seyffert](https://softdesign.com.br/blog/author/pamela-seyffert) em 14 de dezembro de 2021**

2021 foi um ano repleto de desafios complexos, que nos fizeram refletir profundamente. Por meio da tecnologia, a sociedade trilhou um novo caminho de desenvolvimento, expandindo fronteiras e aprimorando processos e sistemas. Agora, é tempo de prever os próximos passos e de construir as novas estratégias. Para lhe inspirar, compartilhamos abaixo highlights extraídos do relatório…

[continuar lendo![img](https://softdesign.com.br/wp-content/themes/bones/library/images/saiba-mais-news.png)](https://softdesign.com.br/blog/tendencias-de-tecnologia-para-2022)

[![Up arrow](https://softdesign.com.br/wp-content/themes/bones/library/images/up-arrow.png)](https://softdesign.com.br/blog/boas-praticas-para-microsservicos-com-12-factor#news-banner)

Deseja receber novidades sobre

## DESIGN, AGILIDADE e TECNOLOGIA?



[![img](https://softdesign.com.br/wp-content/themes/bones/library/images/logo-rodape.svg)](https://softdesign.com.br/)[QUEM SOMOS](https://softdesign.com.br/quem-somos/)[TRABALHE CONOSCO](https://softdesign.com.br/vem-pra-soft)[PROGRAMA DE TRAINEE](https://conteudo.softdesign.com.br/programa_trainee_softdesign)[POLÍTICA DE PRIVACIDADE](https://softdesign.com.br/politica-de-privacidade/)

## +55 51 3022.1367

## +55 51 3286.1631

Rua Siqueira Campos, 1184 / 1° andar
Centro Histórico – CEP: 90010-001
Porto Alegre – RS

[![Redes sociais](https://softdesign.com.br/wp-content/uploads/2020/04/ic-facebook.svg)](https://www.facebook.com/softdesignbrasil/)[![Redes sociais](https://softdesign.com.br/wp-content/uploads/2020/04/ic-instagram.svg)](https://www.instagram.com/softdesignbrasil/)[![Redes sociais](https://softdesign.com.br/wp-content/uploads/2020/04/ic-twitter.svg)](https://twitter.com/softdesignbr)[![Redes sociais](https://softdesign.com.br/wp-content/uploads/2020/04/in-linkedin.svg)](https://www.linkedin.com/company/softdesignbrasil/)[![Redes sociais](https://softdesign.com.br/wp-content/uploads/2020/04/ic-youtube.svg)](https://www.youtube.com/user/softdesignrs)

© 2022 SoftDesign. Todos os direitos reservados.

### 

[![img](https://softdesign.com.br/wp-content/uploads/2020/01/Union.svg)](https://softdesign.com.br/servicos/concepcao)[![img](https://softdesign.com.br/wp-content/uploads/2020/01/desenvolvimento-de-software-icon.svg)](https://softdesign.com.br/servicos/desenvolvimento-de-software)[![img](https://softdesign.com.br/wp-content/uploads/2020/01/Union-1.svg)](https://softdesign.com.br/servicos/consultoria)[![img](https://softdesign.com.br/wp-content/uploads/2020/03/Vector-3.svg)](https://softdesign.com.br/servicos/outsourcing)



<iframe id="rd_tmgr" style="hyphens: none; box-sizing: border-box; color: rgb(92, 107, 128); font-family: Lato, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; width: 1px; height: 1px; position: absolute; top: -100px;"></iframe>