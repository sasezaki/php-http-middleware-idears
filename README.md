PHP HTTP Middleware Ideas - interface, signature
===========================================

a collection of PHP HTTP `middleware` ideas


## Stack

|implements  |Symfony\Component\HttpKernel\HttpKernelInterface|
|----------- |--------------------------------------------------|

|require     |symfony/http-foundation, symfony/http-kernel      |
|----------- |--------------------------------------------------|
  
``` php
/** @return Symfony\Component\HttpFoundation\Response */
public function handle(Request $request, $type = self::MASTER_REQUEST, $catch = true) {}
```
  - http://stackphp.com/


## zend-stratigility, Slim 3 etc.

|implements  |`none`                 |
|----------- |--------------------------------------------------|

|require     |psr/http-message       |
|----------- |--------------------------------------------------|
 


#### signature

```php
/** @return Psr\Http\Message\ResponseInterface */
function ($req, $res, $next) {}
```


  - https://zendframework.github.io/zend-stratigility/middleware/
  - http://www.slimframework.com/docs/concepts/middleware.html

## PSR-15, http-interop


|server implements  |Interop\Http\Middleware\ServerMiddlewareInterface|
|----------- |--------------------------------------------------|


|client implements  |Interop\Http\Middleware\MiddlewareInterface      |
|----------- |--------------------------------------------------|

|require     |psr/http-message                                 |
|----------- |--------------------------------------------------|


```php

interface ServerMiddlewareInterface
{
    /** @return Psr\Http\Message\ResponseInterface */
    public function process(ServerRequestInterface $request, DelegateInterface $delegate);
}
```

```php
interface MiddlewareInterface
{
    /** @return Psr\Http\Message\ResponseInterface */
    public function process(RequestInterface $request, DelegateInterface $delegate);
}
```

  - https://github.com/http-interop/http-middleware

## ircmaxell/tari-php

|require     |psr/http-message       |
|----------- |-----------------------|

   - https://github.com/ircmaxell/Tari-PHP
   
```php
interface ServerMiddlewareInterface {
    public function handle(ServerRequestInterface $request, ServerFrameInterface $frame): ResponseInterface;
}
```

## n1215/http-context

|require     |psr/http-message       |
|----------- |-----------------------|

  - https://github.com/n1215/http-context
  - http://nextat.co.jp/staff/archives/152

## beberlei/http-client-middleware

|require     |psr/http-message       |
|----------- |-----------------------|

  - https://github.com/beberlei/http-client-middleware

```php
interface ClientInterface
{
    /** @return Psr\Http\Message\ResponseInterface */
    public function send(RequestInterface $request, array $options = []);
}
```

```php
<?php
interface AsyncClientInterface
{
    /** @return PromiseInterface */
    public function sendAsync(RequestInterface $request, array $options = []);

    /** @return PromiseInterface */
    public function requestAsync($method, $uri, array $options = []);
}

```

## guzzlehttp/guzzle

|require     |psr/http-message, guzzlehttp/guzzle(as handler ?)|
|----------- |-------------------------------------------------|

  - http://docs.guzzlephp.org/en/latest/handlers-and-middleware.html#middleware

## php-api-clients/middleware

|require|psr/http-message, react/promise?      |
|------- |-----------------------|

```php
interface MiddlewareInterface
{
    public function pre(RequestInterface $request, array $options = []): CancellablePromiseInterface;
    public function post(ResponseInterface $response, array $options = []): CancellablePromiseInterface;
}
```

  - https://github.com/php-api-clients/middleware


# References
  - http://blog.ircmaxell.com/2016/05/all-about-middleware.html
