## Change Format date
in my case format date, that get from Api;
`field_date_end => <time datetime=\"2020-06-22T04:30:00Z\" class=\"datetime\">Mon, 22/06/2020 - 11:30</time>\n`

### Make script
```php
//*** AMBIL DATA START DAN END DARI API

function getArrayDateApi($data) {
    $result = array();

    foreach($data as $key => $val) {
     $date = array();
     $date['start'] = $val['field_date_start'];
     $date['end'] = $val['field_date_end'];
     $result[$key] = $date;
    }

    return $result;
}


//*** FORMATED DATA TANGGAL DAN WAKTU API
// DALAM BENTUK BAHASA INDONESIA

class DateTimeFormat
{

    public $arr_start;
    public $arr_end;


    public function getArrStart($data)
    {
      $s = explode('>', $data);
      $r = preg_replace('/([a-z]+)\, (\d+\/\d+\/\d+) \- (\d+\:\d+)/is', '\1 \2 \3 ', $s[1]);
      $arr = explode(' ', $r);
      $this->arr_start = $arr;
      return $arr;
    }

    public function getArrEnd($data)
    {
      $s = explode('>', $data);
      $r = preg_replace('/([a-z]+)\, (\d+\/\d+\/\d+) \- (\d+\:\d+)/is', '\1 \2 \3 ', $s[1]);
      $arr = explode(' ', $r);
      $this->arr_end = $arr;
      return $arr;
    }

    public function getDay()
    {
      $arr_hari = $this->getNamaHari();
      $arr_s = $this->arr_start;
      $arr_e = $this->arr_end;
      $hari_s = $arr_s['0'];
      $hari_s = $arr_hari[$hari_s];
      $hari_e = $arr_s['0'];
      $hari_e = $arr_hari[$hari_e];
      if($hari_s == $hari_e){
         $hari = $hari_s;
      }else{
         $hari = '';
      }
      return $hari;
    }

    public function getDate()
    {
      $arr_bulan = $this->getNamaBulan();
      $arr_s = $this->arr_start;
      $arr_e = $this->arr_end;
      $dat_s = explode('/', $arr_s['1']);
      $dat_e = explode('/', $arr_e['1']);
      $num_s = $dat_s['0'];
      $num_e = $dat_e['0'];
      $bulan_s = $dat_s['1'];
      $bulan_s = $arr_bulan[$bulan_s];
      $bulan_e = $dat_e['1'];
      $bulan_e = $arr_bulan[$bulan_e];
      //11 juni 2020
      //12-14 juni 2020
      //11 juni - 12 july 2020
      if ($bulan_s == $bulan_e && $num_s == $num_e){
         $date = $num_s . ' ' . $bulan_s . ' ' . $dat_s['2'];
      } elseif ($bulan_s == $bulan_e && $num_s != $num_e){
         $date = $num_s . '-' . $num_e . ' ' . $bulan_s . ' ' . $dat_s['2'];
      } else {
         $date = $num_s . ' ' . $bulan_s . '-' . $num_e . ' ' . $bulan_e .' ' . $dat_s['2'];
      }

      return $date;
    }

    public function getTime()
    {
      $arr_s = $this->arr_start;
      $arr_e = $this->arr_end;
      $arr_s = $arr_s[2];
      $arr_e = $arr_e[2];
      //$arr = preg_replace("/\'(\d+\:\d+)/is", '\1', $arr)
       return $arr_s . '-' . $arr_e;
    }

    public function getNamaBulan()
    {
        return array(
              '01' => 'Januari',
              '02' => 'Februari',
              '03' => 'Maret',
              '04' => 'April',
              '05' => 'Mei',
              '06' => 'Juni',
              '07' => 'Juli',
              '08' => 'Agustus',
              '09' => 'September',
              '10' => 'Oktober',
              '11' => 'November',
              '12' => 'Desember',

        );
    }

    public function getNamaHari()
    {
        return array(
              'Sun' => 'Minggu',
              'Mon' => 'Senin',
              'Tue' => 'Selasa',
              'Wed' => 'Rabu',
              'Thu' => 'Kamis',
              'Fri' => 'Jumat',
              'Sat' => 'Sabtu',

        );
    }

    public function getArrayDateFormat($data) {
    $result = array();
        foreach($data as $key => $val) {
         $date = array();
         $this->getArrStart($val['start']);
         $this->getArrEnd($val['end']);
         $date['hari'] = $this->getDay();
         $date['tanggal'] = $this->getDate();
         $date['waktu'] = $this->getTime();
         $result[$key] = $date;
        }

    return $result;
    }

}

```

### Used script
```php
$dateformat = new DateTimeFormat;
$res_events_se = getArrayDateApi($res_events_home);
$res_events_date = $dateformat->getArrayDateFormat($res_events_se);

```
And output `$res_events_date` is array like:

```php
array (
  0 => 
  array (
    'hari' => 'Jumat',
    'tanggal' => '03 Juli 2020',
    'waktu' => '10:30-12:00',
  ),
  1 => 
  array (
    'hari' => 'Senin',
    'tanggal' => '06-17 Juli 2020',
    'waktu' => '10:00-16:00',
  ),
 );
```
