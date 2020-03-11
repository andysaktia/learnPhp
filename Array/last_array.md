## Define Last Array
I want to do something difference with my last array, example not add coma character.
The key is, define last array first with `end($array)` and then foreach array with include if condition:

```php
<?php foreach ($ab_arr as $title => $items) {
         //define last array
         $last_items = end($items)  
            foreach ($items as $k => $item) {
              $passage = $item['passage'];
              $url = $item['url'];
              if($item == $last_items){
          ?>
          <a href="<?= $url ;?>"><?= $passage ?></a>
          <?php }else{ ?>
          <a href="<?= $url ;?>"><?= $passage ?></a>,
<?php }}};?>
```

