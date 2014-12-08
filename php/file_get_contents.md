# PHP file_get_contents()

``` php
<?php
$options = array(
    'ssl' => array(
        'CN_match' => 'localhost',
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