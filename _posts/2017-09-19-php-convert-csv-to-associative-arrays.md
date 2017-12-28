---
layout: post
title: PHP convert CSV to associative arrays
---

Something handy when importing CSV files:

```php
<?php

$csv = array_map('str_getcsv', file($file));
array_walk($csv, function(&$a) use ($csv) {
   $a = array_combine($csv[0], $a);
});
array_shift($csv); # remove column header

?>
```

This will yield something like this – keys are the fields/ table header of the CSV file.

`[2] => Array ( [Campaign ID] => 295095038 [Ad group ID] => 22460178158 [Keyword ID] => 3993587178 )`
