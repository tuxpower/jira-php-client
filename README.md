# jira-php-client
PHP client to interact with the JIRA API.

We're slowly building out this client as we need the functionality. Initially we only need it for managing user accounts.

This client is built on top of [Guzzle](http://docs.guzzlephp.org/en/latest/index.html), the PHP HTTP Client.
Guzzle has a simple way to create API clients by describing the API in a Swagger-like format without the need to implement 
every method yourself. So adding support for more JIRA APIs is relatively simple. If you want to submit a pull request
to add another feature, please do. If you don't know how to do that, ask us and we might be able to add it in for you.

# JIRA API Authentication #
JIRA uses Basic Auth to authenticate API calls. You must provide the username and password for your API user 
via parameters ```apiuser``` and ```apipass```.

# Install #
Installation is simple with [Composer](https://getcomposer.org/). 
Add ```"silinternational/jira-php-client": "dev-master"``` to your ```composer.json``` file and update.

# Usage #
Example:

```php

<?php

use JIRA\Client;

$client = new Client([
  'apiuser' => 'username',
  'apipass' => 'password',
]);

$user = $client->getUser(['userId' => 123456789]);

echo $user['email'];
// example@domain.org

$newUser = $client->addUser([
  "name" => "test_user",
  "password" => "newpassword",
  "emailAddress" => "test_user@domain.org",
  "displayName" => "test user",
]);

echo $user['data']['userId'];
// 1234567890

```

If you host your own JIRA Enterprise server you can override the default API url:

```php
<?php

use JIRA\Client;

$client = new Client([
  'apiuser' => 'username',
  'apipass' => 'password',
  'description_override' => [
    'baseUrl' => 'https://my.server.com',
  ],
]);

```

## Guzzle Service Client Notes ##
- Presentation by Jeremy Lindblom: https://speakerdeck.com/jeremeamia/building-web-service-clients-with-guzzle-1
- Example by Jeremy Lindblom: https://github.com/jeremeamia/sunshinephp-guzzle-examples
- Parameter docs in source comments: https://github.com/guzzle/guzzle-services/blob/master/src/Parameter.php
