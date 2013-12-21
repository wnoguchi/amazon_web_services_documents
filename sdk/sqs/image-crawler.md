Amazon SQS: Image Crawler
==============================

実装
------------------------------

### 下ごしらえ

* 定数定義

```php
define('URL_QUEUE', 'c_url');
define('PARSE_QUEUE', 'c_parse');
define('IMAGE_QUEUE', 'c_image');
define('RENDER_QUEUE', 'c_render');
```

* キューを作成

```
php create_queues.php c_url c_parse c_image c_render
```

### キューから次のメッセージを取り出す関数の作成

削除しない。

```php
// TODO
```

参考サイト
------------------------------

- [Amazon Simple Queue Service — AWS SDK for PHP 2.4.11 documentation](http://docs.aws.amazon.com/aws-sdk-php/guide/latest/service-sqs.html)
- [Class Aws\Sqs\SqsClient | AWS SDK for PHP](http://docs.aws.amazon.com/aws-sdk-php/latest/class-Aws.Sqs.SqsClient.html)
