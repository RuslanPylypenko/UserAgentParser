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

1. Компонент необходимо загружать в bootstrap, он должен содержать методы для удобной выборки данных.
2. Спарсить информацию:

   - тип платформы (mobile, desktop)
   - операционная система (windows, macos, linux, ios, android, windowsphone)
   - название браузера
   - версия браузера

3. Автоматически подставлять layout представления для разных платформ
4. Возможность редиректа по определенным критериям (платформа, ОС, браузер, версия браузера)
5. Возможность блокирования доступа по определенным критериям (платформа, ОС, браузер, версия браузера)

#USAGE

```php
Yii::$app->userAgent-> ...

Yii::$app->userAgent->platform
// Alias: Yii::$app->userAgent->getPlatform()

Yii::$app->userAgent->os
// Alias: Yii::$app->userAgent->getOs()

Yii::$app->userAgent->browser
// Alias: Yii::$app->userAgent->getBrowser()

Yii::$app->userAgent->browserVersion
// Alias: Yii::$app->userAgent->getBrowserVersion()

Yii::$app->userAgent->isMobile
// Alias: Yii::$app->userAgent->getIsMobile()

Yii::$app->userAgent->isDesktop
// Alias: Yii::$app->userAgent->getIsDesktop()

Yii::$app->userAgent->isMobileHost
// Alias: Yii::$app->userAgent->getIsMobileHost()

Yii::$app->userAgent->mobileLink
// Alias: Yii::$app->userAgent->getMobileLink()

#Compare browser versions
// Compare browser for lower version
Yii::$app->userAgent->browserCompare('55.0.2883.86 < 55.01.27')

// Compare browser for higher version
Yii::$app->userAgent->browserCompare('55.0.2883.86 > 55.01.27')

// Compare browser version for equals
Yii::$app->userAgent->browserCompare('55.0.2883.86 = 55.01.27')


#REDIRECTING

// AUTO REDIRECT
public function init() {
    $this->getUsrAgent();
    $this->Parse();

    // Редирект по платформе
    // (from Desktop -> http://m.localhost/...)
    if ($this->isMobile) {

        // Another way...
        // $tpl = '/https?:\/\/m.'.Yii::$app->getRequest()->serverName.'/';
        // if (preg_match($tpl, Yii::$app->getRequest()->hostInfo) == 0) {

        if (! $this->isMobileHost) {
            Yii::$app->getResponse()->redirect($this->mobileLink);
            //$this->redirect($mobileUrl);

            Yii::$app->end();
        }
    }

    parent::init();
}


// MANIPULATION WITH REDIRECT

if (Yii::$app->userAgent->isMobile) {
    $this->redirect(...);
}

if (Yii::$app->userAgent->isDesktop) {
    $this->redirect(...);
}

if (Yii::$app->userAgent->os == 'windowsphone') {
    $this->redirect(...);
}

if (Yii::$app->userAgent->browser == 'chrome') {
    $this->redirect(...);
}

if (Yii::$app->userAgent->browserCompare('55.0.2883.86 > 55.01.27')) {
    $this->redirect(...);
}

if (Yii::$app->userAgent->browserCompare('55.0.2883.86 < 55.01.27')) {
    $this->redirect(...);
}

if (Yii::$app->userAgent->browserCompare('55.0.2883.86 = 55.01.27')) {
    $this->redirect(...);
}


```

#TESTING
```php
Yii::$app->userAgent->test();
```