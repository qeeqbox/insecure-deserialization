<p align="center"> <img src="https://raw.githubusercontent.com/qeeqbox/insecure-deserialization/main/xslt-injectinsecure-deserializationion.png"></p>

A threat actor may tamper with a stream that gets deserialized on the target causing the target to access data or perform non-intended actions

## Example #1
1. An application sends serialized user's settings in a http request to backend api
2. A threat actor finds out how the serialization works, and inject malicious actions with settings
3. The backend api deserialize the request and perform threat actor's actions

## Code
#### Target-Logic
```php
<?php
class Info{
  public $username;
  public $admin;
}
$user = new Info;
$user->username = 'Victim';
$user->admin = FALSE;
$Info = unserialize($user);
echo $Info->admin
?>
```

#### Target-In
```php
 O:4:"Info":2:{s:8:"username";s:6:"Victim";s:5:"admin";b:1;} 
```

#### Target-Out
```
Admin: True
```

## Impact
High

## Names
- Insecure deserialization
- Untrusted deserialization

## Risk
- Read & modify data

## Redemption
- Use pure data format
- Deserialize signed data only

## ID
a244242a-a9d5-47e0-9c01-86eecdf073ea

## References
- (Wikipedia)[https://en.wikipedia.org/wiki/Serialization]