[CYPRESS](https://talkingabouttesting.com/category/cypress/)

# Usando Dado/Quando/Então sem Cucumber com Cypress

## Não se prenda ao uso do Cucumber para fazer uso das palavras-chave Dado/Quando/Então

Muita gente ainda acha que usar **Cucumber** é a solução para pessoas não técnicas começarem a escrever testes automatizados, visto que você escreve a especificação de como o software deve se comportar em uma linguagem natural e tal especificação pode ser executada para testar o sistema.

Porém, para tal linguagem natural funcionar como script de teste automatizado, precisamos de código que interprete tal linguagem (**Dado/Quanto/Então**). Ou seja, a camada de linguagem natural é um nível de abstração de alto nível, enquanto que o código que a interpreta é o “baixo nível”.

Com frequência em grupos de discussão sobre Cypress vejo pessoas pedindo ajuda com a integração do plugin do Cucumber, erros e outros problemas, os quais poderiam ser completamente evitados se o Cucumber não estivesse sendo usado em primeiro plano.

Daí você me diz: “Mas o teste fica tão legível quando uso as palavras-chave **Dado/Quando/Então**.”

E eu te respondo: “Nada te impede de continuar usando estas palavras-chave sem usar Cucumber.”

Vamos ver como?

Imaginemos um exemplo de um buscador web.

Em **BDD** (***behaviour-driven development\***) teríamos o seguinte requisito:

**Feature: Buscador web**

 Como um usuário da *world-wide web*

 Quero realizar buscas por assuntos do meu interesse

 Para aprofundar meus conhecimentos

Em Gherkin, poderíamos pensar nos seguintes cenários:

 **Cenário 1: Busca digitando um termo e clicando na lupa**

  Dado que acesso a página do buscador

  Quando digito um termo e clico na lupa

  Então vejo uma lista de resultados sobre o termo que procurei

 **Cenário 2: Busca digitando um termo e pressionando ENTER**

  Dado que acesso a página do buscador

  Quando digito um termo e pressiono ENTER

  Então vejo uma lista de resultados sobre o termo que procurei

Vejamos agora um exemplo onde cobri tais cenários com Cypress sem utilizar Cucumber, porém ao mesmo tempo, sem perder o uso das palavras-chave **Dado/Quando/Então**.

```
/* busca.spec.js
 *
 * Como um usuário da world-wide web
 * Quero realizar buscas por assuntos do meu interesse
 * Para aprofundar meus conhecimentos
 */

describe('Buscador web', () => {
  context('Dado que acesso a página do buscador', () => {
    beforeEach(() => {
      cy.visit('https://duckduckgo.com')
    })

    context('Quando digito um termo e clico na lupa', () => {
      beforeEach(() => {
        cy.get('#search_form_input_homepage')
          .type('cypress')
        cy.get('#search_button_homepage')
          .click()
      })

      it('Então vejo uma lista de resultados sobre o termo que procurei', () => {
        cy.get('.results .result')
          .should('have.length', 11)
      })
    })

    context('Quando digito um termo e pressiono ENTER', () => {
      beforeEach(() => {
        cy.get('#search_form_input_homepage')
          .type('cypress{enter}')
      })

      it('Então vejo uma lista de resultados sobre o termo que procurei', () => {
        cy.get('.results .result')
          .should('have.length', 11)
      })
    })
  })
})
```

E esse é o resultado dos testes após executá-los em modo *headless*.

```
Buscador web
  Dado que acesso a página do buscador
    Quando digito um termo e clico na lupa
      ✓ Então vejo uma lista de resultados sobre o termo que procurei (4173ms)
    Quando digito um termo e pressiono ENTER
      ✓ Então vejo uma lista de resultados sobre o termo que procurei (1973ms)
```

Ou seja, ainda tenho as palavras **Dado/Quando/Então**, meus testes continuam legíveis e não perdi um minuto sequer integrando o Cypress ao Cucumber. Fácil assim!

O código completo do exemplo acima pode ser encontrado em meu perfil no **[GitHub](https://github.com/wlsf82/cypress-sem-cucumber)**.

![no-cucumbers-allowed](https://talkingabouttesting.files.wordpress.com/2021/07/no-cucumbers-allowed.png)

------

Aproveito pra te convidar para assistir [uma live onde falei sobre o motivo por eu não usar mais Cucumber para a escrita de testes automatizados e como sou mais feliz com isso](https://youtu.be/Pk3i9sh-55M).

E uma [**talk**](https://youtu.be/zcoAWehiZzg) que fiz (em Inglês), sobre [**como escrever testes com Cypress sem Cucumber**](https://youtu.be/zcoAWehiZzg), onde fui além do usa das palavras-chave Dado/Quando/Então, mostrando também como executar um mesmo teste com base em uma lista de dados pré-definida (tais como as tabelas que o Cucumber permite usar) e como rodar testes utilizando tags, porém, **tudo sem Cucumber**. Confira no [**YouTube**](https://youtu.be/zcoAWehiZzg).

------

Ficou curioso e quer aprender mais sobre **automação de testes com Cypress**? Conheça meus cursos no [**Udemy**](https://www.udemy.com/user/walmyr/) e na [**Escola Talking About Testing**](http://talkingabouttesting.coursify.me/).