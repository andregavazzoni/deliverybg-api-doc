# Categorias

Base URL: http://bomgourmet.delivery/api

## Buscar Categoria
Endpoint para buscar uma única categoria.

```php
<?php
    $curl = curl_init();

    curl_setopt_array($curl, array(
      CURLOPT_URL => "http://bomgourmet.delivery/api/categorias/1671?token=3f59d6f547d995f675522784f5c8c631",
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
var client = new RestClient("http://bomgourmet.delivery/api/categorias/1671?token=3f59d6f547d995f675522784f5c8c631");
var request = new RestRequest(Method.GET);
IRestResponse response = client.Execute(request);
```

> Retorno:

```json
{
  "Result": "OK",
  "Records": {
    "Id": 1671,
    "ParentId": 1682,
    "CustomerId": 104945,
    "StatusId": 1,
    "Name": "Pizza",
    "Description": null,
    "Order": 3,
    "PriceType": 1,
    "Sizes": [
      {
        "CategoryId": 1671,
        "SizeId": 367
      }
    ],
    "KindPastas": [
      {
        "CategoryId": 1671,
        "PastaId": 16
      }
    ]
  }
}
```

### HTTP Request
`GET /categorias/{id}`

### Parametros

Parametro | Formato | Observação
----------|---------|------------
id        |  int    | ID da Categoria
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
Id                          | int               | Identificador da Categoria
ParentId                    | int / null        | Identificador da Categoria Pai
CustomerId                  | int               | Identificador do Restaurante
StatusId                    | int               | Identificador do Status (1 => Ativo, 2 => Inativo, 9 => Excluido)
Name                        | string            | Nome da categoria
Description                 | string            | Descrição da categoria
Order                       | int               | Ordem da categoria
PriceType                   | int               | Tipo do preço (1 => Maior valor, 2 => Média dos Valores)
Sizes                       | Array             | Tamanhos da categoria
KindPastas                  | Array             | Tipo de massas da categoria



## Criar categoria
Endpoint para criar uma categoria.

<aside class="notice">
    O header "Location" pode ser utilizado para buscar a categoria que foi criada
</aside>

```php
<?php
    $curl = curl_init();

    curl_setopt_array($curl, array(
    CURLOPT_URL => "http://bomgourmet.delivery/api/categorias/",
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_CUSTOMREQUEST => "POST",
    CURLOPT_POSTFIELDS => "Token=3f59d6f547d995f675522784f5c8c631&Name=Teste%20API%202&Description=Testando%20API&Size%5B0%5D=360&PriceType=1&KindPasta%5B0%5D=16",
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
var client = new RestClient("http://bomgourmet.delivery/api/categorias/");
var request = new RestRequest(Method.POST);
request.AddHeader("content-type", "application/x-www-form-urlencoded");
request.AddParameter("application/x-www-form-urlencoded", "Token=3f59d6f547d995f675522784f5c8c631&Name=Teste%20API%202&Description=Testando%20API&Size%5B0%5D=360&PriceType=1&KindPasta%5B0%5D=16", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

> Retorno:

```json
{
  "Result": "OK",
  "Records": {
    "Id": 1672,
    "ParentId": 1682,
    "CustomerId": 104945,
    "StatusId": 1,
    "Name": "Pizza",
    "Description": null,
    "Order": 3,
    "PriceType": 1
  }
}
```

> Location: /categorias/1672?token=3f59d6f547d995f675522784f5c8c631

### HTTP Request
`POST /categorias/`

### Response Headers
`Location: /categorias/{id}?token={token}`

### Parametros

Parametro           |     Tipo      | Observação
--------------------|---------------|------------
Token               | string        | Token do Restaurante
ParentCategoryId    | int           | ID da Categoria pai (Opcional)          
Name                | string        | Nome da categoria
Description         | string        | Descrição da categoria
Sizes               | Definir       | Tamanhos que serão aceitos nessa categoria.
PriceType           | int           | Tipo de calculo que será usado para categorias que permitem mais de um sabor. 0 => Maior preço, 1 => Preço médio
KindPasta           | Definir       | Tipos de massas que serão aceitos nessa categoria, caso haja algum.


### Retorno

  Campo | Formato | Observação
--------|---------|-----------
Result  |  string | Identificação do Retorno. OK ou Error
Error   |  array  | Lista de erros, caso exista
Records |  array  | Lista de pedidos, conforme abaixo


### Retorno (Records)
           Campo            |      Formato      | Observação
----------------------------|-------------------|---------------------------------------
Id                          | int               | Identificador da Categoria
ParentId                    | int / null        | Identificador da Categoria Pai
CustomerId                  | int               | Identificador do Restaurante
StatusId                    | int               | Identificador do Status (1 => Ativo, 2 => Inativo, 9 => Excluido)
Name                        | string            | Nome da categoria
Description                 | string            | Descrição da categoria
Order                       | int               | Ordem da categoria
Sizes                       | Array             | Tamanhos da categoria
