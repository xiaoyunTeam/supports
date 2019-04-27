<h1 align="center">xiaoyun.studio/supports</h1>

handle with array/config/log/guzzle etc.

## About log

### Register

#### Method 1

A application logger can extends `XiaoYun\Supports\Log` and modify `createLogger` method, the method must return instance of `Monolog\Logger`.

```PHP
use XiaoYun\Supports\Log;
use Monolog\Logger;

class APPLICATIONLOG extends Log
{
    /**
     * Make a default log instance.
     *
     * @author XiaoYun <shustudio@yeah.net>
     *
     * @return Logger
     */
    public static function createLogger()
    {
        $handler = new StreamHandler('./log.log');
        $handler->setFormatter(new LineFormatter("%datetime% > %level_name% > %message% %context% %extra%\n\n"));

        $logger = new Logger('XiaoYun.private_number');
        $logger->pushHandler($handler);

        return $logger;
    }
}
```

#### Method 2

Or, just init the log service with:

```PHP
use XiaoYun\Supports\Log;

protected function registerLog()
{
    $logger = Log::createLogger($file, $identify, $level);

    Log::setLogger($logger);
}
```

### Usage

After registerLog, you can use Log service:

```PHP
use XiaoYun\Supports\Log;

Log::debug('test', ['test log']);
```
