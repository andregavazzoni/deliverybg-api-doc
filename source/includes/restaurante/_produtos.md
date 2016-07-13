# Produtos

Base URL: http://bomgourmet.delivery/api

## Buscar Produto
Endpoint para buscar um único produto.

```php
<?php
    $curl = curl_init();

    curl_setopt_array($curl, array(
      CURLOPT_URL => "http://bomgourmet.delivery/api/produtos/16832?token=3f59d6f547d995f675522784f5c8c631",
      CURLOPT_RETURNTRANSFER => true,
      CURLOPT_CUSTOMREQUEST => "GET",
    ));

    $response = curl_exec($curl);
    $err = curl_error($curl);

    curl_close($curl);

    if ($err) {
      echo "cURL Error #:" . $err;
    } else {
      echo $response;
    }
?>
```

```c#
var client = new RestClient("http://bomgourmet.delivery/api/produtos/16832?token=3f59d6f547d995f675522784f5c8c631");
var request = new RestRequest(Method.GET);
IRestResponse response = client.Execute(request);
```

> Retorno:

```json
{
  "Id": 16832,
  "PlanId": 232,
  "CategoryId": 1681,
  "SizeId": null,
  "StatusId": 1,
  "Name": "Produto 1",
  "Description": null,
  "Price": "13.00",
  "Photo": null,
  "SizePrice": [
    {
      "Id": 21696,
      "ProductId": 16832,
      "SizeId": 367,
      "Price": "17.50",
      "TotalPrice": "35.00"
    }
  ]
}
```

### HTTP Request
`GET /produtos/{id}`

### Parametros

Parametro | Formato | Observação
----------|---------|------------
id        |  int    | ID do Produto
token     |  string | Token do cliente.


### Retorno

  Campo | Formato | Observação
--------|---------|-----------
Result  |  string | Identificação do Retorno. OK ou Error
Error   |  array  | Lista de erros, caso exista
Records |  array  | Lista de pedidos, conforme abaixo

### Retorno (Records)
           Campo            |      Formato      | Observação
----------------------------|-------------------|---------------------------------------
Id                          | int               | Identificador do Produto
PlanId                      | int               | Identificador do Plano
CategoryId                  | int               | Identificador da Categoria
SizeId                      | int               | Identificador do Tamanho
StatusId                    | int               | Identificador do Status (1 => Ativo, 2 => Inativo, 9 => Excluido)
Name                        | string            | Nome do produto
Description                 | string            | Descrição do produto
Price                       | float             | Preço do produto
Photo                       | string            | URL da foto do produto
SizePrice                   | Array             | Preços do produto, por tamanho


### Retorno (SizePrice)
           Campo            |      Formato      | Observação
----------------------------|-------------------|---------------------------------------
Id                          | int               | Identificador do Preço
ProductId                   | int               | Identificador do Produto
SizeId                      | int               | Identificador do Tamanho
Price                       | float             | Preço do produto, já divido pela quantidade de opções
TotalPrice                  | float             | Preço total do produto


## Criar produto
Endpoint para criar um produto.

<aside class="notice">
    O header "Location" pode ser utilizado para buscar o produto que foi criado
</aside>

```php
<?php
    $curl = curl_init();

    curl_setopt_array($curl, array(
    CURLOPT_URL => "http://bomgourmet.delivery/api/produtos/",
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_CUSTOMREQUEST => "POST",
    CURLOPT_POSTFIELDS => "Token=3f59d6f547d995f675522784f5c8c631&Name=Teste%20de%20Produto%20via%20API&CategoryId=1681&Price=10.50&SizePrice%5B0%5D%5BSizeId%5D=367&SizePrice%5B0%5D%5BPrice%5D=10",
    CURLOPT_HTTPHEADER => array(
    "content-type: application/x-www-form-urlencoded",
    ),
    ));

    $response = curl_exec($curl);
    $err = curl_error($curl);

    curl_close($curl);

    if ($err) {
    echo "cURL Error #:" . $err;
    } else {
    echo $response;
    }
```

```c#
var client = new RestClient("http://bomgourmet.delivery/api/produtos/");
var request = new RestRequest(Method.POST);
request.AddHeader("content-type", "application/x-www-form-urlencoded");
request.AddParameter("application/x-www-form-urlencoded", "Token=3f59d6f547d995f675522784f5c8c631&Name=Teste%20de%20Produto%20via%20API&CategoryId=1681&Price=10.50&SizePrice%5B0%5D%5BSizeId%5D=367&SizePrice%5B0%5D%5BPrice%5D=10", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

> Retorno:

```json
{
  "Result": "OK",
  "Records": {
    "Id": 16833,
    "PlanId": 232,
    "CategoryId": 1681,
    "SizeId": null,
    "StatusId": 1,
    "Name": "Teste de Produto via API",
    "Description": null,
    "Price": "10.5",
    "Photo": null,
    "SizePrice": [
      {
        "Id": 21696,
        "ProductId": 16832,
        "SizeId": 367,
        "Price": "17.50",
        "TotalPrice": "35.00"
      }
    ]
  }
}
```

> Location: /produtos/16833?token=3f59d6f547d995f675522784f5c8c631

### HTTP Request
`POST /produtos`

### Response Headers
`Location: /produtos/{id}?token={token}`

### Parametros

Parametro           |     Tipo      | Observação
--------------------|---------------|------------
Name                | string        | Nome do produto
Description         | string        | Descrição do produto
CategoryId          | int           | ID da categoria que o produto pertence
Price               | float         | Preço do produto
Photo               | Definir       | Precisamos definir se isso será usado
SizePrice           | array         | Lista de preços por tamanho


### Retorno (Records)
           Campo            |      Formato      | Observação
----------------------------|-------------------|---------------------------------------
Id                          | int               | Identificador do Produto
PlanId                      | int               | Identificador do Plano
CategoryId                  | int               | Identificador da Categoria
SizeId                      | int               | Identificador do Tamanho
StatusId                    | int               | Identificador do Status (1 => Ativo, 2 => Inativo, 9 => Excluido)
Name                        | string            | Nome do produto
Description                 | string            | Descrição do produto
Price                       | float             | Preço do produto
Photo                       | string            | URL da foto do produto
SizePrice                   | Array             | Preços do produto, por tamanho


### Retorno (SizePrice)
           Campo            |      Formato      | Observação
----------------------------|-------------------|---------------------------------------
Id                          | int               | Identificador do Preço
ProductId                   | int               | Identificador do Produto
SizeId                      | int               | Identificador do Tamanho
Price                       | float             | Preço do produto, já divido pela quantidade de opções
TotalPrice                  | float             | Preço total do produto


## Atualizar produto
Endpoint para atualizar um produto.

```php
<?php
    $curl = curl_init();

    curl_setopt_array($curl, array(
    CURLOPT_URL => "http://bomgourmet.delivery/api/produtos/16833",
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_CUSTOMREQUEST => "POST",
    CURLOPT_POSTFIELDS => "Token=3f59d6f547d995f675522784f5c8c631&Name=Teste%20de%20Produto%20via%20API&CategoryId=1681&Price=10.50&SizePrice%5B0%5D%5BSizeId%5D=367&SizePrice%5B0%5D%5BPrice%5D=10",
    CURLOPT_HTTPHEADER => array(
    "content-type: application/x-www-form-urlencoded",
    ),
    ));

    $response = curl_exec($curl);
    $err = curl_error($curl);

    curl_close($curl);

    if ($err) {
    echo "cURL Error #:" . $err;
    } else {
    echo $response;
    }
```

```c#
var client = new RestClient("http://bomgourmet.delivery/api/produtos/16833");
var request = new RestRequest(Method.POST);
request.AddHeader("content-type", "application/x-www-form-urlencoded");
request.AddParameter("application/x-www-form-urlencoded", "Token=3f59d6f547d995f675522784f5c8c631&Name=Teste%20de%20Produto%20via%20API&CategoryId=1681&Price=10.50&SizePrice%5B0%5D%5BSizeId%5D=367&SizePrice%5B0%5D%5BPrice%5D=10", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

> Retorno:

```json
{
  "Result": "OK",
  "Records": {
    "Id": 16833,
    "PlanId": 232,
    "CategoryId": 1681,
    "SizeId": null,
    "StatusId": 1,
    "Name": "Teste de Produto via API",
    "Description": null,
    "Price": "10.5",
    "Photo": null,
    "SizePrice": [
      {
        "Id": 21696,
        "ProductId": 16832,
        "SizeId": 367,
        "Price": "17.50",
        "TotalPrice": "35.00"
      }
    ]
  }
}
```

### HTTP Request
`PUT /produtos/{id}`

### Parametros

Parametro           |     Tipo      | Observação
--------------------|---------------|------------
Name                | string        | Nome do produto
Description         | string        | Descrição do produto
CategoryId          | int           | ID da categoria que o produto pertence
Price               | float         | Preço do produto
Photo               | Definir       | Precisamos definir se isso será usado
SizePrice           | array         | Lista de preços por tamanho


### Retorno (Records)
           Campo            |      Formato      | Observação
----------------------------|-------------------|---------------------------------------
Id                          | int               | Identificador do Produto
PlanId                      | int               | Identificador do Plano
CategoryId                  | int               | Identificador da Categoria
SizeId                      | int               | Identificador do Tamanho
StatusId                    | int               | Identificador do Status (1 => Ativo, 2 => Inativo, 9 => Excluido)
Name                        | string            | Nome do produto
Description                 | string            | Descrição do produto
Price                       | float             | Preço do produto
Photo                       | string            | URL da foto do produto
SizePrice                   | Array             | Preços do produto, por tamanho


### Retorno (SizePrice)
           Campo            |      Formato      | Observação
----------------------------|-------------------|---------------------------------------
Id                          | int               | Identificador do Preço
ProductId                   | int               | Identificador do Produto
SizeId                      | int               | Identificador do Tamanho
Price                       | float             | Preço do produto, já divido pela quantidade de opções
TotalPrice                  | float             | Preço total do produto
