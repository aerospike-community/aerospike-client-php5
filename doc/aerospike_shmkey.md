
# Aerospike::shmKey

Aerospike::shmKey - exposes the shared memory key used for storage by
shared-memory cluster tending.

## Description

```
public int|null Aerospike::shmKey ( void )
```

If shm cluster tending is enabled, **Aerospike::shmKey** will return the value
of the shm key being used by the client. If it was set explicitly under the
client's *shm* config parameter, or through the global `aerospike.shm.key` we
expect to see that value. Otherwise the implicit value generated by the client
will be returned.

## Return Values

Returns an integer shared memory identifier. Default: `0xA5000000`.
If shared-memory cluster tending was not enabled the return value will be NULL.

## Examples

```php
<?php

$config = ["hosts" => [["addr"=>"localhost", "port"=>3000]],
           "shm"=> [
             "shm_key" => 0xA5000001]];
$client = new Aerospike($config, true);
if (!$client->isConnected()) {
   echo "Aerospike failed to connect[{$client->errorno()}]: {$client->error()}\n";
   exit(1);
}
$shared_memory_key = $client->shmKey();
var_dump($shared_memory_key);

?>
```

we expect to see:

```
2768240641
```

