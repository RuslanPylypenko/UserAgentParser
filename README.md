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

