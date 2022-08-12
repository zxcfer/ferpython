---
layout: post
title: "PHP Fluent PDO"
tags: ["php", "PDO", "FluentPDO", "ORM"]
---

# FluentPDO Cheat Sheet

- Queries

```php
$query = $fpdo->from('article') 
            ->where('published_at > ?', $date)
            ->orderBy('published_at DESC')
            ->limit(5);

foreach ($query as $row) {
    echo "$row[title]\n";
}

$query->fetchAll();
```

```php
$query = $fpdo->from('article') // SELECT article.*, user.name FROM article 
              ->leftJoin('user ON user.id = article.user_id') // LEFT JOIN user ON user.id = article.user_id
              ->select('user.name');

$query = $fpdo->from('article')->leftJoin('user')->select('user.name');

$query = $fpdo->from('article')->select('user.name');

// SELECT
$query = $fpdo->from('article')->where('id', 1);
$query = $fpdo->from('user', 1);
```

- INSERT

```php
$values = array('title' => 'article 1', 'content' => 'content 1');

$query = $fpdo->insertInto('article')->values($values);
$query = $fpdo->insertInto('article', $values);
```

- UPDATE

```php
$set = array('published_at' => new FluentLiteral('NOW()'));

$query = $fpdo->update('article')->set($set)->where('id', 1);
$query = $fpdo->update('article', $set, 1);

// DELETE
$query = $fpdo->deleteFrom('article')->where('id', 1);
$query = $fpdo->deleteFrom('article', 1);

// INSERT, UPDATE and DELETE will be executed after `->execute()`
$fpdo->deleteFrom('article', 1)->execute();


// For join referencing table use colon after table name.
$query = $fpdo->from('user')->leftJoin('article:')->select('article.title');
// or shortly
$query = $fpdo->from('user')->select('article:title');

  SELECT user.*, article.title 
  FROM user 
      LEFT JOIN article ON article.user_id = user.id

// Alias for columns or tables `AS`:
// SELECT article.*, user.name AS author_name 
// FROM article 
//    LEFT JOIN user ON user.id = article.user_id
$query = $fpdo->from('article')->select('user.name AS author_name');

// For more examples see subdirectory tests/
from($table)        // set $table in FROM clause
from($table, $id)   // shortcut for from($table)->where('id = ?', $id)
select($columns[, ...]) // appends SELECT clause with $column or any expresion (e.g. CURDATE() AS today)
leftJoin($joinedTable)
innerJoin($joinedTable)	 // $joinedTable could be "tableName" only or full join statement
                         // ("tableName:" colon means back reference, see Smart join builder)

where("field", "x")  // Translated to field = 'x'
where("field", null) // Translated to field IS NULL
where(null)          // reset clause and remove all prev defined conditions
where("field", array("x", "y")) // Translated to field IN ('x', 'y')
where("field > ?", "x") // bound by PDO
where("field > :name", array(':name' => 'x')) // bound by PDO
where(array("field1" => "value1", ...))	// Translated to field1 = 'value1' AND ...

groupBy($columns[, ...])  // appends GROUP BY clause
having($columns[, ...])   // appends HAVING clause
orderBy($columns[, ...])  // appends ORDER BY clause
limit($limit)             // sets LIMIT clause
offset($offset)           // sets OFFSET clause

fetch($column = '')       // fetch first row or column only from first row
fetchPairs($key, $value)  // fetch pairs
fetchAll($index = '', $selectOnly = '')	// fetch all rows. You can specify for fetched array index-column and which columns will be fetched.

// If you want to reset a clause (i.e. remove previous defined statements), call any clause with null. E.g.:
$query = $query->where(null);   // remove all prev defined where() clauses
$query = $query->orderBy(null); // remove all prev defined orderBy() clauses
$query = $query->select(null)->select('id'); # set "SELECT id FROM .... WHERE"


// Debugging

$fpdo->debug = true        // log queries to STDERR (for console debugging)
$fpdo->debug = $callback   // or set $callback($FluentQuery)  
                           // @see tests/26-debug.phpt for expample usage
```