---
description: >-
  TusFacturasAPP: API para Facturas A de AFIP/ARCA. Confiable desde 2015. Creada
  por devs y respaldada por expertos impositivos. ¡Los desarrolladores la aman!
icon: code
---

# Webhook

### Ejemplos de Webhook

Segun tu lenguaje de programacion

{% tabs %}
{% tab title="Workflow " %}
1. Obtener los headers recibidos
2. Evaluar si el header incluye el token esperado de TF
3. Si el token coincide:
   1. Obtener la informacion recibida&#x20;
   2. Ejecutar la consulta avanzada por ext. reference para traer la info del comprobante en cuestion.&#x20;
   3. Devolver un codigo http = 200
4. Si el token no coincide, salir del proceso.
{% endtab %}

{% tab title="PHP" %}
```php
<?php

$tf_token 	= 'TOKEN_TF';  
$headers 	= getallheaders();
$header_token 	= ($headers['TF-WebhookToken'] ??  ($headers['tf-webhooktoken'] ?? '')  );

if ($header_token !== $tf_token) 
{

	http_response_code(403);
	echo 'El Token recibido no coincide con el esperado';
	exit;

}else{

	$data = file_get_contents('php://input');

	// Consulto en TF la info asociada a la ext. reference recibida
	consultar_por_ext_ref($data['external_reference']);

	// Respondo a TF con 200 para evitar entrar en el workflow de reintentos
	http_response_code(200);
	echo 'OK';
	
}



// -------------------------------------------------------------------------------------------------------
// Funcion que usa la consulta avanzada por ext. ref
// Docu: 
// https://developers.tusfacturas.app/web-services-afip-api-arca/consulta-avanzada-por-external-reference
// -------------------------------------------------------------------------------------------------------
function consultar_por_ext_ref(string $ext_ref)
{
	//
}

?>
```
{% endtab %}

{% tab title="Python" %}
```python
import os
from flask import Flask, request, abort, jsonify

# Create a Flask application instance
app = Flask(__name__)

# --- Configuration ---
# Your secret token from TusFacturasAPP
# It's better practice to load this from environment variables
# For example: os.environ.get('TF_WEBHOOK_TOKEN', 'YOUR_DEFAULT_TOKEN_IF_ENV_VAR_NOT_SET')
TF_WEBHOOK_TOKEN = 'TOKEN_TF'

# --- Webhook Endpoint ---
# This is the URL where TusFacturasAPP will send webhooks (e.g., http://yourserver.com:5000/webhook)
@app.route('/webhook', methods=['POST'])
def webhook():
    app.logger.info('Webhook received!')

    # 1. Get the token from the request headers
    # Headers in Flask's request.headers are case-insensitive by default, but it's good to check common casings.
    header_token = request.headers.get('TF-WebhookToken') or \
                   request.headers.get('tf-webhooktoken')

    # 2. Validate the token
    if header_token != TF_WEBHOOK_TOKEN:
        app.logger.warning('Unauthorized webhook access: Token mismatch.')
        # Use abort() for Flask to handle HTTP responses more cleanly
        abort(403, description='El Token recibido no coincide con el esperado')

    # 3. Token is valid, process the webhook data
    # request.json automatically parses JSON bodies
    data = request.json

    if not data:
        app.logger.error('No JSON data received in webhook request.')
        abort(400, description='No se recibió información en formato JSON.')

    app.logger.info(f'Webhook data: {data}')

    # Call your function to consult info based on external_reference
    # In a real application, this would involve database operations,
    # calling external APIs, or other backend logic.
    # We'll use a try-except block for robust error handling.
    try:
        # Ensure 'external_reference' exists in the payload
        external_reference = data.get('external_reference')
        if external_reference:
            consultar_por_ext_ref(external_reference)
        else:
            app.logger.warning("Webhook data missing 'external_reference' key.")

        # 4. Respond with 200 OK to prevent re-attempts from TusFacturasAPP
        app.logger.info('Webhook processed successfully. Sending 200 OK.')
        return 'OK', 200
    except Exception as e:
        app.logger.error(f'Error processing webhook: {e}', exc_info=True)
        # For webhook handlers, sending 200 OK even on internal processing errors
        # is often desired to acknowledge receipt and prevent re-attempts from sender.
        # Handle the error internally.
        return 'OK (processed with internal error)', 200


# --- Helper Function (simulating PHP's consultar_por_ext_ref) ---
def consultar_por_ext_ref(ext_ref: str):
    """
    Simulates a function to consult information associated with an external reference.
    In a real scenario, this would involve database operations, calling external APIs, etc.
    """
    app.logger.info(f'Consulting info for external_reference: {ext_ref}')
    # Implement your actual logic here (e.g., call TusFacturasAPP API, update database)
    # This could be an asynchronous operation if using a framework like FastAPI or Quart
    # For Flask, if you need async, you'd use a library like 'gevent' or 'eventlet' or move to FastAPI.
    pass # Placeholder for actual implementation


# --- Start the server ---
if __name__ == '__main__':
    # When running with 'flask run' (development server):
    # Flask will automatically handle port and debug mode.
    # To run directly as a script (for basic testing, not production):
    app.run(host='0.0.0.0', port=5000, debug=True)
    # For production, use a WSGI server like Gunicorn or uWSGI.

```
{% endtab %}

{% tab title="Node.js" %}
```javascript
// Import necessary modules
const express = require('express');
const bodyParser = require('body-parser'); // To parse incoming JSON bodies

// Create an Express application
const app = express();
const port = 3000; // Choose a port for your webhook listener

// --- Configuration ---
// Your secret token from TusFacturasAPP
// It's better practice to load this from environment variables (e.g., process.env.TF_WEBHOOK_TOKEN)
const TF_WEBHOOK_TOKEN = 'TOKEN_TF';

// Middleware to parse JSON request bodies
app.use(bodyParser.json());

// --- Webhook Endpoint ---
// This is the URL where TusFacturasAPP will send webhooks (e.g., http://yourserver.com:3000/webhook)
app.post('/webhook', (req, res) => {
    console.log('Webhook received!');

    // 1. Get the token from the request headers
    // Headers are typically lowercase in Node.js/Express
    const headerToken = req.headers['tf-webhooktoken'];

    // 2. Validate the token
    if (headerToken !== TF_WEBHOOK_TOKEN) {
        console.warn('Unauthorized webhook access: Token mismatch.');
        // Return a 403 Forbidden response
        return res.status(403).send('El Token recibido no coincide con el esperado');
    }

    // 3. Token is valid, process the webhook data
    const data = req.body; // The parsed JSON body of the webhook

    if (!data) {
        console.error('No JSON data received in webhook request.');
        return res.status(400).send('No se recibió información en formato JSON.');
    }

    console.log('Webhook data:', data);

    // Call your function to consult info based on external_reference
    // In a real application, this would involve database operations,
    // calling external APIs, or other backend logic.
    // We'll use a try-catch block for robust error handling.
    try {
        // Ensure 'external_reference' exists in the payload
        const externalReference = data.external_reference; // Access directly from parsed JSON object
        if (externalReference) {
            consultarPorExtRef(externalReference);
        } else {
            console.warn("Webhook data missing 'external_reference' key.");
        }

        // 4. Respond with 200 OK to prevent re-attempts from TusFacturasAPP
        console.log('Webhook processed successfully. Sending 200 OK.');
        res.status(200).send('OK');
    } catch (error) {
        console.error('Error processing webhook:', error);
        // For webhook handlers, sending 200 OK even on internal processing errors
        // is often desired to acknowledge receipt and prevent re-attempts from sender.
        // Handle the error internally.
        res.status(200).send('OK (processed with internal error)');
    }
});

// --- Helper Function (simulating PHP's consultar_por_ext_ref) ---
/**
 * Simulates a function to consult information associated with an external reference.
 * In a real scenario, this would likely be an async operation (e.g., database query, API call).
 * @param {string} extRef The external reference from the webhook.
 */
function consultarPorExtRef(extRef) {
    console.log(`Consulting info for external_reference: ${extRef}`);
    // Implement your actual logic here (e.g., call TusFacturasAPP API, update database)
    // This function can be async if it involves promises (e.g., network requests, database calls)
    // Example:
    // return new Promise(resolve => {
    //     setTimeout(() => {
    //         console.log(`Information for ${extRef} consulted.`);
    //         resolve();
    //     }, 100); // Simulate network delay
    // });
}

// --- Start the server ---
app.listen(port, () => {
    console.log(`Node.js Webhook listener running on http://localhost:${port}`);
    console.log('Remember to expose this server to the internet if TusFacturasAPP needs to reach it!');
});

```
{% endtab %}

{% tab title="Ruby" %}
```ruby
# Import necessary gems
require 'sinatra'
require 'json' # To parse incoming JSON bodies

# --- Configuration ---
# Your secret token from TusFacturasAPP
# It's better practice to load this from environment variables (e.g., ENV['TF_WEBHOOK_TOKEN'])
TF_WEBHOOK_TOKEN = 'TOKEN_TF'

# Set the port for your webhook listener
# This can also be set via environment variable: PORT=4567 ruby app.rb
set :port, 4567

# Disable Sinatra's default error pages for a cleaner response
disable :show_exceptions
disable :raise_errors

# --- Webhook Endpoint ---
# This is the URL where TusFacturasAPP will send webhooks (e.g., http://yourserver.com:4567/webhook)
post '/webhook' do
  puts 'Webhook received!'

  # 1. Get the token from the request headers
  # Headers in Rack (which Sinatra uses) are prefixed with HTTP_ and uppercase,
  # with hyphens converted to underscores.
  header_token = request.env['HTTP_TF_WEBHOOKTOKEN']

  # 2. Validate the token
  if header_token != TF_WEBHOOK_TOKEN
    warn 'Unauthorized webhook access: Token mismatch.'
    status 403 # Set HTTP status code to 403 Forbidden
    body 'El Token recibido no coincide con el esperado'
    return # Stop processing
  end

  # 3. Token is valid, process the webhook data
  # request.body is an IO object, read its content
  request_body = request.body.read
  data = nil
  begin
    data = JSON.parse(request_body)
  rescue JSON::ParserError => e
    warn "Invalid JSON received: #{e.message}"
    status 400 # Bad Request
    body 'No se recibió información válida en formato JSON.'
    return
  end

  puts "Webhook data: #{data}"

  # Call your function to consult info based on external_reference
  # In a real application, this would involve database operations,
  # calling external APIs, or other backend logic.
  # We'll use a begin-rescue block for robust error handling.
  begin
    # Ensure 'external_reference' exists in the payload
    external_reference = data['external_reference'] # Access directly from parsed JSON hash
    if external_reference
      consultar_por_ext_ref(external_reference)
    else
      warn "Webhook data missing 'external_reference' key."
    end

    # 4. Respond with 200 OK to prevent re-attempts from TusFacturasAPP
    puts 'Webhook processed successfully. Sending 200 OK.'
    status 200 # Set HTTP status code to 200 OK
    body 'OK'
  rescue StandardError => e
    warn "Error processing webhook: #{e.message}"
    # For webhook handlers, sending 200 OK even on internal processing errors
    # is often desired to acknowledge receipt and prevent re-attempts from sender.
    # Handle the error internally.
    status 200
    body 'OK (processed with internal error)'
  end
end

# --- Helper Function (simulating PHP's consultar_por_ext_ref) ---
# This is a synchronous function for simplicity, but in a real app,
# it might involve network requests or database calls that could be async.
def consultar_por_ext_ref(ext_ref)
  puts "Consulting info for external_reference: #{ext_ref}"
  # Implement your actual logic here (e.g., call TusFacturasAPP API, update database)
  # Example:
  # some_api_client.fetch_data(ext_ref)
end


```
{% endtab %}
{% endtabs %}

### **Información sobre Webhooks:**&#x20;

Para una comprensión completa de cómo integrar y utilizar el webhook, [**consultá la documentación detallada desde aquí.**](../api-factura-electronica-afip-facturacion-ventas/webhooks-notificaciones.md)

***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).&#x20;

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
