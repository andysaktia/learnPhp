## Grouping array
Make new array with grouping based on category key, use this fuction:

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

In my case, i want make array assosiative based on chapter video, but not all chapter that i want take only chapter that in `$key_book`. key book is value key from `$videos`. So, first step i made array chapter for `$key_book` and than make group array based on key array `'chapter'`

```php 
// array that want to fill videos base $key_book
$book_arr = array(); 
foreach ($key_book as $num) {
   // $videos in array include complete video
   array_push($book_arr, $videos[$num]); 
}

// array grouping based key chapter
$chap_arr = group_by('chapter', $book_arr); 

//Dump result
echo "<pre>" . var_export($chap_arr, true) . "</pre>"; 
```
