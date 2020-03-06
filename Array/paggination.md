## Paggination
this function have job to get next and prev array
```php
    function get_next($array, $key) {
    $currentKey = current($array);
    while ($currentKey !== null && $currentKey != $key) {
       next($array);
       $currentKey = current($array);
    }
    return next($array);
    };

    function get_prev($array, $key) {
    $currentKey = current($array);
    while ($currentKey !== null && $currentKey != $key) {
       next($array);
       $currentKey = current($array);
    }
    return prev($array);
    };

    // next and prev key book

    $next = get_next($key_book, $key_vid);
    $prev = get_prev($key_book, $key_vid);

    // set url next and prev

    $next_url = (isset($videos[$next]['url'])?$videos[$next]['url']:"");
    $prev_url = (isset($videos[$prev]['url'])?$videos[$prev]['url']:"");
```
