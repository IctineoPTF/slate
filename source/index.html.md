---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  # - <a href='#'>Sign Up for a Developer Key</a>
  # - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introducción


# Autenticación

En la autentificación se utilizan mensajes en clave-hash (HMAC) es una construcción específica para calcular un código de autentificación de mensaje, esto que implica una función hash criptográfica en combinación con una llave criptográfica secreta. Como cualquier MAC, puede ser utilizado para verificar simultáneamente la integridad de los datos y la autentificación de un mensaje. Se utiliza la función hash criptográfica SHA-512. La función hash rompe un mensaje en un bloque de un tamaño fijo e itera sobre ellos con una función de compresión. La fuerza criptográfica del HMAC depende de la potencia criptográfica de la función de hash subyacente, el tamaño de su salida de hash y el tamaño y calidad de la llave.

> Para autorizar utiliza este codigo:

```javascript
function getPath(url) {
    var pathRegex = /.+?\:\/\/.+?(\/.+?)(?:#|\?|$)/;
    var result = url.match(pathRegex);
    return result && result.length > 1 ? result[1] : ''; 
}

function getQueryString(url) {
    var arrSplit = url.split('?');
    return arrSplit.length > 1 ? url.substring(url.indexOf('?')+1) : ''; 
}

var _requestData;

function getAuthHeader(httpMethod, requestUrl, _requestBody) {
    var CLIENT_KEY = 'CLIENT_KEY';
    var hash = 'SECRET_KEY';
    var SECRET_KEY = CryptoJS.enc.Hex.stringify(CryptoJS.SHA512(hash));
    var AUTH_TYPE = 'Ictineo';
    var requestBody = '';
    var requestPath = getPath(requestUrl);
    var queryString = getQueryString(requestUrl);
    if (httpMethod == 'GET' || !_requestBody) {
        requestBody = ''; 
    } else {
        requestBody = JSON.stringify(JSON.parse(_requestBody) );
    }
        
    var timestamp = new Date().getTime(); 
    var requestData = [timestamp,httpMethod, requestPath, queryString, requestBody].join("");
    requestData = requestData.trim();
    _requestData = requestData;        
    var hmacDigest = CryptoJS.enc.Hex.stringify(CryptoJS.HmacSHA256(requestData, SECRET_KEY));
    var authHeader = AUTH_TYPE + ' ' + CLIENT_KEY + ':'+ timestamp + ":"  + hmacDigest;
    return authHeader;
}

postman.setEnvironmentVariable('hmacAuthHeader', getAuthHeader(request['method'], request['url'], request['data']));
postman.setEnvironmentVariable('hmac_d',_requestData);
```

<!-- 
// > Make sure to replace `meowmeowmeow` with your API key.

// Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

// Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

// `Authorization: meowmeowmeow`

// <aside class="notice">
// You must replace <code>meowmeowmeow</code> with your personal API key.
// </aside>  -->

# Clientes

## Creación de cliente

```shell
curl "https://dev.ictineo.com/clients"
  -H "Authorization: token"
```

> El comando anterior devuelve un JSON estructurado como:

```json
{
    "status": "success",
    "message": "Consulta Exitosa",
    "internalCode": "000",
    "data": [
        {
            "numcte": "0001001131",
            "respcode": "000",
            "resptext": "Cliente nuevo:TEGC8810102I1"
        }
    ]
}
```

Endpoint para creación de clientes

### HTTP Request

`POST https://dev.ictineo.com/clients`

### Envío de parametros

Parametro | Requerido | Descripción
--------- | ------- | -----------
name | si | Nombre
second_name | si | Segundo nombre
last_name | si | Apellido paterno
second_lastname | si | Apellido materno
phone | si | Telefono a 10 digitos
date_birth | si | Fecha de nacimiento MM/DD/YYYY
gender | si | Genero - F := Femenino, M := Masculino
country_of_birth_id | si |  Id del pais de nacimiento, consultar catalogo 
nationality_id | si | Id de nacionalidad
place_of_birth_id | si | Id de lugar de nacimiento
curp | si | CURP
civil_status | si | Estatus Civil
profession_id | si | Id de profesión
occupation_id | si | Id de ocupación
economy_activity_id | si | Id de actividad economica
education_id | si | Educación
main_activity_id | si | Id de principal actividad economica
street | si | Calle de dirección
number | si | Numero exterior de dirección
apartment_number | si | Numero interior de dirección
postal_code | si | Codigo postal
suburb_id | si | Id de colonia
city_id | si | Id de ciudad
state_id | si | Id de estado
country_id | si | Id de pais

<!-- <aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside> -->

## Consulta de cliente

```shell
curl "https://dev.ictineo.com/clients/0001001131"
  -H "Authorization: token"
```
<!-- 
```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
``` -->

> El comando anterior devuelve un JSON estructurado como:

```json
{
    "status": "success",
    "message": "Consulta Exitosa",
    "internalCode": "000",
    "data": [
        {
            "codret": "000",
            "numcte": "0001001131",
            "sucursal": "0001",
            "ejecutivo": "usuponic",
            "tp_persona": "01",
            "tp_cliente": "1",
            "apell_pat": "DELGADO",
            "apell_mat": "SANCHEZ",
            "nombre1": "JOSE JHONATTAN",
            "nombre2": "",
            "rfc": "DESJ830127UBA",
            "sector": "0",
            "segmento": "0",
            "actividad_princ": "0",
            "grupo": "0",
            "subgrupo": "0",
            "residencia": "1",
            "apell_casada": "",
            "numcte_ref": "",
            "distrito": "0",
            "puesto_ppes": "0",
            "familiar_ppes": "0",
            "actividad_esp": "9999999",
            "fecha_nac": "27/01/1983",
            "lugar_nac": "32",
            "nacionalidad": "1",
            "fm3": "",
            "estado_civil": "",
            "regimen_mat": "0",
            "profesion": "1",
            "sexo": "M",
            "curp": "DESJ830127HZSLNH04",
            "codidentif": "3",
            "numidentif": "0211045936150",
            "no_imss": "",
            "dependientes": 0,
            "tutor": "",
            "email": "0",
            "nom_conyuge": "0",
            "seguro_defunc": "0",
            "escolaridad": "04",
            "habita_en": "0",
            "anios_habita": 0,
            "nombre_prop": "0",
            "imphiporenta": 0,
            "numeroife": "",
            "numerotutor": "",
            "numeroconyuge": "0",
            "ejecut_autoriza": "0",
            "valor_inmueble": 0,
            "renta_mensual": 0,
            "sindicato": "0",
            "sindicalizado": "0",
            "cta_bancaria": "0",
            "cod_cta_bancari": "0",
            "meses_habita": 0,
            "buro_cred": "0",
            "numcta": "0",
            "fam_financiera": "0",
            "parentesco_fam": "0",
            "susceptible": "0",
            "calificacion": 0,
            "colegiatura": 0,
            "tipoingreso": "",
            "motingreso": "",
            "status": "A",
            "reactivacion": "",
            "tposocio": "M",
            "inactivacion": "",
            "dom_extranjero": "0",
            "autorizacion": 0,
            "representante": "0",
            "tarjetadesc": 0,
            "ocupacion": "99",
            "pais_cte": "484",
            "recurso": "S",
            "titular": "",
            "nombre_titular": "",
            "numtitular": "",
            "titular2": "",
            "nombre_titular2": "",
            "numtitular2": "",
            "fecha_alta": "19/03/2019"
        }
    ]
}
```

Endpoint para consultar los datos de un cliente en especifico

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### HTTP Request

`GET https://dev.ictineo.com/clients/<CLIENT_NUMBER>`

### URL Parameters

Parameter | Description
--------- | -----------
client_number | El numero de cliente que se quiere consultar.

# Cuentas

## Creación de cuenta

```shell
curl "https://dev.ictineo.com/accounts"
  -H "Authorization: token"
```

> El comando anterior devuelve un JSON estructurado como:

```json
{
    "status": "success",
    "message": "Consulta Exitosa",
    "internalCode": "000",
    "data": [
        {
            "numcte": "0001001131",
            "cuenta": "10000006764",
            "cuentaclabe": "646180123310006764",
            "respcode": "000",
            "resptext": "Alta de cuenta exitosa"
        }
    ]
}
```

Endpoint para creación de una cuenta de captación

### HTTP Request

`POST https://dev.ictineo.com/accounts`

### Envío de parametros

Parametro | Requerido | Descripción
--------- | ------- | -----------
client_number | si | Numero de cliente al que se le creara la cuenta
product_id | si | Id del producto de cuenta que se le asignara 

## Consulta de saldo

```shell
curl "https://dev.ictineo.com/accounts/10000006764/balance"
  -H "Authorization: token"
```

> El comando anterior devuelve un JSON estructurado como:

```json
{
    "status": "success",
    "message": "Consulta Exitosa",
    "internalCode": "000",
    "data": [
        {
            "vcod_ret": "000",
            "vcuenta": "10000006764",
            "vnum_cte": "0001001131",
            "vapell_pat": "TEJEDA",
            "vapell_mat": "GONZALEZ",
            "vnombre1": "CARO",
            "vnombre2": "DOLO",
            "vrazon_soc": "",
            "vedo_cta": "0",
            "vsdo_disp": 0,
            "vsdo_ret": 0,
            "vsdo_ccc": 0,
            "vsdo_disp_ccc": 0,
            "vsdo_cta": 0,
            "vtipo_linea": "0",
            "vdescrip1": "1000 CUENTA EJE",
            "vdescrip2": "01 Peso Mexicano",
            "vsdo_t1": 0,
            "vsdo_cong": 0,
            "vimp_chq_sbc": 0,
            "vusubloq": "",
            "vfecbloq": "",
            "vnum_tarjeta": "",
            "vcta_clabe": "646180123310006764"
        }
    ]
}
```

Endpoint para consultar el saldo de una cuenta en especifico

### HTTP Request

`GET https://dev.ictineo.com/accounts/<account>/balance`

### Envío de parametros

Parametro | Requerido | Descripción
--------- | ------- | -----------
account | si | Numero de cuenta

## Consulta de transacciones

```shell
curl "https://dev.ictineo.com/accounts/10000006764/transactions?dateIni=05/01/2020&dateEnd=05/30/2020"
  -H "Authorization: token"
```

> El comando anterior devuelve un JSON estructurado como:

```json
{
    "status": "success",
    "message": "Consulta Exitosa",
    "internalCode": "000",
    "data": []
}
```

Endpoint para consultar las transacciones de una cuenta en especifico

### HTTP Request

`GET https://dev.ictineo.com/accounts/<account>/transactions?dateIni=<dateIni>&dateEnd=<dateEnd>`

### Envío de parametros

Parametro | Requerido | Descripción
--------- | ------- | -----------
account | si | Numero de cuenta
dateIni | no | Fecha de inicio para filtro de transacciones
dateEnd | no | Fecha de fin para inicio de transacciones

# Tarjetas

## Asignación de tarjeta

```shell
curl "https://dev.ictineo.com/card/active"
  -H "Authorization: token"
```

> El comando anterior devuelve un JSON estructurado como:

```json
{
    "status": "success",
    "message": "Consulta Exitosa",
    "internalCode": "000",
    "data": [
        {
            "(expression 1)": "000",
            "(expression 2)": "5064600000000462"
        }
    ]
}
```

Endpoint para asignación de tarjeta de debito a una cuenta en especifico

### HTTP Request

`POST https://dev.ictineo.com/card/active`

### Envío de parametros

Parametro | Requerido | Descripción
--------- | ------- | -----------
account | si | Numero de cuenta a la que se le asignara la cuenta.
product_id | si | Id del producto de cuenta que tiene asignado.
product_card_id | si | Id del producto de tarjeta que se le asignara.
card_number | no | Se le puede enviar el numero de tarjeta a asignar o si se envia vacio se asigna una tarjeta del stock.

## Cambio de estatus

```shell
curl "https://dev.ictineo.com/card/status"
  -H "Authorization: token"
```

> El comando anterior devuelve un JSON estructurado como:

```json
{
    "status": "success",
    "message": "Consulta Exitosa",
    "internalCode": "000",
    "data": [
        {
            "(expression 1)": "000"
        }
    ]
}
```

Endpoint para cambio de estatus de una tarjeta en especifico

### HTTP Request

`POST https://dev.ictineo.com/card/status`

### Envío de parametros

Parametro | Requerido | Descripción
--------- | ------- | -----------
card_number | si | Numero de tarjeta a la que se le cambiara el estatus.
status | si | Tipos de estatus - A := Activa, I := Inactiva, E := Extravio, B := Bloqueada, F := Bloqueo Fraude, D := Dañada, P := Preventivo Fraude, C := Cancelada, X := Bloqueada por el cliente, R := Robo.
comment | no | Comentario sobre el cambio de estatus


# Transferencias

## Generar transferencia

```shell
curl "https://dev.ictineo.com/transfers"
  -H "Authorization: token"
```

> El comando anterior devuelve un JSON estructurado como:

```json
{
    "status": "success",
    "message": "Consulta Exitosa",
    "internalCode": "000",
    "data": [
        {
            "ocodret": "000",
            "omensaje": "PROCESO SATISFACTORIO",
            "oimporte": 5,
            "ofolio": "BCAELECT124514"
        }
    ]
}
```

Endpoint para realizar transferencias a cuentas propias, cuentas de terceros y cuentas a otros bancos.

### HTTP Request

`POST https://dev.ictineo.com/transfers`

### Envío de parametros

Parametro | Requerido | Descripción
--------- | ------- | -----------
type | si | Tipo de transferencia - thirdy := Transferencia a cuentas de terceros, accounts := Transferencia a cuentas propias, spei := Transferencia a otros bancos 
client_number | si | Numero de cliente que realizara la transferencia
account_origin | si | Numero de cuenta origen
account_destination | si | Numero de cuenta destino
amount | si | Monto que se enviara
reference | si | Referencia de identificación de transferencia
date | si | Fecha MM-DD-YYYY
concept | si | Concepto de la transferencia

# Catalogos

## General

```shell
curl "https://dev.ictineo.com/catalog/4"
  -H "Authorization: token"
```

> El comando anterior devuelve un JSON estructurado como:

```json
{
    "status": "success",
    "message": "Consulta Exitosa",
    "internalCode": "000",
    "data": [
        {
            "codret": 0,
            "sqlerr": 0,
            "catalogo": "bdinteg:si_edocivil",
            "codigo_descripcion": "S",
            "descripcion": "SOLTERO(A)"
        },
        {
            "codret": 0,
            "sqlerr": 0,
            "catalogo": "bdinteg:si_edocivil",
            "codigo_descripcion": "C",
            "descripcion": "CASADO(A)"
        },
        {
            "codret": 0,
            "sqlerr": 0,
            "catalogo": "bdinteg:si_edocivil",
            "codigo_descripcion": "D",
            "descripcion": "DIVORCIADO(A)"
        },
        {
            "codret": 0,
            "sqlerr": 0,
            "catalogo": "bdinteg:si_edocivil",
            "codigo_descripcion": "V",
            "descripcion": "VIUDO(A)"
        },
        {
            "codret": 0,
            "sqlerr": 0,
            "catalogo": "bdinteg:si_edocivil",
            "codigo_descripcion": "U",
            "descripcion": "UNION LIBRE"
        }
    ]
}
```

Endpoint para consultar los distintos catalogos para llenado de datos en creación de cliente

### HTTP Request

`POST https://dev.ictineo.com/catalog/<ID>`

### Envío de parametros

Parametro | Requerido | Descripción
--------- | ------- | -----------
id | si | Id del catalogo que se consultara