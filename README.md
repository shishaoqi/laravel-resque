## Laravel Resque

This package allows you to connect to Resque when using `Queue`. 

## Requirements

- PHP 5.6.4+
- Illuminate\Config 5.3+
- Illuminate\Queue 5.3+
- Resque 1.5+
- ResqueScheduler 1.4+ (Optional)

## Installation

First you need to add the following to your project's `composer.json`:

    "require": {
    	"pdffiller/laravel-resque": "^1.4"
    },
    "repositories": [
        {
            "type": "vcs",
            "url": "git@github.com:pdffiller/laravel-resque.git"
        },
    ]

Now you need to run the following to install the package:

	composer update

Next you need to add the following service provider to your `app/config/app.php`:

    'Awellis13\Resque\ServiceProviders\ResqueServiceProvider'

Now you need to add the following to your `/app/config/queue.php` "connections" section:

    "resque" => [
    	"driver" => "resque"
    ]

To provide custom redis connection use config key `connection`:

        "resque" => [
        	"driver" => "resque",
        	"connection" => "{custom redis connection name from config database.redis}"
        ]

If you wish to use this driver as your default Queue driver you will need to set the following as your "default" drive in `app/config/queue.php`:

    "default" => "resque",


## Usage

If you choose to not use this driver as your default Queue driver you can call a Queue method on demand by doing:

    Queue::connection('resque')->push('JobName', ['name' => 'Andrew']);

### Enqueing a Job

	Queue::push('JobName', ['name' => 'Andrew']);

### Tracking a Job

	$token = Queue::push('JobName', ['name' => 'Andrew'], true);
	$status = Queue::getStatus($token);

### Enqueing a Future Job

	$when = time() + 3600; // 1 hour from now
	Queue::later($when, 'JobName', ['name' => 'Andrew']);
	
### Run console queue listener

	php artisan resque:listen --queue=*

## Further Documentation

- [PHP-Resque](https://github.com/pdffiller/php-resque)
- [PHP-Resque-Scheduler](https://github.com/pdffiller/php-resque-scheduler)

## License

Laravel Resque is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).
