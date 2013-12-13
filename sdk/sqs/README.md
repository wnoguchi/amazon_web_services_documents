# Amazon SQS Development

Amazon Simple Queue Service.

## レシピ

### キューを作成する

* `awssecure.php`

```php
<?php
// AWSアクセストークン
$config = array(
  'key'    => 'AKIAIOSFODNN7EXAMPLE',
  'secret' => 'wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY'
  'region' => \Aws\Common\Enum\Region::AP_NORTHEAST_1,
);
```

* `create_queue.php`

```php
<?php

error_reporting(E_ALL);

// Composer
require_once('vendor/autoload.php');
// AWS
require_once('include/awssecure.inc.php');

require_once('include/book.inc.php');

use Aws\Sqs\SqsClient;

$client = SqsClient::factory($config);

if (count($argv) < 2)
{
    exit("Usage: " . $argv[0] . " QUEUE...\n");
}

for ($i = 1; $i < count($argv); $i++)
{
    $queue = $argv[$i];
    
    try {
        $result = $client->createQueue(array(
            'QueueName' => $queue,
        ));
    } catch (Exception $ex) {
        exit("error while creating queue: " . $queue . ": " . $ex->getMessage() . "\n");
    }
    
    $queueUrl = $result->get('QueueUrl');
    echo "Queue: $queue has been created: ${queueUrl}\n";
}

echo "finished!\n";
```

* 結果

```
$ php create_queues.php aaa bbb ccc
Queue: aaa has been created: https://sqs.ap-northeast-1.amazonaws.com/585028639641/aaa
Queue: bbb has been created: https://sqs.ap-northeast-1.amazonaws.com/585028639641/bbb
Queue: ccc has been created: https://sqs.ap-northeast-1.amazonaws.com/585028639641/ccc
finished!
```

### キューの一覧を表示する

* `list_queues.php`

```php
<?php

error_reporting(E_ALL);

// Composer
require_once('vendor/autoload.php');
// AWS
require_once('include/awssecure.inc.php');

require_once('include/book.inc.php');

use Aws\Sqs\SqsClient;

$client = SqsClient::factory($config);

try {
    $result = $client->listQueues();
} catch (Exception $ex) {
    exit("error list queue: " . $ex->getMessage() . "\n");
}

$queueUrlList = $result->get('QueueUrls');

foreach ($queueUrlList as $queue)
{
    echo "Queue: ${queue}\n";
}

echo "finished!\n";
```

* 結果

```
$ php list_queues.php
Queue: https://sqs.ap-northeast-1.amazonaws.com/585028639641/aaa
Queue: https://sqs.ap-northeast-1.amazonaws.com/585028639641/bbb
Queue: https://sqs.ap-northeast-1.amazonaws.com/585028639641/ccc
finished!
```

## 参考サイト

- [Amazon Simple Queue Service — AWS SDK for PHP 2.4.11 documentation](http://docs.aws.amazon.com/aws-sdk-php/guide/latest/service-sqs.html)
- [Class Aws\Sqs\SqsClient | AWS SDK for PHP](http://docs.aws.amazon.com/aws-sdk-php/latest/class-Aws.Sqs.SqsClient.html)
