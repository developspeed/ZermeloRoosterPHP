# ZermeloRoosterPHP

A PHP wrapper for the Zermelo API to get information out of the Zermelo zportal.
Let me know what you did build with it. I am really curious :)

Create a pull request if you like to contribute, or create an issue if you expercience any issues so I can help you out :)

### License

Using the MIT license.

For all the forkers or users of the code, please add a (small) reference to the original code. That would be nice, tnx!

### Installing and creating a API instance
To create a new API instance, you may want to require the composer autoloader.
So add the following to your composer.json file

```json
{
    "require": {
        "wvanbreukelen/zermelo-rooster-php": "1.0.*"
    }
}
```

And run

```
composer update
```

If you like, you can also use the build-in autoloader that I have created by using the following code

```php
require('custom_autoload.php');

register_zermelo_api();

$zermelo = new ZermeloAPI('hereyourschoolname');
```

(HTTPS not working probably, see outgoing issue #11) It's also possible to connect with the HTTPS protocol enabled, if your webserver supports this feature, just add the true boolean to the class instance constructor

```php
$zermelo = new ZermeloAPI('hereyourschoolname', true)
```


#### Authentation tokens
To receive an authentation token for a specific student, you will need a code, that you can get from the Zermelo zportal itself.
Use the following method

```php
$zermelo->grabAccessToken('user', 'code');
```
The authentation token will be automatically saved to a cache file (cache.json).
If you received your authentation token, you can skip this method because the class will automatically check for the existance in "cache.json"

#### Grids

This method returns an array with all the information about the grid. The class automatically optimizes and sorts the grid out. Also, some easy to use parameters like timestamps are added.

```php
$grid = $zermelo->getStudentGrid('user');
```

To get a grid for example three weeks ahead, please use the following code

```php
$grid = $zermelo->getStudentGridAhead('user', 3)
```

#### Classes

For resolving classes with an additional rule involved, you can use the resolveClasses method.

##### Teachers

By example, if you want to get some hours where a specific teacher is involved, use the following method call

```php
$grid = $zermelo->resolveTeacherClasses($grid, 'hlf');
```

The first argument contains the grid that you received from the Zermelo servers (by using the getStudentGrid method)
The second argument contains the teachers abbreviation of his/her last name.

##### Cancelled Classes

If you want to receive all of the cancelled classes in a grid, use the following method call

```php
$grid = $zermelo->resolveCancelledClasses($grid);
```

The first argument contains the grid that you received from the Zermelo servers (by using the getStudentGrid method)

#### Announcements

It is possible to receive all of the user's announcements by using the following method

```php
$messages = $zermelo->getAnnouncements('user');
```

Also the future

```php
$messages = $zermelo->getAnnouncementsAhead('user', 3);
```

#### Formatting

If you like, you can format the given array to XML code using the "formatXML" method.
See code

```php
$xml = $zermelo->formatXML($grid);
```

You can specify the root element by added a second parameters, like this

```php
$xml = $zermelo->formatXML($grid, '<grid><grid/>');
```

#### Remarks

This project does not have any connections to Zermelo itself! I cannot guarentee any expectations of the class.
