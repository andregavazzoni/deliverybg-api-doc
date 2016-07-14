
# GNC
Documentação para integração com a GNC. Essa documentação não é a versão final estando sujeita a alterações. Apenas para análise

<aside class="notice">
    "Categoria" e "Produtos" foram removidas daqui e criado uma documentação mais detalhada.
    Consultar menu ao lado.
</aside>

## Listar

Endpoint para buscar os pedidos que ainda não foram recebidos pelo restaurante.

```php
<?php

$data = [
    "token" => "3f59d6f547d995f675522784f5c8c631"
];

$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "http://bomgourmet.delivery/api/pedidos/listar",
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
          "GNCId":  123,
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
`POST /pedidos/listar`

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
       Campo            |       Tipo        | Observação
------------------------|-------------------|----------------
ProductId               | int               | Identificador do produto
GNCId                   | int               | ID do produto no sistema GNC. (Confimar o tipo de dado).
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

## Categorias
Como ainda estamos definindo como irá funcionar a integração, esta é só o básico que precisamos para importar categorias.

### Parametros
Outros parametros ainda serão definidos junto com a GNC

  Campo     |     Tipo    | Observação
------------|-------------|------------
 Token      |   string    | Token do restaurante

### Campos necessários para importar categoria

  Campo             |     Tipo      | Observação
--------------------|---------------|------------
CustomerId          | int           | ID do Cliente, podemos usar o token para isso também.
ParentCategoryId    | int           | ID da Categoria pai (Opcional)          
Name                | string        | Nome da categoria
Description         | string        | Descrição da categoria
Sizes               | Definir       | Tamanhos que serão aceitos nessa categoria.
PriceType           | int           | Tipo de calculo que será usado para categorias que permitem mais de um sabor. 0 => Maior preço, 1 => Preço médio
KindPasta           | Definir       | Tipos de massas que serão aceitos nessa categoria, caso haja algum.

## Produtos
Como ainda estamos definindo como irá funcionar a integração, esta é só o básico que precisamos para importar produtos.

### Parametros
Outros parametros ainda serão definidos junto com a GNC

  Campo     |     Tipo    | Observação
------------|-------------|------------
 Token      |   string    | Token do restaurante


### Campos necessários para importar produtos

  Campo             |     Tipo      | Observação
--------------------|---------------|------------
Name                | string        | Nome do produto
Description         | string        | Descrição do produto
CategoryId          | int           | ID da categoria que o produto pertence
Price               | float         | Preço do produto
Photo               | Definir       | Precisamos definir se isso será usado
SizePrice           | array         | Lista de preços por tamanho
