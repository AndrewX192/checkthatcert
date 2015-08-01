# PHP file_get_contents()

Specify the certificate of the server you want to communicate with in cert.pem.

``` php
<?php
$options = array(
    'ssl' => array(
        'verify_peer' => true,
        'verify_peer_name' => true,
        'SNI_enabled' => true,
        'cafile' => '../cert.pem',
    ),
);
$context = stream_context_create($options);

$result = file_get_contents("https://127.0.0.1:4433", false, $context);

if ($result !== false) {
  echo $result;
}
```

## PHP 5.5 Notes

Tested on PHP 5.5.26 (cli) (built: Jun 11 2015 08:23:07) 

### Certificate Validation is not default

$ php -r 'echo file_get_contents("https://localhost:4433");'
<HTML><BODY BGCOLOR="#ffffff">

###
