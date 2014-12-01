# PHP cURL

Specify the certificate of the server you want to communicate with in cert.pem. cURL will only communicate with this server and will ignore the local certificate store.

``` php
<?php
error_reporting(E_ALL);
ini_set("display_errors", 1);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://localhost:4433");
curl_setopt($ch, CURLOPT_CAINFO, getcwd() . "/cert.pem");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($ch);
echo $response;
curl_close($ch);

```

## Error Handling

In the event that the certificate presented by the server fails validation, the result "false" will be returned in place of $response. Your application must check the result of curl_exec() before using the response.
