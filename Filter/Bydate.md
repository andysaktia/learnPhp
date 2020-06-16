## Make filter
In server declare default timezone first with code function `date_default_timezone_set("UTC");` 
after that you can declare format date that you use, in my case `$now = date("Y-m-d H:i:s");`.

Data will split `$data = '<time datetime=\"2020-05-18T02:00:00Z\" class=\"datetime\">Mon, 18/05/2020 - 09:00</time>\n';`.
And function to spilt for format like `$now`.

```php
function getDateFormat($data){
       $d = split('\"', $data);
       $t = preg_replace('/[T]/is', ' ', $d[1]);
       $t = preg_replace('/[Z]\\\/is', ' ', $t);
       return $t;
}
```
## Filter in Action
if date past `<` and vice versa.
```php
 if ($t <= $now ){
     echo('yes');
 } else {
     echo('no');
 }
```
