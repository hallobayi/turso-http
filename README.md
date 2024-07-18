![TursoHTTP](https://i.imgur.com/eH0PqQ6.png)

The `TursoHTTP` library is a PHP wrapper for Turso HTTP Database API (Only). It simplifies interaction with Turso databases using the Hrana over HTTP protocol. This library provides an object-oriented approach to build and execute SQL queries with same API Interface like PHP Native Extension [Turso Client PHP](https://github.com/tursodatabase/turso-client-php).

## Requirements
- Intention and Courage
- Instinct as a Software Freestyle Engineer
- Strong determination!
- [Turso](https://turso.tech/) Account
- Don't forget to install [PHP](https://php.net) on your machine
- A cup of coffee and the music you hate the most
- Dancing (optional: if you are willing)

## Installation

You can install the **TursoHTTP** library using Composer:

```bash
composer require darkterminal/turso-http
```

## Usage Example

```php
use Darkterminal\TursoHttp\LibSQL;

require_once 'vendor/autoload.php';

$dbname     = getenv('DB_URL');
$authToken  = getenv('DB_TOKEN');
$db         = new LibSQL("dbname=$dbname&authToken=$authToken");

echo $db->version() . PHP_EOL;

$create_table = <<<SQL
CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT, 
    name TEXT, 
    email TEXT
)
SQL;

$db->execute($create_table);
```

## LibSQL Schema Builder

```php
<?php

use Darkterminal\TursoHttp\LibSQL;
use Darkterminal\TursoHttp\sadness\LibSQLBlueprint;
use Darkterminal\TursoHttp\sadness\LibSQLSchemaBuilder;

require_once 'vendor/autoload.php';

try {
    $dbname = getenv('DB_URL');
    $authToken = getenv('DB_TOKEN');

    $db = new LibSQL("dbname=$dbname&authToken=$authToken");
    $schemaBuilder = new LibSQLSchemaBuilder($db);

    $schemaBuilder->create('contacts', function(LibSQLBlueprint $table) {
        $table->increments('id');
        $table->string('name');
        $table->unique('email');
        $table->string('phone');
        $table->timestamp('created_at');
    })->execute();

    echo "Table created successfully.\n";

    $schemaBuilder->table('contacts', function(LibSQLBlueprint $table) {
        $table->addColumn('DATETIME', 'updated_at', null, 'DEFAULT CURRENT_TIMESTAMP');
    })->execute();

    echo "Column added successfully.\n";
} catch (Exception $e) {
    echo "An error occurred: " . $e->getMessage();
}
```

## Turso Platform API - PHP

Manage databases, replicas, and teams with the Turso Platform API using PHP.

- [Quickstart](docs/PlatformAPI/README.md)
- [API Tokens](docs/PlatformAPI/APITokens.md)
- [Audit Logs](docs/PlatformAPI/AuditLogs.md)
- [Databases](docs/PlatformAPI/Databases.md)
- [Groups](docs/PlatformAPI/Groups.md)
- [Locations](docs/PlatformAPI/Locations.md)

## License

This library is licensed under the MIT License - see the [LICENSE](https://github.com/darkterminal/turso-http/blob/main/LICENSE) file for details.
