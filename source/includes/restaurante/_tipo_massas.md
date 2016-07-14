# Tipo de Massas

Base URL: http://bomgourmet.delivery/api

## Buscar Produto
Endpoint para buscar um único tipo de massa.

```php
<?php
    $curl = curl_init();

    curl_setopt_array($curl, array(
      CURLOPT_URL => "http://bomgourmet.delivery/api/tipo-massas/16?token=3f59d6f547d995f675522784f5c8c631",
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
var client = new RestClient("http://bomgourmet.delivery/api/tipo-massas/16?token=3f59d6f547d995f675522784f5c8c631");
var request = new RestRequest(Method.GET);
IRestResponse response = client.Execute(request);
```

> Retorno:

```json
{
  "Id": 16,
  "CustomerId": 104945,
  "Name": "Massa API Atualizado",
  "Price": "10.50"
}
```

### HTTP Request
`GET /tipo-massas/{id}`

### Parametros

Parametro | Formato | Observação
----------|---------|------------
id        |  int    | ID do Tipo de Massa
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
Id                          | int               | Identificador do Tipo de Massa
CustomerId                  | int               | Identificador do Cliente
Name                        | string            | Nome do tipo de massa
Price                       | float             | Preço do tipo de massa


## Criar Tipo de Massa
Endpoint para criar um tipo de massa.

<aside class="notice">
    O header "Location" pode ser utilizado para buscar o tipo de massa que foi criado
</aside>

```php
<?php
    $curl = curl_init();

    curl_setopt_array($curl, array(
    CURLOPT_URL => "http://bomgourmet.delivery/api/tipo-massas",
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_CUSTOMREQUEST => "POST",
    CURLOPT_POSTFIELDS => "Token=3f59d6f547d995f675522784f5c8c631&Name=Massa%20API&Price=10"
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
var client = new RestClient("http://bomgourmet.delivery/api/tipo-massas");
var request = new RestRequest(Method.POST);
request.AddHeader("content-type", "application/x-www-form-urlencoded");
request.AddParameter("application/x-www-form-urlencoded", "Token=3f59d6f547d995f675522784f5c8c631&Name=Massa%20API%20&Price=10", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

> Retorno:

```json
{
  "Id": 16,
  "CustomerId": 104945,
  "Name": "Massa API",
  "Price": "10"
}
```

> Location: /tipo-massas/373?token=3f59d6f547d995f675522784f5c8c631

### HTTP Request
`POST /tipo-massas`

### Response Headers
`Location: /tipo-massas/{id}?token={token}`

### Parametros

Parametro           |     Tipo      | Observação
--------------------|---------------|------------
Token               | string        | Token do cliente
Name                | string        | Nome do tipo de massa
Price               | float         | Preço do tipo de massa

### Retorno (Records)
           Campo            |      Formato      | Observação
----------------------------|-------------------|---------------------------------------
Id                          | int               | Identificador do Tipo de massa
CustomerId                  | int               | Identificador do Cliente
Name                        | string            | Nome do tipo de massa
Price                       | float             | Preço do tipo de massa



## Atualizar tipo de massa
Endpoint para atualizar um tipo de massa.

```php
<?php
    $curl = curl_init();

    curl_setopt_array($curl, array(
    CURLOPT_URL => "http://bomgourmet.delivery/api/tipo-massas/16",
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_CUSTOMREQUEST => "PUT",
      CURLOPT_POSTFIELDS => "Token=3f59d6f547d995f675522784f5c8c631&Name=Massa%20API%20Atualizado&Price=15",
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
var client = new RestClient("http://bomgourmet.delivery/api/tipo-massas/16");
var request = new RestRequest(Method.PUT);
request.AddHeader("content-type", "application/x-www-form-urlencoded");
request.AddParameter("application/x-www-form-urlencoded", "Token=3f59d6f547d995f675522784f5c8c631&Name=Massa%20API%20Atualizado&Price=15", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

> Retorno:

```json
{
  "Id": 16,
  "CustomerId": 104945,
  "Name": "Massa API Atualizado",
  "Price": "15"
}
```

### HTTP Request
`PUT /tipo-massas/{id}`

### Parametros

Parametro           |     Tipo      | Observação
--------------------|---------------|------------
Token               | string        | Token do cliente
Name                | string        | Nome do tipo de massa
Price               | float         | Preço do tipo de massa


### Retorno (Records)
           Campo            |      Formato      | Observação
----------------------------|-------------------|---------------------------------------
Id                          | int               | Identificador do Tipo de massa
CustomerId                  | int               | Identificador do Cliente
Name                        | string            | Nome do tipo de massa
Price                       | float             | Preço do tipo de massa
