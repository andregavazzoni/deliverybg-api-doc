# Tamanhos

Base URL: http://bomgourmet.delivery/api

## Buscar Produto
Endpoint para buscar um único tamanho.

```php
<?php
    $curl = curl_init();

    curl_setopt_array($curl, array(
      CURLOPT_URL => "http://bomgourmet.delivery/api/tamanhos/373?token=3f59d6f547d995f675522784f5c8c631",
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
var client = new RestClient("http://bomgourmet.delivery/api/tamanhos/373?token=3f59d6f547d995f675522784f5c8c631");
var request = new RestRequest(Method.GET);
IRestResponse response = client.Execute(request);
```

> Retorno:

```json
{
  "Id": 373,
  "CustomerId": 104945,
  "Name": "Teste API Atualizado",
  "Quantity": 4
}
```

### HTTP Request
`GET /tamanhos/{id}`

### Parametros

Parametro | Formato | Observação
----------|---------|------------
id        |  int    | ID do Tamanho
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
Id                          | int               | Identificador do Tamanho
CustomerId                  | int               | Identificador do Cliente
Name                        | string            | Nome do tamanho
Quantity                    | int               | Quantidade de sabores permitidos


## Criar tamanho
Endpoint para criar um tamanho.

<aside class="notice">
    O header "Location" pode ser utilizado para buscar o tamanho que foi criado
</aside>

```php
<?php
    $curl = curl_init();

    curl_setopt_array($curl, array(
    CURLOPT_URL => "http://bomgourmet.delivery/api/tamanhos",
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_CUSTOMREQUEST => "POST",
    CURLOPT_POSTFIELDS => "Token=3f59d6f547d995f675522784f5c8c631&Name=Teste%20API&Quantity=4"
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
request.AddParameter("application/x-www-form-urlencoded", "Token=3f59d6f547d995f675522784f5c8c631&Name=Teste%20API%20&Quantity=4", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

> Retorno:

```json
{
  "Id": 373,
  "CustomerId": 104945,
  "Name": "Teste API Atualizado",
  "Quantity": 4
}
```

> Location: /tamanhos/373?token=3f59d6f547d995f675522784f5c8c631

### HTTP Request
`POST /tamanhos`

### Response Headers
`Location: /tamanhos/{id}?token={token}`

### Parametros

Parametro           |     Tipo      | Observação
--------------------|---------------|------------
Token               | string        | Token do cliente
Name                | string        | Nome do tamanho
Quantity            | int           | Quantidade de sabores permitidos

### Retorno (Records)
           Campo            |      Formato      | Observação
----------------------------|-------------------|---------------------------------------
Id                          | int               | Identificador do Tamanho
CustomerId                  | int               | Identificador do Cliente
Name                        | string            | Nome do tamanho
Quantity                    | int               | Quantidade de sabores permitidos



## Atualizar tamanho
Endpoint para atualizar um tamanho.

```php
<?php
    $curl = curl_init();

    curl_setopt_array($curl, array(
    CURLOPT_URL => "http://bomgourmet.delivery/api/tamanhos/373",
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_CUSTOMREQUEST => "POST",
      CURLOPT_POSTFIELDS => "Token=3f59d6f547d995f675522784f5c8c631&Name=Teste%20API%20Atualizado&Quantity=4",
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
var client = new RestClient("http://bomgourmet.delivery/api/tamanhos/373");
var request = new RestRequest(Method.POST);
request.AddHeader("content-type", "application/x-www-form-urlencoded");
request.AddParameter("application/x-www-form-urlencoded", "Token=3f59d6f547d995f675522784f5c8c631&Name=Teste%20API%20Atualizado&Quantity=4", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

> Retorno:

```json
{
  "Id": 373,
  "CustomerId": 104945,
  "Name": "Teste API Atualizado",
  "Quantity": 4
}
```

### HTTP Request
`PUT /tamanhos/{id}`

### Parametros

Parametro           |     Tipo      | Observação
--------------------|---------------|------------
Token               | string        | Token do cliente
Name                | string        | Nome do tamanho
Quantity            | int           | Quantidade de sabores permitidos


### Retorno (Records)
           Campo            |      Formato      | Observação
----------------------------|-------------------|---------------------------------------
Id                          | int               | Identificador do Tamanho
CustomerId                  | int               | Identificador do Cliente
Name                        | string            | Nome do tamanho
Quantity                    | int               | Quantidade de sabores permitidos
