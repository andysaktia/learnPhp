## Group array
make new array with grouping based on category key, use this fuction:

```php
function group_by($key, $data) {
    $result = array();

    foreach($data as $val) {
        if(array_key_exists($key, $val)){
            $result[$val[$key]][] = $val;
        }else{
            $result[""][] = $val;
        }
    }

    return $result;
}
```

in my case, i want make array assosiative based on chapter video, but not all chapter that i want take only chapter that in `$key_book`. 
key book is value key from `$videos`.

so, first step i made array chapter for `$key_book` and than make group array based  key`'chapter'`

```php 
$book_arr = array(); // array that want to fill videos base $key_book
foreach ($key_book as $num) {
   array_push($book_arr, $videos[$num]); // $videos in array include complete video
}

// array grouping based key chapter
$chap_arr = group_by('chapter', $book_arr); 

//Dump result
echo "<pre>" . var_export($chap_arr, true) . "</pre>"; 
```
