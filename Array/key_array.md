## Function key Array
This function have job to get key in array multidimension

```php
function array_search_inner ($array, $attr, $val, $strict = FALSE) {
  // Error is input array is not an array
  if (!is_array($array)) return FALSE;
  // Loop the array
  foreach ($array as $key => $inner) {
    // Error if inner item is not an array (you may want to remove this line)
    if (!is_array($inner)) return FALSE;
    // Skip entries where search key is not present
    if (!isset($inner[$attr])) continue;
    if ($strict) {
      // Strict typing
      if ($inner[$attr] === $val) return $key;
    } else {
      // Loose typing
      if ($inner[$attr] == $val) return $key;
    }
  }
  // We didn't find it
  return NULL;
}
```
### Hoe to use?
Example, i want to get key in `$video_lumo` array based on value `$id` that have key `'url'`.
```php
$key_vid = array_search_inner($videos_lumo, 'url', $id);
```
