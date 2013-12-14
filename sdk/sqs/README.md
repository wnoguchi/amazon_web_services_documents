Amazon SQS Development
==============================

Amazon Simple Queue Service.

レシピ
------------------------------

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

### キューにアイテムを挿入する

* `post_queue.php`

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
  exit("Usage: " . $argv[0] . " QUEUE_NAME ITEM...\n");
}

$queue = $argv[1];
$result = $client->createQueue(array(
  'QueueName' => $queue,
));
$queueUrl = $result->get('QueueUrl');

for ($i = 2; $i < count($argv); $i++)
{
  $message = $argv[$i];
  
  try {
    $result = $client->sendMessage(array(
      'QueueUrl'    => $queueUrl,
      'MessageBody' => 'An awesome message!',
    ));
    
    $messageId = $result->get('MessageId');
    echo "Posted to $queue ${messageId}: $message\n";

  } catch (Exception $ex) {
    exit("Could not post message to " . $queue . ": " . $message . $ex->getMessage() . "\n");
  }
  
  echo "Queue: $queue has been created: ${queueUrl}\n";
}

echo "finished!\n";
```

* 結果

```
php post_queue.php aaa hello goodnigt goodmorning
Posted to aaa 83b89bc8-00b9-4542-8424-279500c9abf0: hello
Queue: aaa has been created: https://sqs.ap-northeast-1.amazonaws.com/585028639641/aaa
Posted to aaa 110237f6-6af5-4523-a6f9-3da4eef25212: goodnigt
Queue: aaa has been created: https://sqs.ap-northeast-1.amazonaws.com/585028639641/aaa
Posted to aaa dd8ef2ea-8a7b-444a-8639-8a265a827b05: goodmorning
Queue: aaa has been created: https://sqs.ap-northeast-1.amazonaws.com/585028639641/aaa
finished!
```

参考サイト
------------------------------

- [Amazon Simple Queue Service — AWS SDK for PHP 2.4.11 documentation](http://docs.aws.amazon.com/aws-sdk-php/guide/latest/service-sqs.html)
- [Class Aws\Sqs\SqsClient | AWS SDK for PHP](http://docs.aws.amazon.com/aws-sdk-php/latest/class-Aws.Sqs.SqsClient.html)
