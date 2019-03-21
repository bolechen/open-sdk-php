# open-sdk-php

[![Latest Version on Packagist][ico-version]][link-packagist]
[![Software License][ico-license]](LICENSE.md)
[![Total Downloads][ico-downloads]][link-downloads]

Youzan Open SDK


## NOTICE

有赞开放平台升级为有赞云，开发者需要进行迁移工作，此为兼容版本SDK，理论上可以无痛迁移(只需更改引入包版本)，但依然强烈建议你在生产环境迁移前进行充分的测试！


## Install

Via Composer

``` bash
$ composer require xu42/open-sdk "dev-compatible"
```


## Usage

### 1. 获取 accessToken

#### 工具型应用
``` php
require_once './vendor/autoload.php';

$clientId = "fill your client_id";
$clientSecret = "fill your client_secret";
$redirectUrl = "fill your redirect_url";

$type = 'oauth';  //如要刷新access_token，type值为refresh_token
$keys['code'] = $_GET['code'];  //如要刷新access_token，这里为$keys['refresh_token']
$keys['redirect_uri'] = $redirect_url;

$accessToken = (new \Youzan\Open\Token($clientId, $clientSecret))->getToken($type, $keys);
var_dump($accessToken);
```

#### 自用型应用
``` php
require_once './vendor/autoload.php';

$clientId = "fill your client_id";
$clientSecret = "fill your client_secret";

$type = 'self';
$keys['kdt_id'] = '160';

$accessToken = (new \Youzan\Open\Token($clientId, $clientSecret))->getToken($type, $keys);
var_dump($accessToken);
```

#### 平台型应用获取初始化token
``` php
require_once './vendor/autoload.php';

$clientId = "fill your client_id";
$clientSecret = "fill your client_secret";

$type = 'platform_init';

$accessToken = (new \Youzan\Open\Token($clientId, $clientSecret))->getToken($type);
var_dump($accessToken);
```

#### 平台型应用获取店铺token
``` php
require_once './vendor/autoload.php';

$clientId = "fill your client_id";
$clientSecret = "fill your client_secret";

$type = 'platform';
$keys['kdt_id'] = '160';

$accessToken = (new \Youzan\Open\Token($clientId, $clientSecret))->getToken($type, $keys);
var_dump($accessToken);
```

### 2. 接口调用示例1
``` php
require_once './vendor/autoload.php';
$accessToken = 'fill your token';
$client = new \Youzan\Open\Client($accessToken);

$method = 'youzan.item.get';
$apiVersion = '3.0.0';

$params = [
    'alias' => 'fa8989ad342k',
];

$response = $client->get($method, $apiVersion, $params);
var_dump($response);
```

### 2. 接口调用示例2
``` php
require_once './vendor/autoload.php';
$accessToken = 'fill your token';
$client = new \Youzan\Open\Client($accessToken);

$method = 'youzan.materials.storage.platform.img.upload';
$apiVersion = '3.0.0';

$params = [
    'alias' => 'fa8989ad342k',
];

$files = [
    [
        'url' => __DIR__ . '/test1.png',
        'field' => 'image[]',
    ],
];

$response = $client->post($method, $apiVersion, array(), $files);
var_dump($response);
```

## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.


## Security

If you discover any security related issues, please using the issue tracker.


## License

The MIT License. Please see [License File](LICENSE.md) for more information.

[ico-version]: https://img.shields.io/packagist/v/xu42/open-sdk.svg?style=flat-square
[ico-license]: https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square
[ico-downloads]: https://img.shields.io/packagist/dt/xu42/open-sdk.svg?style=flat-square

[link-packagist]: https://packagist.org/packages/xu42/open-sdk
[link-downloads]: https://packagist.org/packages/xu42/open-sdk