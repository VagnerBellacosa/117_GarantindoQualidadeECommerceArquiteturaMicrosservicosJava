##### Rest assured Teste de integração

Vamos lá! se você se deparou com alguns desse erros ao tentar implementar teste de integração com Rest assured..

```
  out of START_OBJECT token
  com.fasterxml.jackson.databind.exc.MismatchedInputException: Cannot deserialize instance of
  java.net.ConnectException: Connection refused: connect
```

Todos foram resolvidos aqui!!

Antes de começar, vamos usar como base o projeto que foi criado [nesse post](http://www.davifelipe.com.br/backend-spring-boot-rest-json).

Primeiramente vamos adicionar a dependência no pom.xml

```
          <dependency>
              <groupId>io.rest-assured</groupId>
              <artifactId>rest-assured</artifactId>
              <version>3.3.0</version>
              <scope>test</scope>
          </dependency>
```

 

Antes de implementar o teste, vamos fazer uma alteração no resocurce para retornar uma lista de objetos Product ao invés de retornar o objeto diretamente:

```
  package com.br.davifelipe.springjwt.resources;
 import java.math.BigDecimal;
  import java.util.ArrayList;
  import java.util.List;
 import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RequestMapping;
  import org.springframework.web.bind.annotation.RestController;
 import com.br.davifelipe.springjwt.model.Product;
 @RestController
  @RequestMapping("/products")
  public class ProductResoruce {
      
      @GetMapping("/test")
      public List<Product> test() {
          
          BigDecimal price = new BigDecimal(4.5);
          Product mouse = new Product(1, "Mouse", price);
          
          List<Product> lista = new ArrayList<Product>();
          lista.add(mouse);
          
          return lista;
      }
  }
  
```

Agora vamos criar a classe de teste em src/test/java com nome ProductResourceTest dentro de um novo pacote chamado resources

```
  package com.br.davifelipe.springjwt.resources;
 import static io.restassured.RestAssured.given;
  import static org.junit.jupiter.api.Assertions.assertEquals;
 import java.util.Arrays;
  import java.util.List;
 import org.junit.jupiter.api.Test;
  import org.springframework.boot.test.context.SpringBootTest;
  import org.springframework.boot.web.server.LocalServerPort;
 import com.br.davifelipe.springjwt.model.Product;
 @SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
  public class ProductResourceTest {
      
      @LocalServerPort
      private int port;
      
      @Test
      public void testProduct() {
          
          List<Product> products = Arrays.asList(
                                                  given()
                                                  .contentType("application/json")
                                                  .port(port)
                                                  .when().get("/products/test").then().statusCode(200)
                                                  .extract().as(Product[].class)
                                                );
          
          assertEquals("Mouse", products.get(0).getName());
     }
      
  }
  
```

Esse teste vai simular uma requisição para url /products/test, deserializar a lista de objetos para um ArrayList de Products e em seguida conferir se o nome do primeiro objeto da lista corresponde a String Mouse

Para rodar o teste pelo STS basta clicar com botão direto no pacote de testes e mandar rodar com JUnit Test

![Imagem](http://www.davifelipe.com.br/foto_conteudo/conteudo_84_img_2.JPG)

![Imagem](http://www.davifelipe.com.br/foto_conteudo/conteudo_84_img_3.JPG)

https://github.com/davifelipems/spring-backend-template/tree/integration_test