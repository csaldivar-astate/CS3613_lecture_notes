# Model Requirements

---

## Specifying the Schema

The schema should be an associative array in which the name of the column is the key and the SQL datatype and any constraints on the column are the value.

Example of schema attribute of a `Book` class:

```php
public static $schema = [
    'id'     => 'INTEGER PRIMARY KEY AUTOINCREMENT',
    'title'  => 'TEXT NOT NULL',
    'author' => 'TEXT',
    'isbn'   => 'TEXT NOT NULL'
];
```

---

## Full `Book` Model:

```php
class Book {
    // Required by Paris framework (github.com/j4mie/paris):
    public static $_table_use_short_name = true;

    // Required by `update_db.php`:
    public static $schema = [
        'id'     => 'INTEGER PRIMARY KEY AUTOINCREMENT',
        'title'  => 'TEXT NOT NULL',
        'author' => 'TEXT',
        'isbn'   => 'TEXT NOT NULL'
    ];
}
```

---

## List of SQL Data Types

The following data types are available in SQLite3:

```sql
INTEGER
TEXT
DOUBLE
```

---

## Constraints

In additon to type, you can specify _constraints_ to help convey things like optional items, default values, or the most important field in your model (from a searching perspective):

```sql
PRIMARY KEY   --- indicates this is the primary, unique 
                  --- identifier field
UNIQUE        --- specifies this field must be unique
NOT NULL      --- never allow this field to be left out 
                  --- when adding data
DEFAULT v     --- set this field's value to 'v' if it is 
                  --- not specified
AUTOINCREMENT --- generate this field's value automatically 
                  --- by counting up
```

You may specify several constraints on a field if necessary; some constraints imply others (but redundancy is not an error).

---

## Resources

https://github.com/jcausey-astate/php_model_to_db
https://github.com/j4mie/paris
