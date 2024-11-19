# SDK Redirection for .Net Standard 2.0 (EN)

Refer to https://www.getnet.cl/developers for more information.

## Requirements
- SoapHttpClient = v1.4.3
- RestSharp = v105.2.3
- Newtonsoft.Json = v10.0.1

### Adding Dependency in Visual Studio
Go to Solution Explorer, expand project options and then:

> Dependencies -> Add Reference -> Browse -> Browse -> Select dll -> Accept

----------

### Authentication
Configure PlacetoPay instance required to authenticate against PlacetoPay web services.

#### Config:

```csharp
using P2P = PlacetoPay.Integrations.Library.CSharp.PlacetoPay;
Gateway gateway = new P2P(YOUR_LOGIN, YOUR_TRANKEY, new Uri("URL_INTEGRATION"), Gateway.TP_SOAP or Gateway.TP_REST);
```
----------

### Create a New Payment Session
Requests the creation of a session (payment request or subscription) and returns the identifier and processing URL.

#### Example Call:

```csharp
Amount amount = new Amount('PAYMENT_AMOUNT');
Payment payment = new Payment("REFERENCE", "DESCRIPTION", amount);
RedirectRequest request = new RedirectRequest(payment, RETURN_URL, IP_ADDRESS, USER_AGENT, EXPIRATION);
RedirectResponse response = gateway.Request(request);
```

#### Return:
Service responds with an instance of the RedirectResponse class. By checking the response status, you can determine if the payment session was created.

### Success Response:
If status equals "OK" verify

```csharp
response.IsSuccessful() // return boolean
```

#### Error Response:
If status equals "ERROR". Check error reason

```csharp
response.Status.Message // return string
```

----------

### Get Session Information
Gets the information of the session and completed transactions.

#### Example Call:

```csharp
RedirectInformation response = gateway.Query(requestId);
```

#### Return:
Service responds with an instance of the RedirectInformation class. You can verify the session status through

```csharp
response.IsSuccessful() // return boolean
response.IsRejected() // return boolean
response.IsApproved() // return boolean
response.Status.status // return boolean
```

----------

### Charge Without User Intervention
Allows making charges without user intervention using previously subscribed payment methods.

#### Example Call:

```csharp
Token token = new Token("YOUR_TOKEN");
Instrument instrument = new Instrument(token);
Person person = new Person(dni, type, Name, Surname, email);
Amount amount = new Amount(1000);
Payment payment = new Payment("123456789", "TEST", amount);
CollectRequest collectRequest = new CollectRequest(person, payment, instrument);
RedirectInformation collect = this.gateway.Collect(collectRequest);
```

#### Return:
Service responds with an instance of the RedirectInformation class. You can verify the session status through:

```csharp
response.IsSuccessful() // return boolean
response.IsRejected() // return boolean
response.IsApproved() // return boolean
response.Status.status // return boolean
```

----------

### Reverse a Payment
Allows reversing an approved payment using the internal reference code.

#### Example Call:

```csharp
ReverseResponse response = this.gateway.Reverse(requestId);
```

#### Return:
Service responds with an instance of the ReverseResponse class. You can verify the session status through:

```csharp
response.IsSuccessful() // return boolean
response.Status.status // return boolean
```


# SDK Redirection for .Net Standard 2.0 (ES)
Refer to https://www.getnet.cl/developers for more information.

## Requerimientos
- SoapHttpClient = v1.4.3
- RestSharp = v105.2.3
- Newtonsoft.Json = v10.0.1

### Agregar dependencia en Visual Studio
Ir al explorador de soluciones, desplegar las opciones delproyecto y luego:

> Dependencias -> agregar referencia -> examinar -> examinar -> seleccionar dll -> Aceptar

----------

### Autenticación
Configurar instancia PlacetoPay necesaria para autenticarse ante los servicios web de PlacetoPay.

#### Config:

```csharp
using P2P = PlacetoPay.Integrations.Library.CSharp.PlacetoPay;
Gateway gateway = new P2P(YOUR_LOGIN, YOUR_TRANKEY, new Uri("URL_INTEGRATION"), Gateway.TP_SOAP or Gateway.TP_REST);
```
----------

### Crear una nueva sesión de pago
Solicita la creación de la sesión (petición de cobro o suscripción) y retorna el identificador y la URL de procesamiento.

#### Ejemplo de llamada:

```csharp
Amount amount = new Amount('PAYMENT_AMOUNT');
Payment payment = new Payment("REFERENCE", "DESCRIPTION", amount);
RedirectRequest request = new RedirectRequest(payment, RETURN_URL, IP_ADDRESS, USER_AGENT, EXPIRATION);
RedirectResponse response = gateway.Request(request);
```

#### Retorno:
Servicio responde una instancia de la clase RedirectResponse. Verificando el status de la respuesta se puede determinar si se creó la session de pago.

### Success Response:
Si el status es igual a “OK” verifica

```csharp
response.IsSuccessful() // return boolean
```

#### Error Response:
Si el status es igual a “ERROR”. Verificar motivo del error

```csharp
response.Status.Message // return string
```

----------

### Obtenga información sobre una sesión
Obtiene la información de la sesión y transacciones realizadas.

#### Ejemplo de llamada:

```csharp
RedirectInformation response = gateway.Query(requestId);
```

#### Retorno:
Servicio responde una instancia de la clase RedirectInformation. Se puede verificar el status de la sesión a través

```csharp
response.IsSuccessful() // return boolean
response.IsRejected() // return boolean
response.IsApproved() // return boolean
response.Status.status // return boolean
```

----------

### Cobro sin intervención del usuario
Permite realizar cobros sin la intervención del usuario usando medios de pago previamente suscritos.

#### Ejemplo de llamada:

```csharp
Token token = new Token(“YOUR_TOKEN”);
Instrument instrument = new Instrument(token);
Person person = new Person(dni, type, Name, Surname, email);
Amount amount = new Amount(1000);
Payment payment = new Payment("123456789", "TEST", amount);
CollectRequest collectRequest = new CollectRequest(person, payment, instrument);
RedirectInformation collect = this.gateway.Collect(collectRequest);
```

#### Retorno:
Servicio responde una instancia de la clase RedirectInformation. Se puede verificar el status de la sesión a través:

```csharp
response.IsSuccessful() // return boolean
response.IsRejected() // return boolean
response.IsApproved() // return boolean
response.Status.status // return boolean
```

----------

### Revertir un pago
Permite revertir un pago aprobado con el código de referencia interna.

#### Ejemplo de llamada:

```csharp
ReverseResponse response = this.gateway.Reverse(requestId);
```

#### Retorno:
Servicio responde una instancia de la clase ReverseResponse. Se puede verificar el status de la sesión a través:

```csharp
response.IsSuccessful() // return boolean
response.Status.status // return boolean
```