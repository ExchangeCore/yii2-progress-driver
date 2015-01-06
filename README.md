## License

This library is licensed under the [MIT License](https://github.com/ExchangeCore/yii2-progress-driver/blob/master/LICENSE).

## Purpose

The purpose of this library is to allow [Yii2](https://github.com/yiisoft/yii2) to leverage Progress OpenEdge databases.
Each version of Progress OpenEdge may have its own branch in this repository in order to accomodate the different levels
of support available for different levels of the OpenEdge driver.

## Installing & Setup

To install this library simply add the appropriate branch to your composer.json file in your yii application and run the
`composer update` command. Your composer.json require section might look something like this:

```
    "require": {
        "php": ">=5.4.0",
        "yiisoft/yii2": "*",
        "yiisoft/yii2-bootstrap": "*",
        "yiisoft/yii2-swiftmailer": "*",
        "kartik-v/yii2-detail-view": "*",
        "exchangecore/yii2-progress-driver": "10.2.*@dev"
    },
```

Once composer has added the library you can configure your database the same as you would other yii databases except you
will now need to use the modified connection class. Here is a sample of connecting to an ODBC DSN on windows that is called
`MyProgressDb`:

```
   'db' => [
       'class' => 'exchangecore\yii2\progress\driver\db\Connection',
       'driverName' => 'progress',
       'dsn' => 'odbc:MyProgressDb',
       'username' => 'testuser',
       'password' => 'testpass',
       'charset' => 'utf8',
   ];
```

## Usage Notes

### Handling Primary Keys

As of right now I have yet to find a way to determine the primary keys for a table from an ODBC call. This means that
for those of you who are planning on using this for things like ActiveRecord, you will need to manually define a primary
key in your Models. This can be done by simply overwriting the function with an array of fields that make up the primary
key for that table. Example:

```
    /**
     * @inheritdoc
     */
    public static function primaryKey()
    {
        return ['usr_userid'];
    }
```