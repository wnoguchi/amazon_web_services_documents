# Amazon S3 Development

## 準備

* Composerのインストール

```
curl -s http://getcomposer.org/installer | php

#!/usr/bin/env php
All settings correct for using Composer
Downloading...

Composer successfully installed to: /var/www/aws/s3/composer.phar
Use it: php composer.phar
```

ここで `composer.phar` がカレントに作成される。

* `composer.json` の作成

```json
{
  "require": {
    "aws/aws-sdk-php": "*"
  }
}
```

* Composerで依存パッケージのインストール

ここで `composer.json` に記述された依存パッケージがインストールされる。

```
php composer.phar install

Loading composer repositories with package information
Installing dependencies (including require-dev)
Your requirements could not be resolved to an installable set of packages.

  Problem 1
    - aws/aws-sdk-php 2.4.0 requires guzzle/guzzle ~3.7.0 -> satisfiable by guzzle/guzzle[v3.7.0, v3.7.1, v3.7.2, v3.7.3, v3.7.4].
    - aws/aws-sdk-php 2.4.1 requires guzzle/guzzle ~3.7.0 -> satisfiable by guzzle/guzzle[v3.7.0, v3.7.1, v3.7.2, v3.7.3, v3.7.4].
    - aws/aws-sdk-php 2.4.10 requires guzzle/guzzle ~3.7.0 -> satisfiable by guzzle/guzzle[v3.7.0, v3.7.1, v3.7.2, v3.7.3, v3.7.4].
    - aws/aws-sdk-php 2.4.11 requires guzzle/guzzle ~3.7.0 -> satisfiable by guzzle/guzzle[v3.7.0, v3.7.1, v3.7.2, v3.7.3, v3.7.4].
    - aws/aws-sdk-php 2.4.2 requires guzzle/guzzle ~3.7.0 -> satisfiable by guzzle/guzzle[v3.7.0, v3.7.1, v3.7.2, v3.7.3, v3.7.4].
    - aws/aws-sdk-php 2.4.3 requires guzzle/guzzle ~3.7.0 -> satisfiable by guzzle/guzzle[v3.7.0, v3.7.1, v3.7.2, v3.7.3, v3.7.4].
    - aws/aws-sdk-php 2.4.4 requires guzzle/guzzle ~3.7.0 -> satisfiable by guzzle/guzzle[v3.7.0, v3.7.1, v3.7.2, v3.7.3, v3.7.4].
    - aws/aws-sdk-php 2.4.5 requires guzzle/guzzle ~3.7.0 -> satisfiable by guzzle/guzzle[v3.7.0, v3.7.1, v3.7.2, v3.7.3, v3.7.4].
    - aws/aws-sdk-php 2.4.6 requires guzzle/guzzle ~3.7.0 -> satisfiable by guzzle/guzzle[v3.7.0, v3.7.1, v3.7.2, v3.7.3, v3.7.4].
    - aws/aws-sdk-php 2.4.7 requires guzzle/guzzle ~3.7.0 -> satisfiable by guzzle/guzzle[v3.7.0, v3.7.1, v3.7.2, v3.7.3, v3.7.4].
    - aws/aws-sdk-php 2.4.8 requires guzzle/guzzle ~3.7.0 -> satisfiable by guzzle/guzzle[v3.7.0, v3.7.1, v3.7.2, v3.7.3, v3.7.4].
    - aws/aws-sdk-php 2.4.9 requires guzzle/guzzle ~3.7.0 -> satisfiable by guzzle/guzzle[v3.7.0, v3.7.1, v3.7.2, v3.7.3, v3.7.4].
    - aws/aws-sdk-php 2.3.4 requires guzzle/guzzle ~3.6.0 -> satisfiable by guzzle/guzzle[v3.6.0].
    - aws/aws-sdk-php 2.3.1 requires guzzle/guzzle ~3.4.3 -> satisfiable by guzzle/guzzle[v3.4.3].
    - aws/aws-sdk-php 2.3.2 requires guzzle/guzzle >=3.4.3,<4 -> satisfiable by guzzle/guzzle[v3.4.3, v3.5.0, v3.6.0, v3.7.0, v3.7.1, v3.7.2, v3.7.3, v3.7.4].
    - aws/aws-sdk-php 2.3.3 requires guzzle/guzzle >=3.4.3,<4 -> satisfiable by guzzle/guzzle[v3.4.3, v3.5.0, v3.6.0, v3.7.0, v3.7.1, v3.7.2, v3.7.3, v3.7.4].
    - aws/aws-sdk-php 2.3.0 requires guzzle/guzzle ~3.4.1 -> satisfiable by guzzle/guzzle[v3.4.1, v3.4.2, v3.4.3].
    - aws/aws-sdk-php 2.2.0 requires guzzle/guzzle ~3.3.0 -> satisfiable by guzzle/guzzle[v3.3.0, v3.3.1].
    - aws/aws-sdk-php 2.2.1 requires guzzle/guzzle ~3.3.0 -> satisfiable by guzzle/guzzle[v3.3.0, v3.3.1].
    - aws/aws-sdk-php 2.1.1 requires guzzle/guzzle ~3.2.0 -> satisfiable by guzzle/guzzle[v3.2.0].
    - aws/aws-sdk-php 2.1.2 requires guzzle/guzzle ~3.2.0 -> satisfiable by guzzle/guzzle[v3.2.0].
    - aws/aws-sdk-php 2.1.0 requires guzzle/guzzle ~3.1.2 -> satisfiable by guzzle/guzzle[v3.1.2].
    - aws/aws-sdk-php 2.0.0 requires guzzle/guzzle 3.0.* -> satisfiable by guzzle/guzzle[v3.0.0, v3.0.1, v3.0.2, v3.0.3, v3.0.4, v3.0.5, v3.0.6, v3.0.7].
    - aws/aws-sdk-php 2.0.1 requires guzzle/guzzle 3.0.* -> satisfiable by guzzle/guzzle[v3.0.0, v3.0.1, v3.0.2, v3.0.3, v3.0.4, v3.0.5, v3.0.6, v3.0.7].
    - aws/aws-sdk-php 2.0.2 requires guzzle/guzzle 3.0.* -> satisfiable by guzzle/guzzle[v3.0.0, v3.0.1, v3.0.2, v3.0.3, v3.0.4, v3.0.5, v3.0.6, v3.0.7].
    - aws/aws-sdk-php 2.0.3 requires guzzle/guzzle 3.0.* -> satisfiable by guzzle/guzzle[v3.0.0, v3.0.1, v3.0.2, v3.0.3, v3.0.4, v3.0.5, v3.0.6, v3.0.7].
    - guzzle/guzzle v3.7.4 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.7.3 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.7.2 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.7.1 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.7.0 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.6.0 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.5.0 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.4.3 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.4.2 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.4.1 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.3.1 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.3.0 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.2.0 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.1.2 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.0.7 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.0.6 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.0.5 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.0.4 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.0.3 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.0.2 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.0.1 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - guzzle/guzzle v3.0.0 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - Installation request for aws/aws-sdk-php * -> satisfiable by aws/aws-sdk-php[2.0.0, 2.0.1, 2.0.2, 2.0.3, 2.1.0, 2.1.1, 2.1.2, 2.2.0, 2.2.1, 2.3.0, 2.3.1, 2.3.2, 2.3.3, 2.3.4, 2.4.0, 2.4.1, 2.4.10, 2.4.11, 2.4.2, 2.4.3, 2.4.4, 2.4.5, 2.4.6, 2.4.7, 2.4.8, 2.4.9].

```

んー、PHPのcurl拡張がないって言ってる？

```
sudo apt-get -y install php5-curl
```

もういっかい。

```
Loading composer repositories with package information
Installing dependencies (including require-dev)
  - Installing symfony/event-dispatcher (v2.3.7)
    Downloading: 100%         

  - Installing guzzle/guzzle (v3.7.4)
    Downloading: 100%         

  - Installing aws/aws-sdk-php (2.4.11)
    Downloading: 100%         

symfony/event-dispatcher suggests installing symfony/dependency-injection ()
symfony/event-dispatcher suggests installing symfony/http-kernel ()
aws/aws-sdk-php suggests installing doctrine/cache (Adds support for caching of credentials and responses)
aws/aws-sdk-php suggests installing ext-apc (Allows service description opcode caching, request and response caching, and credentials caching)
aws/aws-sdk-php suggests installing monolog/monolog (Adds support for logging HTTP requests and responses)
aws/aws-sdk-php suggests installing symfony/yaml (Eases the ability to write manifests for creating jobs in AWS Import/Export)
Writing lock file
Generating autoload files
```

OKっぽい。

* `awssecure.inc.php`

```php
<?php
// AWSアクセストークン
$config = array(
  'key'    => 'AKIAIOSFODNN7EXAMPLE',
  'secret' => 'wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY'
);
```

gitで管理するときはこのファイルのトラッキングを外しましょう。
ただ、テンプレート的なファイルだけは残っていてほしいのでインデックスから無視するようにします。

```
git update-index --skip-worktree awssecure.inc.php
```

* `s3_list_buckets.php`

```php
<?php
require_once("vendor/autoload.php");
require_once("awssecure.inc.php");

use Aws\S3\S3Client;

$s3 = S3Client::factory($config);

?><!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="utf-8">
<title></title>
<meta name="keywords" content="">
<meta name="description" content="">
<script
src="http://ajax.googleapis.com/ajax/libs/jquery/1/jquery.min.js"></script>
</head>
<body>
<?php
$buckets= $s3->listBuckets();

?>
<pre>
<?php
foreach ($buckets as $bucket)
{
  var_dump($bucket);
}
?>
</pre>
</body>
</html>
```

これでOKです。

どうやら本に載っている `new AmazonS3()` とかの記述は AWS SDK for PHP のもので、
上で紹介しているのは AWS SDK for PHP 2のようだ・・・。  
どうりでまるっきり書き方が違うわけだ・・・。

AWS Management Console上でしかS3を使っていなかったから気が付かなかったけど、バケットを作成するときにリージョン指定することができるんだね。今までずっとデフォルトでバケットを作成してたからダウンロードものすごく遅かったんだけど、東京リージョンでバケット作ってダウンロードするようにしたら速くなるんだろうか。そうすればCloudFrontはつかわなくてもよくなるのかな？どうなんだろう。

## レシピ

以下の記述はAWS SDK for PHP2のものです。

### バケットを作成してみる

* `include/book.inc.php`

```php
<?php
define('BOOK_BUCKET', 'sitepoint-aws-cloud-book-wnoguchi');
```

* `create_bucket.php`

```php
<?php

error_reporting(E_ALL);

// Composer
require_once('vendor/autoload.php');
// AWS
require_once('awssecure.inc.php');

require_once('include/book.inc.php');

use Aws\S3\S3Client;

$s3 = S3Client::factory($config);

$res = $s3->createBucket(array(
  'Bucket' => BOOK_BUCKET,
  // Tokyo Region
  'LocationConstraint' => \Aws\Common\Enum\Region::AP_NORTHEAST_1,
));

if (!empty($res))
{
  echo $res["Location"] . "\n";
  echo $res["RequestId"] . "\n";
  echo "'" . BOOK_BUCKET . "' bucket created.\n";
}
```

これから先はこのあたりが参考になりそう。

- [AWS/S3 - Ebisawa's Wiki](http://www.ebisawa.co.jp/wiki/index.php?AWS%2FS3)

Composerでlog4phpを入れたいんだけど、

- [gist:7838085](https://gist.github.com/wnoguchi/7838085)

## CloudFrontを使ってみる

AWS Management Consoleでディストリビューションを作成する。  
OriginにS3のバケットを選択して作成。ステータスがDeployedとなれば完了。  
URLはDomain NameにS3のバケットのルートパスからそのまま記述すればOK。

例えば

```
https://foobarbucket-wnoguchi.s3-ap-northeast-1.amazonaws.com/hoge/tumblr_mqp9pnVFZo1qg2hlto1_500.gif
```

なら

```
http://abcdefghijk01234.cloudfront.net/hoge/tumblr_mqp9pnVFZo1qg2hlto1_500.gif
```

となる。

さて、CloudFrontディストリビューションの一覧を作成するなら以下のようになる。

```php
<?php

error_reporting(E_ALL);

// Composer
require_once('vendor/autoload.php');
// AWS
require_once('include/awssecure.inc.php');

require_once('include/book.inc.php');

use Aws\CloudFront\CloudFrontClient;

$cf = CloudFrontClient::factory($config);

$distributionList = $cf->listDistributions();

printf ("%-16s %-32s %-40s\n", "ID", "Domain Name", "Origin");
printf ("%'=-16s %'=-32s %'=-40s\n", "", "", "");

foreach ($distributionList['Items'] as $k => $v)
{
  $id = $v['Id'];
  $domainName = $v['DomainName'];
  $origin = $v['Origins']['Items'][0]['DomainName'];

  printf ("%-16s %-32s %-40s\n", $id, $domainName, $origin);
}
```

- [Class Aws\CloudFront\CloudFrontClient | AWS SDK for PHP](http://docs.aws.amazon.com/aws-sdk-php/latest/class-Aws.CloudFront.CloudFrontClient.html#_listDistributions)

## 参考サイト

- [AWS SDK for PHP 2のインストール 〜 S3のバケット一覧取得まで - developer's diary](http://devlog.mitsugeek.net/entry/2013/06/13/AWS_SDK_for_PHP_2%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB_%E3%80%9C_S3%E3%81%AE%E3%83%90%E3%82%B1%E3%83%83%E3%83%88%E4%B8%80%E8%A6%A7%E5%8F%96%E5%BE%97%E3%81%BE%E3%81%A7)
- [既に git 管理しているファイルをあえて無視したい - Qiita [キータ]](http://qiita.com/usamik26/items/56d0d3ba7a1300625f92)
- [Amazon Simple Storage Service — AWS SDK for PHP 2.4.11 documentation](http://docs.aws.amazon.com/aws-sdk-php/guide/latest/service-s3.html)
- [AWS SDK for PHP 1.6.2](http://docs.aws.amazon.com/AWSSDKforPHP/latest/index.html#m=AmazonS3/create_bucket)
- [AWS SDK for PHP — AWS SDK for PHP 2.4.11 documentation](http://docs.aws.amazon.com/aws-sdk-php/guide/latest/index.html)
- [Migration Guide — AWS SDK for PHP 2.4.11 documentation](http://docs.aws.amazon.com/aws-sdk-php/guide/latest/migration-guide.html)

