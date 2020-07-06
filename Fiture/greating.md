```php
//***GREATING SELAMAT PAGI/SIANG/SORE DAN WAKTU

class Greating
{

  public $f;
  public $D;
  public $d;
  public $m;
  public $y;
  public $w;
  function setTimeZone($location)
  {
    $f = new DateTimeFormat;
    date_default_timezone_set($location);
    $D = date('D');
    $d = date('d');
    $m = date('m');
    $y = date('Y');
    $w = date('H');
    $this->f = $f;
    $this->D = $D;
    $this->d = $d;
    $this->m = $m;
    $this->y = $y;
    $this->w = $w;
  }
  function getDay()
  {
    $f = $this->f;
    $D = $this->D;
    $arr_day = $f->getNamaHari();
    $ret = $arr_day[$D];
    return $ret;
  }
  function getDate()
  {
    $f = $this->f;
    $m = $this->m;
    $arr_month = $f->getNamaBulan();
    $m = $arr_month[$m];
    $ret = $this->d . ' ' . $m . ' ' . $this->y;
    return $ret;
  }
  function getUcapan()
  {
     $a = $this->w;
     if (($a>=6) && ($a<=11)) {
      return " <b> Selamat Pagi !! </b>";
    } else if(($a>=11) && ($a<15)){
      return " <b> Selamat  Siang !! </b>";
    } elseif(($a>=15) && ($a<=18)){
      return " <b> Selamat Sore !! </b>";
    } else{
      return " <b> Selamat Malam !! </b>";
    }
  }
}
```
