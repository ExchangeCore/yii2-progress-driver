## License

This library is licensed under the [MIT License](https://github.com/ExchangeCore/yii2-progress-driver/blob/master/LICENSE).

## Purpose

The purpose of this library is to allow [Yii2](https://github.com/yiisoft/yii2) to leverage Progress OpenEdge databases.
Each version of Progress OpenEdge may receive it's own tagged version in the repository if appropriate which will directly correspond to the version of Progress OpenEdge driver being used.

## Installing & Setup

To install this library simply add the appropriate branch to your composer.json file in your yii application and run the
`composer update` command. Your composer.json require section might look something like this:

```
    "require": {
        "exchangecore/yii2-progress-driver": "*"
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

Because Progress does not use primary keys as constraints or unique identifiers the driver makes a best guess at what
might actually be a primary key constraint and what probably isn't. It does this by checking for a key marked as primary
and unique; if it is primary but not unique it will not be treated as a primary key. Because it's possible that not
every table will have a primary key you may need to add one manually to your model in order to leverage certain Yii
functionality. Additionally, if you find the driver has inaccurately determined a primary key you may need to set it
manually. Example of manually setting a primary key in a model:

```
    /**
     * @inheritdoc
     */
    public static function primaryKey()
    {
        return ['usr_userid'];
    }
```
