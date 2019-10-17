![LambdaTest Logo](https://www.lambdatest.com/static/images/logo.svg)
---

# php-laravel-dusk-todo
A Sample PHP-Laravel app to run selenium automation tests on LambdaTest grid. 

### Prerequisites
- Install php and composer on your system. Setup Instructions for the same can be found  [here](https://www.lambdatest.com/support/docs/display/TD/Quick+Guide+To+Run+PHP+Tests+on+LambdaTest+Selenium+Grid) 

### Installation
```bash
# setup project dependencies
composer install
composer dump-autoload
```

### Configuration steps
- Create `.env` from example file
    ```bash
        cp .env.example .env
    ```
- Replace `LT_USERNAME` with your LambdaTest username. It can be obtained from [LambdaTest dashbaord](https://automation.lambdatest.com/)
- Replace `LT_ACCESS_KEY` with your access key. It can be generated from [LambdaTest dashbaord](https://automation.lambdatest.com/) 
- Update platform configuration in driver method of `tests/DuskTestCase.php`, to specify the target where tests should run. (List of supported OS platfrom, Browser, resolutions can be found at [LambdaTest capability generator](https://www.lambdatest.com/capabilities-generator/)) 
 Sample configuration
    ```php
    return RemoteWebDriver::create($url, 
            DesiredCapabilities::chrome()
                ->setCapability("platform", "win10")
                ->setCapability("browserName", "chrome")
                ->setCapability("version", "71.0")
                ->setCapability("resolution", "1024x768")
                ->setCapability("build", "LaravelDusk Build")
                ->setCapability("name", "LaravelDusk Test")
                ->setCapability("network", true)
                ->setCapability("video", true)
                ->setCapability("visual", true)
                ->setCapability("console", true)
                ->setCapability("tunnel", false)
        );
    ```



###  Routing traffic through your local machine
- Set tunnel value to `true` in test capabilities (found in driver method of `tests/DuskTestCase.php`). 

    e.g:
    ```php
    return RemoteWebDriver::create($url, 
                DesiredCapabilities::chrome()
                    ->setCapability("platform", "win10")
                    ->setCapability("browserName", "chrome")
                    ->setCapability("version", "71.0")
                    ->setCapability("resolution", "1024x768")
                    ->setCapability("build", "LaravelDusk Build")
                    ->setCapability("name", "LaravelDusk Test")
                    ->setCapability("network", true)
                    ->setCapability("video", true)
                    ->setCapability("visual", true)
                    ->setCapability("console", true)
                    ->setCapability("tunnel", true)
            );
    ```
> OS specific instructions to download and setup tunnel binary can be found at the following links.
>    - [Windows](https://www.lambdatest.com/support/docs/display/TD/Local+Testing+For+Windows)
>    - [Mac](https://www.lambdatest.com/support/docs/display/TD/Local+Testing+For+MacOS)
>    - [Linux](https://www.lambdatest.com/support/docs/display/TD/Local+Testing+For+Linux) 

### Run tests
```bash
php artisan dusk
```

### Generate test cases
- Change directory to project root `cd /your/project`
- Execute `php artisan dusk:make {test case name}` 
    e.g:
    ```bash
    php artisan dusk:make TodoTest
    ```
### Note
Our sample test case can be found in `tests/Browser/TodoTest.php` file. It navigates to our sample to-do app.

## About LambdaTest
[LambdaTest](https://www.lambdatest.com/) is a cloud based selenium grid infrastructure that can help you run automated cross browser compatibility tests on 2000+ different browser and operating system environments. All test data generated during testing including Selenium command logs, screenshots generated in testing, video logs, selenium logs, network logs, console logs, and metadata logs can be extracted using [LambdaTest automation APIs](https://www.lambdatest.com/support/docs/api-doc/). This data can then be used for creating custom reports.
