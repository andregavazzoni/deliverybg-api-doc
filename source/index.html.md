---
title: Delivery | Bom Gourmet - Documentação API

language_tabs:
  - php: PHP
  - csharp: C#

toc_footers:
  - <a href='http://bomgourmet.delivery' target="_blank">Delivery | Bom Gourmet</a>

search: true
---

# Impressora
Documentação para a integração com o sistema de impressão automática de pedidos.

## Listar

Endpoint para buscar os pedidos que ainda não foram listados no Software da Impressora

```php
<?php

$data = [
    "token" => "3f59d6f547d995f675522784f5c8c631"
];

$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "http://bomgourmet.delivery/api/pedido/confirmacao",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => $data,
]);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

> Retorno:

```json
{
  "Result"  ​:"OK",
  "Errors"  ​:[

  ],
  "Records"  ​:[
    {
      "Id"      ​:1,
      "RestaurantName"      ​:"Teste",
      "Price"      ​:50.00,
      "Discount"      ​:0.00,
      "Fare"      ​:10.00,
      "CustomerId"      ​:1,
      "CustomerName"      ​:"Cliente",
      "CustomerEmail"      ​:"cliente@email.com",
      "CustomerPhone"      ​:"(41) 99887766",
      "DeliveryAddressZipcode"      ​:"80010-020",
      "DeliveryAddressRegion"      ​:"Centro",
      "DeliveryAddressCity"      ​:"Curitiba",
      "DeliveryAddressState"      ​:"Paraná",
      "DeliveryAddressAddress"      ​:"Rua Pedro Ivo",
      "DeliveryAddressNumber"      ​:"409",
      "DeliveryAddressComplement"      ​:null,
      "PaymentMethodId"      ​:1,
      "PaymentMethodName"      ​:"Dinheiro",
      "PaymentMethodMoneyReturn"      ​:100.00,
      "VoucherId"      ​:1,
      "VoucherName"      ​:"Teste de voucher",
      "VoucherCode"      ​:"CODIGO-VOUCHER",
      "VoucherDiscount"      ​:20.00,
      "DeliveryWayId"      ​:1,
      "DeliveryWayName"      ​:"Entrega",
      "Date"      ​:"2015-10-13 13:35:00",
      "Observation": "Exemplo de observação",
      "CustomerDocument": "59273924310",
      "Products"      ​:[
        {
          "ProductId"          ​:1,
          "ProductQuantity"          ​:1,
          "ProductPrice"          ​:70.00,
          "ProductName"          ​:"Coca cola",
          "ProductCategoryParent"          ​:"600ml",
          "ProductCategory"          ​:"Bebidas",
          "SizeName"          ​:null,
          "SizeQuantity"          ​:null,
          "Part"          ​:1,
          "PastaName"          ​:null,
          "PastaPrice"          ​:null,
          "SaleName"          ​:null,
          "Observation"          ​:"Trazer quente"
        }
      ]
    }
  ]
}
```

### HTTP Request
`POST /impressora/listar`

### Parametros

Parametro | Formato | Observação
----------|---------|------------
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
Id                          | int               | Identificado do pedido
RestaurantName              | string            | Nome do restaurante
Price                       | float             | Valor total do pedido
Discount                    | float / null      | Valor de desconto do pedido
Fare                        | float             | Valor da taxa de entrega
CustomerId                  | int               | Identificado do cliente
CustomerName                | string            | Nome do cliente
CustomerEmail               | string            | Email do cliente
CustomerPhone               | string            | Telefone do cliente
DeliveryAddressZipcode      | string            | CEP de entrega
DeliveryAddressRegion       | string            | Bairro de entrega
DeliveryAddressCity         | string            | Cidade de entrega
DeliveryAddressState        | string            | Estado de entrega
DeliveryAddressAddress      | string            | Endereço de entrega
DeliveryAddressNumber       | int               | Número
DeliveryAddressComplement   | string            | Complemento
PaymentMethodId             | int               | Identificador da forma de pagamento
PaymentMethodName           | string            | Nome da forma de pagamento
PaymentMethodMoneyReturn    | float / null      | Troco
VoucherId                   | int / null        | Identificado do voucher
VoucherName                 | string / null     | Nome da promoção
VoucherCode                 | string / null     | Código do voucher
VoucherDiscount             | float / null      | Valor de desconto do voucher
DeliveryWayId               | int               | Identificador da forma de entrega
DeliveryWayName             | string            | Nome da forma de entrega
CustomerDocument            | string            | CPF do Cliente
Observation                 | string            | Observação sobre o pedido
Date                        | datetime          | Data e hora do pedido
Products                    | array             | Lista com os produtos, conforme abaixo.

### Retorno (Products)
       Campo            |      Formato      | Observação
------------------------|-------------------|----------------
ProductId               | int               | Identificado do produto
ProductQuantity         | int               | Quantidade
ProductPrice            | float             | Valor do produto
ProductName             | string            | Nome do produto
ProductCategoryParent   | string            | Categoria principal do produto
ProductCategory         | string / null     | Categoria do produto
SizeName                | string / null     | Nome do tamanho do produto
SizeQuantity            | int  / null       | Quantidade de partes do tamanho
Part                    | int               | Parte que o produto atual representa no tamanho
PastaName               | string / null     | Tipo de massa do produto
PastaPrice              | float / null      | Valor da massa
SaleName                | string / null     | Nome da promoção
Observation             | string / null     | Observações do cliente

## Cancelar pedido
Endpoint para cancelar um pedido.

```php
<?php

$data = [
    "token" => "3f59d6f547d995f675522784f5c8c631",
    "order" => "100"
];

$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "http://bomgourmet.delivery/api/pedido/cancelar",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => $data,
]);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

> Retorno:

```json
{
  "Result"  ​:"OK",
  "Errors"  ​:[]
}
```

### HTTP Request
`POST /impressora/cancelar`

### Parametros

Parametro | Formato | Observação
----------|---------|------------
token     | string  | Token do cliente.
order     | int     | ID do pedido


### Retorno

  Campo | Formato | Observação
--------|---------|-----------
Result  |  string | Identificação do Retorno. OK ou Error
Error   |  array  | Lista de erros, caso exista


## Ping
Endpoint para verificar se a API esta respondendo

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "http://bomgourmet.delivery/api/pedido/ping",
  CURLOPT_RETURNTRANSFER => true
]);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

> Retorno:

```json
{
  "Result"  ​:"OK"
}
```

### HTTP Request
`GET /impressora/ping`

### Retorno

  Campo | Formato | Observação
--------|---------|-----------
Result  |  string | Identificação do Retorno. OK ou Error
