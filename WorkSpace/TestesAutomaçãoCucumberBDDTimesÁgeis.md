# Testes de Automação com Cucumber BDD em times Ágeis

CURTIR[DÊ SUA OPINIÃO](https://www.infoq.com/br/articles/cucumber-bdd-automation-testing/#theCommentsSection)PRINT

27 NOV 2018 11 MIN(S) DE LEITURA

por

- [![img](https://cdn.infoq.com/statics_s2_20211214-0231/images/profiles/hGaJHWY0kh5u8vS0JvpRQ9H8uzeRGpDK.jpg)](https://www.infoq.com/br/profile/Trong-Bui/)[Trong Bui](https://www.infoq.com/br/profile/Trong-Bui/)

revisados por

- [Mayra Michels](https://www.infoq.com/br/profile/Mayra-Michels/)

Nos últimos anos, há cada vez mais equipes de software implementado a metodologia de software Ágil em seu processo de desenvolvimento para se adaptar a esse mercado volátil. Essa tendência desafia as equipes de teste na gerência de casos e scripts de teste que precisam ser mantidos de acordo com os requisitos em constante mudança. Encontrar um método de teste apropriado desde o início é um dos elementos-chave para um projeto de software Ágil bem-sucedido.

## O que é o Cucumber?

Muitas equipes Ágeis implementaram com sucesso o método BDD (Behavior-Driven Development - Desenvolvimento Orientado por Comportamento) em seu processo de teste usando a ferramenta Cucumber. Mas o que é Cucumber? E por que essa estratégia é a adequada e sugerida para projetos Ágeis, junto com o BDD?

O [Cucumber](https://cucumber.io/) é uma ferramenta usada para executar testes de aceitação automatizados que foram criados em um formato BDD. Um de seus recursos mais destacados é a capacidade de realizar descrições funcionais de texto simples (escritas numa linguagem chamada Gherkin) como testes automatizados. Vamos dar uma olhada no exemplo:

```
Feature: Update password
  Scenario: Admin user can update the user password
Given I am in the HR system with an Admin account
When I update password of another user
Then I receive a message for updating password successfully
And user password is updated to the new password
```

Esta característica incrível da abordagem BDD apresenta as seguintes vantagens:

- Escrever testes de BDD em uma linguagem onipresente, estruturada em torno do modelo de domínio e amplamente usada por todos os membros da equipe incluindo desenvolvedores, testadores, analistas de negócio e clientes;
- Conexão técnica com membros não técnicos de uma equipe de software;
- Permitir a interação direta com o código do desenvolvedor; os testes de BDD são escritos em um idioma que também podem ser criados pelos stakeholders envolvidos;
- Por último, mas não menos importante, os testes de aceitação podem ser executados automaticamente, enquanto são executados manualmente pelos stakeholders.

## O Cucumber ajuda a melhorar a comunicação

O Cucumber ajuda a melhorar a comunicação entre membros técnicos e não técnicos em um mesmo projeto. Isso pode ser observado no requisito abaixo e seus testes de automação:

```
1 As an Admin User,
2 I would like to change the password of other user's accounts.
3 Feature: Update password
4   Scenario: Admin user can update the user password
5     Given I am in the HR system with an Admin account
6     When I update password of another user
7     Then I receive a message for updating password successfully
8     And user's password is updated to the new password
```

Com TestNG, o cenário de teste acima pode ser implementado conforme abaixo:

```
1 @test
2 public void testAdminUserCanUpdateUserAccountPassword() {
3   // criar usuários
4   User userAdmin = new User(UserRole.ADMIN, username, password);
5   User user = new User(UserRole.VIEWER, user_username, user_password);
6
7   // use o Admin user para atualizar a senha de um usuário
8    String message = userAdmin.updatePassword(user, user_new_password);
9
10 // verifica a mudança de senha
11    Assert.assertEquals(message, "Password changed successfully");
12    Assert.assertEquals(user.getPassword(), user_new_password);
13 }
```

O mesmo caso de teste pode ser escrito usando o Cucumber:

```
1 Feature: Update password
2  Scenario: Admin user can update the user password
3    Given I am in the HR system with an Admin account
4    When I update password of another user
5    Then I receive a message for updating password successfully
6    And user's password is updated to the new password
```

Ambos os scripts de teste de automação apresentam um bom desempenho para concluir o teste automaticamente. Mas todos os testadores do seu time fazem esses testes? Outros analistas de negócios e stakeholders podem usar esses testes novamente no estágio de teste de aceitação?

O teste de automação com o TestNG pode ser difícil para a maioria dos testadores manuais e analistas de negócio. Além disso, é impossível usar este teste novamente para o teste de aceitação. Como resultado, com base nessas falhas mencionadas anteriormente, isso não pode ser considerado como um método adequado.

Por outro lado, o teste de automação usando o Cucumber é criado em uma linguagem de domínio do negócio, ou em uma linguagem natural, que pode ser facilmente produzida por todos os membros do projeto. A comunicação é crucial para qualquer time de desenvolvimento, especialmente para um time Ágil. Geralmente, há muitos bate-papos, discussões e longas argumentações entre desenvolvedores e testadores para descobrir qual é o comportamento correto de uma funcionalidade. Usando o Cucumber, a mesma especificação da funcionalidade agora é usada para o desenvolvimento pelos desenvolvedores, e para testes pelos testadores. É considerada uma ferramenta poderosa porque pode ajudar a reduzir o risco de mal-entendidos, bem como a falha na comunicação.

## O Cucumber é uma ferramenta de teste de aceitação automatizada

O teste de aceitação geralmente é realizado por analistas de negócio/clientes para garantir que o time de desenvolvimento tenha construído as funcionalidades exatas. A atividade típica neste estágio de teste é verificar o sistema em relação aos requisitos originais com dados reais específicos da produção. O teste do Cucumber não apenas segue os requisitos como seus cenários de teste, mas também ajuda os analistas de negócios ou o gerente de produto a ajustar facilmente os dados de teste. Aqui está uma demonstração com um pequeno ajuste:

```
1 As an Admin User,
2 I would like to change the password of other user's accounts.
3            
4 Feature: Update password
5   Scenario: Admin user can update the user password
6     Given I am in the HR system with an Admin account
7     When I update password of another user
8     Then I receive a message for updating password successfully
9     And user's password is updated to the new password
```

O teste de automação escrito no framework do Cucumber:

```
1  Scenario Outline: Verify Updating user password feature
2    Given I am in the HR system with "<account_type>" account
3    And there is another user with "<old_password>" password
4    When I update password of the user to "<new_password>"
5    Then I got the message "<message>"
6    And the user password should be "<final_password>"
7 
8  Examples:
9  |account_type  |old_password  |new_password |message                |final_password |
10 |Admin     	|$Test123      |@Test123 	|Password changed.. 	|@Test123   	|
11 |Viewer        |$Test123      |@Test123 	|Invalid right access.. |$Test123   	|
```

## Todos os testadores podem participar do teste de automação com Cucumber

Além de melhorar a comunicação entre os membros de um mesmo time de testes, o Cucumber também ajuda a aproveitar as habilidades do testador com eficiência. A lacuna de conhecimento sempre existe em todas as empresas. Em outras palavras, existem alguns testadores que possuem alta especialização técnica em programação utilizando testes automatizados, enquanto outros realizam testes manuais com habilidades de programação limitadas - e tudo isso na mesma equipe. Graças ao Cucumber, todos os testadores, independentemente de seus níveis de habilidade, podem participar do processo de execução dos testes de automação.

Vamos dar uma olhada no exemplo acima:

- Qualquer testador que esteja ciente das regras de negócio e do fluxo de trabalho pode escrever arquivos de funcionalidades, adicionar mais cenários e testar conjuntos de dados;
- Qualquer testador que tenha um conhecimento básico de programação e saiba como criar objetos, acessar propriedades e chamar métodos, pode gerar definições de etapas;
- Qualquer testador com nível de habilidade de programação mais alto pode participar do processo de criação de um framework, definir a conexão da fonte de dados e assim por diante.

Porém, ainda existem alguns problemas potenciais ao implementar o Cucumber:

- O Cucumber ajuda a executar cenários de teste específicos em um arquivo de texto simples usando o conhecimento do domínio de negócio. Assim, o uso de linguagens e a percepção de quem cria o teste pode influenciar diretamente os cenários de teste, levando ao risco de mal-entendidos. Os cenários de teste devem ser apresentados com clareza e sua implementação deve ser realizada com precisão para cada passo. Por exemplo, quando quiser verificar a funcionalidade de pesquisa do Google, o teste deveria ser: 

```
1 Scenario: performing a search on google
2 Given I am on "www.google.com" site
3 When I search for "Cucumber and BDD"
4 Then ...
```

Esses passos podem ser incorporados para se obter o seguinte teste:

```
1 Scenario: performing a search on google
2 When I search for "Cucumber and BDD"
3 Then ...
```

Os estágios do Cucumber são executados em uma linguagem comum. E podem ser usados novamente em vários cenários de teste. Isso ajuda a reduzir o esforço para criar testes. No entanto, manter o teste legível e reutilizável é realmente um grande desafio. Se o teste for escrito em um nível muito alto para qualquer stakeholder; poucos passos poderão ser reutilizados. Ambos os scripts acima estão corretos; no entanto, o segundo não é aparente porque faz muito mais do que o esperado: abre o site do Google e pesquisa com o texto especificado. Imagine que queira estender o teste para pesquisar mais textos, e provavelmente repetirá o mesmo passo acima para isso, consequentemente, o site do Google estará aberto duas vezes. Se o requisito não for seguido rigorosamente, a ferramenta de teste do Cucumber causará mal-entendidos mais cedo ou mais tarde, e será difícil de manter quando for estendido.

```
1 Feature: Update password
2   Scenario: Admin user can update the user password
3     Given I am in the HR system with an Admin account
4     When I update password of another user
5     Then I receive a message for updating password successfully
6     And user's password is updated to the new password
7 
8   Scenario: Viewer user cannot update the user password
9     Given I am in the HR system with a Viewer account
10  	When I update password of another user
11  	Then I receive a message for not able to update the user password
12  	And user's password remains the same
```

Por outro lado, se o teste for genérico e puder ser reutilizado, por exemplo, verificar o sobrenome do usuário de atualização, os stakeholders não-técnicos terão dificuldade em entendê-lo e executar testes de aceitação:

```
1 Scenario: Admin user can update user password:
2   Given I am in the "$System.HR_Page" with "admin@test.com" username
3 and "$Test123" password
4   And there is another user in "$System.HR_Page" with "user@test.com"
5 username and "$Test123" password
6   When I update "$UserTemplate.Password" of "user@test.com" user to"@Test123"
7   And I save the response message as "response_message"
8   Then "$response_message" should be "Password changed successfully"
9   And the  "user@test.com" user's "$UserTemplate.Password" should be"@Test123"
```

Durante o processo de teste, deve-se ajustar os cenários de teste regularmente até que alcancem um equilíbrio aceitável completamente, no qual todos os membros possam entender e reutilizar.

```
1 Scenario: Verify Updating user password feature
2   Given I am in the HR system with "Admin" account
3   And there is another user with "$Test123" password
4   When I update password of the user to "@Test123"
5   Then I got the message "Password changed successfully."
6   And the user password should be "@Test123"
```

Ou com mais alguns dados de teste:

```
1 Scenario Outline: Verify Updating user password feature
2    Given I am in the HR system with "<account_type>" account
3    And there is another user with "<old_password>" password
4    When I update password of the user to "<new_password>"
5    Then I got the message "<message>"
6    And the user password should be "<final_password>"
7 
8 Examples:
9   |account_type |old_password |new_password |message       	|final_password |
10  |Admin        |$Test123 	|@Test123 	|Password changed.. 	|@Test123  |
11  |Viewer   	|$Test123 	|@Test123 	|Invalid right access.. |$Test123  |
```

## Notas importantes para o time de testes que deseja começar com o Cucumber

- Considere os testes de automação sendo essenciais como qualquer outro projeto real. O código deve seguir a boas práticas de codificação, convenções, etc.
- Deve ser considerada uma ferramenta de edição apropriada. Este editor deve ajudar a depurar e editar arquivos de funcionalidades no formato de texto padrão. O Aptana (editor gratuito), o RubyMine (editor pago) e o [Katalon Studio](https://www.katalon.com/) são opções adequadas que suportam completamente o Cucumber baseado em BDD.
- Por último, mas não menos importante, torne os arquivos de funcionalidades uma camada de "comunicação" real, na qual se pode armazenar dados de testes recebidos e formatar dados de teste. O domínio das regras de negócio não está contido.

Para concluir, oferecendo a camada de comunicação real sobre um framework de teste robusto, o Cucumber não apenas pode executar testes de automação em uma ampla demanda de testes do backend ao frontend, mas também criar conexões profundas entre os membros dos times de teste. Esse recurso dificilmente é encontrado em outros frameworks de teste. Com muitos anos de experiência na área de criação e aplicação de testes de automação, sugiro que o Cucumber para testes de Web UI e Web services seja aplicado a projetos de software Ágeis. Usar o BDD baseado em Cucumber com um editor coerente é uma escolha acertada que pode ajudar significativamente a reduzir o esforço para executar testes de regressão.

#### Conteúdo publicado no tópico [Cloud Computing](https://www.infoq.com/br/cloud-computing/)

SEGUIR TÓPICO

##### Tópicos Relacionados:

- DESENVOLVIMENTO
- CLOUD COMPUTING
- CONTINUOUS DELIVERY
- DESENVOLVIMENTO ÁGIL
- TÉCNICAS ÁGEIS
- TESTES AUTOMATIZADOS
- BDD
- AGILE
- CUCUMBER

- #### CONTEÚDO EDITORIAL RELACIONADO

  - ##### [Entendendo Os Valores e Princípios Ágeis](https://www.infoq.com/br/minibooks/valores-principios-ageis/?itm_source=infoq&itm_medium=related_content_link&itm_campaign=relatedContent_articles_clk)

  - ##### [Adquira leads qualificados no mercado de desenvolvimento de software com a eMag InfoQ](https://www.infoq.com/br/news/2021/12/emag-sponsor/?itm_source=infoq&itm_medium=related_content_link&itm_campaign=relatedContent_articles_clk)

  - ##### [O último conteúdo do InfoQ Brasil](https://www.infoq.com/br/news/2021/02/ultimo-conteudo-do-infoq-brasil/?itm_source=infoq&itm_medium=related_content_link&itm_campaign=relatedContent_articles_clk)

  - ##### [O fim do Privacy Shield pode levar a um desastre para os provedores de nuvem em hiperescala](https://www.infoq.com/br/articles/privacy-shield-hyperscale-clouds/?itm_source=infoq&itm_medium=related_content_link&itm_campaign=relatedContent_articles_clk)

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

## 