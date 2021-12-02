

# Teste end-to-end

![Cedro Technologies](https://blog.cedrotech.com/hs-fs/hubfs/apple-icon-180x180.png?width=45&name=apple-icon-180x180.png)



![img](https://blog.cedrotech.com/hubfs/Imported_Blog_Media/Teste-end-to-end.jpg)

O teste end-to-end é uma metodologia utilizada para testar se o fluxo de um aplicativo está sendo executado conforme o projeto do início ao fim. O objetivo da realização de testes end-to-end é identificar dependências do sistema e garantir que a informação certa seja passada entre vários componentes e sistemas do sistema.Resumindo, o teste end-to-end é um forma de realizar testes nas quais visam provar o sistema de uma forma mais completa simulando o ambiente real. Exemplo de tarefas comuns a serem realizadas são: acessar um banco de dados, usar uma rede comunicação e interagir com outros hardwares ou sistema.Por exemplo, um teste simplificado de end-to-end de um aplicativo de email pode envolver:Iniciando uma sessão no aplicativo;Acessando a caixa de entrada;Abrir e fechar a caixa de corre;Composição, encaminhamento ou respostas ao e-mail;Verificando os itens enviados;Como sair do aplicativo.Automação de teste end-to-end com NightwatchO Nightwatch.js é uma solução de teste end-to-end fácil baseado no Node.js voltado para aplicativos e sites baseados em browser.Neste exemplo iremos criar um breve teste de demonstração na página do Google. Para iniciarmos, é necessário ter instalado o Node.js e o Java na sua máquina para a execução do Selenium.Crie uma nova pasta para iniciarmos o teste, chamada de “2e2”, depois inicie o Node.js com o comando:[![img](https://blog.cedrotech.com/hs-fs/hubfs/Imported_Blog_Media/18_05_-4.png?width=218&height=19&name=18_05_-4.png)](https://f.hubspotusercontent30.net/hubfs/8797985/Imported_Blog_Media/18_05_-4.png)[![Teste end-to-end](https://blog.cedrotech.com/hs-fs/hubfs/Imported_Blog_Media/18_05_-6.png?width=596&height=620&name=18_05_-6.png)](https://f.hubspotusercontent30.net/hubfs/8797985/Imported_Blog_Media/18_05_-6.png)

Preencha os campos se for necessário e aperte enter até a mensagem de confirmação aparecer.Agora iremos instalar o Nightwatch.js através do comando:[![Teste end-to-end](https://blog.cedrotech.com/hs-fs/hubfs/Imported_Blog_Media/18_05_-5.png?width=221&height=20&name=18_05_-5.png)](https://f.hubspotusercontent30.net/hubfs/8797985/Imported_Blog_Media/18_05_-5.png)Após a instalação, criaremos um novo arquivo chamado “nightwatch.json”, onde será nosso arquivo de configuração.[![img](https://blog.cedrotech.com/hs-fs/hubfs/Imported_Blog_Media/18_05_-8.png?width=372&height=747&name=18_05_-8.png)](https://f.hubspotusercontent30.net/hubfs/8797985/Imported_Blog_Media/18_05_-8.png)Agora criaremos uma nova pasta na raiz do nosso projeto chamada “bin”, nela iremos salvar as ferramentas de configuração.O próximo passo é realizar o download do [Selenium Server](http://selenium-release.storage.googleapis.com/index.html). Após realizar o download salve na pasta “bin”.Neste exemplo iremos mostrar como realizar o teste com os web drivers [GoogleDriver](https://chromedriver.storage.googleapis.com/index.html?path=2.37/) (ficará ao seu critério escolher qual browser driver será trabalhado) e o [GeckoDriver](https://github.com/mozilla/geckodriver/releases). Faça o download acessando os links abaixo e salve na pasta “bin”.Vamos configurar nosso arquivo de configuração conforme a figura abaixo:[![Teste end-to-end](https://blog.cedrotech.com/hs-fs/hubfs/Imported_Blog_Media/18_05_-7.png?width=437&height=160&name=18_05_-7.png)](https://f.hubspotusercontent30.net/hubfs/8797985/Imported_Blog_Media/18_05_-7.png)Em “start_process” define como true, em “server_path” será o caminho no qual o selenium server está salvo, “cli_args” são as configurações de qual webdriver será usado.
Com o nosso arquivo de configuração organizado iremos criar uma nova pasta chamada “tests”, na raiz do no nosso projeto. A pasta deve ser nomeada conforme está configurado no nightwatch.json, como mostra a figura abaixo:[![Teste end-to-end](https://blog.cedrotech.com/hs-fs/hubfs/Imported_Blog_Media/18_05_-2.png?width=238&height=74&name=18_05_-2.png)](https://f.hubspotusercontent30.net/hubfs/8797985/Imported_Blog_Media/18_05_-2.png)Criada a pasta, agora um novo arquivo chamado “demo.js” será criado e o script abaixo será implementado.[![Teste end-to-end](https://blog.cedrotech.com/hs-fs/hubfs/Imported_Blog_Media/18_05_-1.png?width=520&height=251&name=18_05_-1.png)](https://f.hubspotusercontent30.net/hubfs/8797985/Imported_Blog_Media/18_05_-1.png)Com todo o processo feito iremos executar o nosso teste. Abra o terminal e navegue até a raiz do projeto e execute o comando.`.\node_modules\.bin\nightwatch`Espere os testes serem realizados e o resultado será concluído no terminal como na figura abaixo:[![Teste end-to-end](https://blog.cedrotech.com/hs-fs/hubfs/Imported_Blog_Media/18_05_-3.png?width=409&height=170&name=18_05_-3.png)](https://f.hubspotusercontent30.net/hubfs/8797985/Imported_Blog_Media/18_05_-3.png)

![Cedro Technologies](https://blog.cedrotech.com/hs-fs/hubfs/apple-icon-180x180.png?width=150&name=apple-icon-180x180.png)

### 

## Artigos relacionados 

[![img](https://blog.cedrotech.com/hubfs/Imported_Blog_Media/como-deve-ser-feito-um-teste-de-software-ideal-1.jpg)](https://blog.cedrotech.com/entenda-como-deve-ser-feito-um-teste-de-software-ideal)

### [Entenda como deve ser feito um teste de software ideal](https://blog.cedrotech.com/entenda-como-deve-ser-feito-um-teste-de-software-ideal)

[SAIBA MAIS](https://blog.cedrotech.com/entenda-como-deve-ser-feito-um-teste-de-software-ideal)

[![img](https://blog.cedrotech.com/hubfs/Imported_Blog_Media/signalr.jpg)](https://blog.cedrotech.com/novas-versoes-do-signalr-e-asp-net)

### [Conhecendo as novas versões do SignalR e Asp.Net](https://blog.cedrotech.com/novas-versoes-do-signalr-e-asp-net)

[SAIBA MAIS](https://blog.cedrotech.com/novas-versoes-do-signalr-e-asp-net)

### [Localizar endereços por CPF](https://blog.cedrotech.com/localizar-enderecos-por-cpf)

[SAIBA MAIS](https://blog.cedrotech.com/localizar-enderecos-por-cpf)