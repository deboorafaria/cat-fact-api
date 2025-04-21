# cat-fact-api

1. ##   **Objetivo da Documentação**

Esta documentação tem como propósito registrar os os cenários de testes realizados na API pública **Cat Fact** utilizando o Postman. Ao longo deste material, serão apresentados os limites máximos e mínimos dos parâmetros aceitos, além de orientações detalhadas sobre como configurá-los corretamente para efetuar as requisições.

Adicionalmente, serão descritos os cenários de testes desenvolvidos, oferecendo uma visão abrangente do comportamento da API em diferentes condições.

2. ## **Sobre a Cat Fact API**

A Cat Fact API é uma API pública de gerenciamento de fatos sobre gatos, basicamente é um serviço que pode ser usado para coletar automaticamente fatos aleatórios sobre gatos, para aprender mais sobre felinos ou simplesmente se divertir.

Desenvolvedores podem integrar essa API em suas aplicações para fornecer conteúdo interessante e divertido aos seus usuários.

Os fatos disponíveis variam conforme o tipo de busca realizada. O usuário pode optar por fazer uma requisição para obter toda a listagem de fatos sobre gatos, solicitar um fato aleatório por vez, ou explorar informações detalhadas sobre as raças de gatos. Nessa última opção, é possível descobrir dados como o país de origem, o tipo de pelagem e a cor padrão dessa pelagem.

Além disso, a API oferece filtros úteis, permitindo ao usuário ajustar o tamanho máximo de caracteres dos fatos retornados ou limitar a quantidade de fatos e raças exibidos nos resultados.

3. ## **Como importar um arquivo de coleções do teste do postman**

   ### **1\. Importar o Arquivo no Postman**

* Abra o Postman.  
* Clique no botão **"Import"** no canto superior esquerdo.  
* Escolha o arquivo que deseja importar, neste caso o formato utilizado é um JSON.
* [Collection para importação](https://github.com/deboorafaria/cat-fact-api/blob/main/Cat%20Fact%20API.postman_collection.json)
* Arraste o arquivo para a janela de importação ou clique em **"Upload Files"** para selecioná-lo do seu computador.  
* Após a importação, a coleção aparecerá na barra lateral esquerda.

  ### **2\. Configurar a Coleção**

* Clique na coleção importada para visualizar as requisições.

  ### **3\. Executar a Coleção com o Runner**

* Clique no ícone “...” ao lado do nome da coleção importada.  
* Abrirá um pequeno menu e clique em ‘Run’  
* Na janela do Runner, selecione a coleção que deseja executar.  
* Escolha o ambiente (se aplicável) e configure os parâmetros, como número de iterações ou arquivos de dados (se estiver usando dados externos).  
* Clique em **"Run"** para iniciar a execução.

  ### **4\. Visualizar os Resultados**

* Após a execução, o Postman exibirá os resultados de cada requisição, incluindo status, tempo de resposta e dados retornados.  
* Você pode exportar os resultados para análise posterior.

![Gif Import Collection Postam ](https://github.com/user-attachments/assets/cc506066-d951-4dc9-a756-070c4e0899d7)


4. ## **Mapeamento dos testes** 

   1. # Fact

Busca por fatos aleatórios.

| Requisição |  |
| :---: | :---: |
| URL | Autenticação **por Requisição:** [`https://catfact.ninja/fact`](https://catfact.ninja/fact)  |
| Método | GET |

| Params |  |  |  |  |
| :---: | :---: | ----- | ----- | :---: |
| **Name** | **Type** | **Value** | **Description** | **Obrigatório** |
| Params | `'max_length'` | `Do tipo inteiro` | Tamanho máximo do fato retornado | **Não** |

1. #### **Cenário de teste**

##### **CT01 \-  Obter um fato aleatório sobre gatos**

* **Dado** **que** o usuário tenha acesso à API   
  * **E** tenha o endpoint `https://catfact.ninja/fact`   
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
* **Então** a requisição será enviada com sucesso  
  * **E** o sistema retornará uma resposta no formato JSON contendo fatos aleatórios sobre gatos  
  * **E** o código de status da resposta será `200 - OK`.

##### **CT02:  Obter um fato aleatório sobre gatos com parâmetro `‘max_length'` com valor igual a `vazio`**

* **Dado** **que** o usuário tenha acesso à API   
  * **E** tenha o endpoint `https://catfact.ninja/fact`   
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `‘max_length'`  
* **Então** a requisição será enviada com sucesso  
  * **E** o sistema retornará uma resposta no formato JSON contendo uma lista de fatos aleatório sobre gatos contendo no máximo o valor estimado de caracteres.   
  * **E** o código de status da resposta será `200 - OK`.

##### **CT03:  Obter um fato aleatório sobre gatos com parâmetro `‘max_length'` com  valor igual a `zero (0)`**

* **Dado** **que** o usuário tenha acesso à API   
  * **E** tenha o endpoint `https://catfact.ninja/fact`   
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro   
  * **E** inserir um `value = 0`  
* **Então** a requisição será enviada com sucesso  
  * **E** o sistema listará uma resposta no formato JSON contendo a estrutura de dados do tipo `‘data’` como vazio  
  * **E** o código de status da resposta será `200 - OK`.

##### **CT04: No campo `‘max_length'` informar um valor do tipo `número inteiro`** 

* **Dado que** o usuário tenha acesso à API   
  * **E** tenha o endpoint `https://catfact.ninja/fact`   
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado   
  * **E** adicionar o parâmetro `'max_length'`   
  * **E** inserir um `value` \= *\[inserir um número inteiro positivo, ex: 35\]*  
*  **Então** a requisição será enviada com sucesso   
  * **E** o código de status da resposta será `200 - OK`   
  * **E** o sistema retornará uma resposta no formato JSON contendo uma lista de fatos aleatórios sobre gatos, contendo a estrutura de dados do tipo `‘fact’` com uma string de tamanho menor ou igual a *\[o número inteiro inserido\].*  
  * **E** o campo `‘length’` terá um valor numérico menor ou igual a *\[o número inteiro inserido\].*

##### **CT05: Obter um fato aleatório sobre gatos com params `'max_length'` com valor string** 

* **Dado que** o usuário tenha acesso à API   
  * **E** tenha o endpoint `https://catfact.ninja/fact`   
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado   
  * **E** adicionar o parâmetro `'max_length'`  
  * **E** inserir um value \= *\[inserir uma string, ex: abc\]*   
* **Então** a requisição será enviada com falha   
  * **E** o código de status da resposta será `400 - Bad Request`   
  * **E** o sistema retornará uma resposta no formato JSON contendo uma mensagem de erro indicando que o parâmetro `‘max_length'` deve ser um número inteiro válido.

| Descrição do teste realizado |  |
| ----- | ----- |
| **Resultado Esperado:**  De acordo com a documentação fornecida, o parâmetro `‘max_length’` aceita apenas números inteiros. Portanto, o comportamento esperado para essa requisição seria o retorno de um código `400 - Bad Request`, pois o retorno seria vazio. |  |
| **Resultado obtido:** Foi realizado um teste utilizando o Postman com a seguinte requisição: `https://catfact.ninja/facts?max_length=dbr` com o retorno `200 - Ok` e foi apresentado uma lista de fatos aleatórios com tamanhos variados. |  |
| **Teste Adicional:**  Para confirmar o comportamento, o teste foi executado diretamente na documentação da API. O retorno foi a seguinte mensagem de erro: *“Corrija os seguintes erros de validação e tente novamente. Para 'max\_length': O valor deve ser um número inteiro.” O resultado da busca seria vazio.*  |  |
| **Documentação API**![imagem 2](https://github.com/user-attachments/assets/53935d60-3f12-4dce-b8df-45135727d0d2)
  |  |

##### **CT06: Obter um fato aleatório sobre gatos com parâmetro `‘max_length'` com valor `negativo`** 

1. **Dado que** o usuário tenha acesso à API   
   * **E** tenha o endpoint `https://catfact.ninja/fact`   
2. **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado   
   * **E** adicionar o parâmetro `'max_length'`  
   * **E** inserir um `value` \= *\[inserir um número inteiro negativo, ex: \-5\]*   
3. **Então** a requisição será enviada com sucesso  
   * **E** o código de status da resposta será  `200 - OK`    
   * **E** o sistema retornará uma resposta no formato JSON vazio.Get a list of facts

   2. ### **Facts**

Busca por lista de fatos de gatos de forma aleatórias 

| Requisição |  |
| :---: | :---: |
| URL | Autenticação **por Requisição**: [`https://catfact.ninja/fact`](https://catfact.ninja/fact)`s`  |
| Método | GET |

| Params |  |  |  |  |
| :---: | :---: | ----- | ----- | :---: |
| **Name** | **Type** | **Value** | **Description** | **Obrigatório** |
| Params | `''max_length'` | `Do tipo inteiro` | Duração máxima do fato retornado | **Não** |
|  | `‘limit’` | `Do tipo inteiro` | Limitar a quantidade de resultados retornados  | **Não** |

1. #### **Cenário de teste**

##### **CT01 \- Obter um fato aleatório sobre gatos com parâmetro `‘max_length’` com valor `negativo`**

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/facts`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `'max_length'`  
  * **E** inserir um `value = -5`  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será  `200 - OK`    
  * **E** o sistema retornará uma resposta no formato JSON vazio..

##### **CT02 \- Obter um fato aleatório sobre gatos com parâmetro `‘max_length’` com valor `zero`**

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/facts`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `'max_length'`  
  * **E** inserir um `value = 0`  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será `200 - OK`  
  * **E** o sistema retornará uma resposta no formato JSON contendo a estrutura de dados do tipo `‘fact’` com uma string vazia  
  * **E** o campo `‘length’` terá o valor 0\.

##### **CT03 \-  Obter um fato aleatório sobre gatos com parâmetro `‘max_length’` com valor `inteiro`** 

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/facts`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `'max_length'`  
  * **E** inserir um `value = 150`  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será `200 - OK`  
  * **E** o sistema retornará uma resposta no formato JSON contendo a estrutura de dados do tipo `‘fact’` com uma string de tamanho menor ou igual a 150  
  * **E** o campo `‘length’` terá um valor numérico menor ou igual a 150\.

##### **CT04 \- Obter um fato aleatório sobre gatos com parâmetro `‘max_length’` com valor do tipo `string`**

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/facts`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `'max_length'`  
  * **E** inserir um `value = "texto"`  
* **Então** a requisição será enviada com sucesso  
  * **E** o sistema listará uma resposta no formato JSON contendo a estrutura de dados do tipo `‘data’` como vazio  
  * **E** o código de status da resposta será `200 - OK`.

##### **CT05 \- Obter múltiplos fatos aleatórios sobre gatos com parâmetro `‘limit’` com valor `inteiro`** 

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/facts`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `'limit'`  
  * **E** inserir um `value = 3`  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será `200 - OK`  
  * **E** o sistema retornará uma resposta no formato JSON contendo uma estrutura de dados do tipo `‘data’` com uma lista com 3 objetos  
  * **E** cada fato dentro dessa lista conterá os campos `‘fact’` (string não vazia) e `‘length’` (número inteiro positivo).

##### **CT06-  Obter múltiplos fatos aleatórios sobre gatos com parâmetro `‘limit’` com valor `zero`**

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/facts`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `'limit'`  
  * **E** inserir um `value = 0`  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será `200 - OK`  
  * **E** o sistema retornará uma resposta no formato JSON contendo uma estrutura de dados do tipo `‘data’` retornará uma lista vazia.

##### **CT07 \- Obter múltiplos fatos aleatórios sobre gatos com parâmetro `‘limit’` com valor `negativo`**

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/facts`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `'limit'`  
  * **E** inserir um `value = -2`  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será `200 - OK`  
  * **E** o sistema retornará uma resposta no formato JSON contendo uma estrutura de dados do tipo `‘data’` retornará uma lista vazia.

##### **CT08 \- Obter múltiplos fatos aleatórios sobre gatos com parâmetro `‘limit’` com valor do tipo `string`**

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/facts`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `'limit'`  
  * **E** inserir um `value = "DBR"`  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será `200 - OK`  
  * **E** o sistema retornará uma resposta no formato JSON contendo uma estrutura de dados do tipo `‘data’` retornará uma lista vazia.

##### **CT09 \-  Obter um fato aleatório sobre gatos com parâmetro `‘max_length’` `vazio`**

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/facts`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `'max_length'`  
  * **E** inserir um `value = ""` *(string vazia)*  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será `200 - OK`  
  * **E** o sistema retornará uma resposta no formato JSON contendo a estrutura de dados do tipo `‘fact’` com uma string de tamanho qualquer  
  * **E** o campo `‘length’` terá um valor numérico correspondente ao tamanho do fato retornado**.**

##### **CT10: Obter múltiplos fatos aleatórios sobre gatos com parâmetro `‘limit’` `vazio`** 

* **Dado que** o usuário tenha acesso à API   
  * **E** tenha o endpoint `https://catfact.ninja/facts`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado   
  * **E** adicionar o parâmetro `'limit'` E inserir um `value = ""` *(string vazia)*   
* **Então** a requisição será enviada com sucesso   
  * **E** o código de status da resposta será `200 - OK`   
  * **E** o sistema retornará uma resposta no formato JSON contendo uma estrutura de dados do tipo `‘data’` uma lista com a quantidade padrão de resultados *(se houver um padrão definido pela API)*   
  * **E** contendo a estrutura de dados do tipo `‘data’` terá os campos `‘fact’` *(string não vazia)* e `‘length’` *(número inteiro positivo).*

##### **CT11 \- Obter fatos aleatórios com max\_length inteiro e limit inteiro**

* Dado que: O usuário tem acesso à API e ao endpoint `https://catfact.ninja/facts`  
* Quando: O usuário realiza uma requisição HTTP GET para o endpoint, e adiciona os parâmetros `max_length` \= 100 e `limit` \= 5  
* Então a requisição é enviada com sucesso.  
  * E o código de status da resposta é **200 \- OK.**  
  * E o sistema retorna uma resposta no formato JSON contendo uma lista de 5 fatos.  
  * E cada fato na lista tem no máximo 100 caracteres no campo `fact`.  
  * E cada fato na lista tem um valor de `length` menor ou igual a 100\.

##### **CT12 \- Obter fatos com max\_length negativo e limit inteiro**

* Dado que: O usuário tem acesso à API e ao endpoint `https://catfact.ninja/facts`  
* Quando: O usuário realiza uma requisição HTTP GET para o endpoint, e adiciona os parâmetros `max_length` \= \-10 e `limit` \= 5  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será `200 - OK`  
  * **E** o sistema retornará uma resposta no formato JSON contendo uma estrutura de dados do tipo `‘data’` retornará uma lista vazia.

##### **CT13 \- Obter fatos com max\_length inteiro e limit negativo**

* Dado que: O usuário tem acesso à API e ao endpoint `https://catfact.ninja/facts`  
* Quando: O usuário realiza uma requisição HTTP GET para o endpoint, e adiciona os parâmetros `max_length` \= 100 e `limit` \= \-5  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será `200 - OK`  
  * **E** o sistema retornará uma resposta no formato JSON contendo a estrutura de dados do tipo `‘fact’` com uma string de tamanho qualquer  
  * **E** o campo `‘length’` terá um valor numérico correspondente ao tamanho do fato retornado**.**  
  * **E** o limite de fatos retornados será o valor padrão (10)

##### **CT14 \- Obter fatos com max\_length negativo e limit negativo**

* Dado que: O usuário tem acesso à API e ao endpoint `https://catfact.ninja/facts`  
* Quando: O usuário realiza uma requisição HTTP GET para o endpoint, e adiciona os parâmetros `max_length` \= \-10 e `limit` \= \-5  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será `200 - OK`  
  * **E** o sistema retornará uma resposta no formato JSON contendo uma estrutura de dados do tipo `‘data’` retornará uma lista vazia.

##### **CT15 \- Obter fatos com max\_length inteiro e limit vazio**

* Dado que: O usuário tem acesso à API e ao endpoint `https://catfact.ninja/facts`  
* Quando: O usuário realiza uma requisição HTTP GET para o endpoint, e adiciona os parâmetros `max_length` \= 100 e `limit` \= ""  
* Então:  
  * A requisição é enviada com sucesso.  
  * O código de status da resposta é **200 \- OK.**  
  * O sistema retorna uma resposta no formato JSON contendo uma lista de fatos (a quantidade padrão de resultados da API).  
  * Cada fato na lista tem no máximo 100 caracteres no campo `fact`.  
  * Cada fato na lista tem um valor de `length` menor ou igual a 100\.

##### **CT16 \- Obter fatos com max\_length vazio e limit inteiro**

* Dado que: O usuário tem acesso à API e ao endpoint `https://catfact.ninja/facts`  
* Quando: O usuário realiza uma requisição HTTP GET para o endpoint, e adiciona os parâmetros `max_length` \= "" e `limit` \= 5  
* Então:  
  * A requisição é enviada com sucesso.  
  * O código de status da resposta é **200 \- OK.**  
  * O sistema retorna uma resposta no formato JSON contendo uma lista de 5 fatos.  
  * Os fatos na lista podem ter qualquer tamanho.

##### **CT17 \- Obter fatos com max\_length vazio e limit vazio**

* Dado que: O usuário tem acesso à API e ao endpoint `https://catfact.ninja/facts`  
* Quando: O usuário realiza uma requisição HTTP GET para o endpoint, e adiciona os parâmetros `max_length` \= "" e `limit` \= ""  
* Então:  
  * A requisição é enviada com sucesso.  
  * O código de status da resposta é **200 \- OK.**  
  * O sistema retorna uma resposta no formato JSON contendo uma lista de fatos (a quantidade padrão de resultados da API).  
  * Os fatos na lista podem ter qualquer tamanho.

  3. ### **Breeds**

Busca por lista de fatos.

| Requisição |  |
| :---: | :---: |
| URL | Autenticação **por Requisição:** `https://catfact.ninja/breeds`  |
| Método | GET |

| Params |  |  |  |  |
| :---: | :---: | ----- | ----- | :---: |
| **Name** | **Type** | **Value** | **Description** | **Obrigatório** |
| **Params** | `‘limit’` | `Do tipo inteiro` | Limitar a quantidade de resultados retornados  | **Não** |

1. #### **Cenário de teste**

##### **CT01 \- Obter a lista de raças de gatos sem o parâmetro `‘limit’`**

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/breeds`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será `200 - OK`  
  * **E** o sistema retornará uma resposta no formato JSON contendo uma lista de todas as raças de gatos disponíveis  
  * **E** cada item nessa lista terá informações sobre a raça, como `‘breed’`, `‘country’`, `‘origin’, ‘coat’, ‘pattern’`.

##### **CT02 \- Obter a lista de raças de gatos com parâmetro ‘limit’ com valor inteiro positivo**

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/breeds`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `'limit'`  
  * **E** inserir um `value = 5`  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será `200 - OK`  
  * **E** o sistema retornará uma resposta no formato JSON contendo uma lista de 5 raças de gatos  
  * **E** cada item nessa lista terá informações sobre a raça, como `‘breed’`, `‘country’`, `‘origin’`, `‘coat’`, `‘pattern’`.

##### **CT03 \- Obter a lista de raças de gatos com parâmetro ‘limit’ com valor zero**

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/breeds`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `'limit'`  
  * **E** inserir um `value = 0`  
* **Então** a requisição será enviada com sucesso  
* **E** o código de status da resposta será `200 - OK`  
* **E** o sistema retornará uma resposta no formato JSON contendo uma lista vazia de raças de gatos.

##### **CT04 \- Obter a lista de raças de gatos com parâmetro `‘limit’` com valor `negativo`**

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/breeds`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `'limit'`  
  * **E** inserir um `value = -3`  
* **Então** a requisição será enviada com falha  
  * **E** o código de status da resposta será  `404 - Not Found`  
  * **E** o sistema retornará uma resposta no formato JSON contendo uma mensagem de erro;

**CT05 \- Obter a lista de raças de gatos com parâmetro** `‘limit’` **com valor do tipo** `string`

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/breeds`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `'limit'`  
  * **E** inserir um `value = "dois"`  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será `200 - OK`  
  * **E** o sistema retornará uma resposta no formato JSON contendo uma lista de raças de gatos.

##### **CT06 \- Obter a lista de raças de gatos com parâmetro `‘limit’` `vazio`**

* **Dado que** o usuário tenha acesso à API  
  * **E** tenha o endpoint `https://catfact.ninja/breeds`  
* **Quando** o usuário realizar uma requisição HTTP utilizando o método GET no endpoint mencionado  
  * **E** adicionar o parâmetro `'limit'`  
  * **E** inserir um `value = ""` *(texto vazio)*  
* **Então** a requisição será enviada com sucesso  
  * **E** o código de status da resposta será `200 - OK`  
  * **E** o sistema retornará uma resposta no formato JSON contendo uma lista de todas as raças de gatos disponíveis *(comportamento padrão).*

[image1]: <data:image/png;base64,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>

[image2]: <data:image/png;base64,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>

## **Relatório de Testes**

[Relatório de Testes](https://github.com/deboorafaria/cat-fact-api/blob/main/%F0%9F%A7%AA%20Relat%C3%B3rio%20de%20Testes%20%E2%80%93%20Cat%20Fact%20API.md)
