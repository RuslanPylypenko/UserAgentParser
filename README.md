#User-Agent Parser

1. Crate 'components' directory if not exists (in your basic dir)
2. Copy 'UserAgent.php' into 'components' dir
3. Adjust the config file 'web.php' in 'config' dir

    ```php
    'components' => [
        'userAgent' => [
            'class' => 'app\components\UserAgent'
        ],

        ...
    ]
    ```

#TECHNICAL TASK
реализовать для фреймворка Yii2 компонент определения платформы по UserAgent браузера.
Основные задачи компонента:

1) Компонент необходимо загружать в bootstrap, он должен содержать методы для удобной выборки данных.
2) Спарсить информацию:

   - тип платформы (mobile, desktop)
   - операционная система (windows, macos, linux, ios, android, windowsphone)
   - название браузера
   - версия браузера

3) Автоматически подставлять layout представления для разных платформ
4) Возможность редиректа по определенным критериям (платформа, ОС, браузер, версия браузера)
5) Возможность блокирования доступа по определенным критериям (платформа, ОС, браузер, версия браузера)

#USAGE

```php
Yii::$app->userAgent-> ...

Yii::$app->userAgent->getPlatform()
//Alias: Yii::$app->userAgent->platform

Yii::$app->userAgent->getOs()
//Alias: Yii::$app->userAgent->os

Yii::$app->userAgent->getBrowser()
//Alias: Yii::$app->userAgent->browser

Yii::$app->userAgent->getBrowserVersion()
//Alias: Yii::$app->userAgent->browserVersion

Yii::$app->userAgent->getIsMobile()
//Alias: Yii::$app->userAgent->isMobile

Yii::$app->userAgent->getIsDesktop()
//Alias: Yii::$app->userAgent->isDesktop

Yii::$app->userAgent->getIsMobileHost()
//Alias: Yii::$app->userAgent->isMobileHost

Yii::$app->userAgent->getMobileLink()
//Alias: Yii::$app->userAgent->mobileLink

#Compare browser versions
// Compare browser for lower version
Yii::$app->userAgent->lower('55.0.2883.87')

// Compare browser for higher version
Yii::$app->userAgent->higher('55.0.2883.86')

// Compare browser version for equals
Yii::$app->userAgent->equal('55.0.2883.85')
```

#TESTING
```php
Yii::$app->userAgent->test();
```