```php

class Pagination 
{ 

    private $page;
    private $limit;
    private $offset;
    private $totalPages;
    private $arr_page;
    private $link;

    public function setPager($page, $arr_page, $limit, $link) 
    { 
      $total = count( $arr_page );
      $totalPages = ceil( $total/ $limit ); 
      $page = max($page, 1);
      $page = min($page, $totalPages);
            $offset = ($page - 1) * $limit;
      if( $offset < 0 ) $offset = 0;
      $this->page = $page;
      $this->limit  = $limit;
      $this->offset = $offset;
      $this->totalPages = $totalPages;
      $this->arr_page = $arr_page;
      $this->link = $link;
    }   

    public function getArrayPage() 
    { 
        $res_testimony_page = array_slice( $this->arr_page, $this->offset, $this->limit );
        return $res_testimony_page;
    }

    public function getTestiContainerPager()
    {    
      $ret = '<div style="min-width: 300px;">';
      if( $this->totalPages != 0 ) {
        if( $this->page == 1 ) {
          $ret .= '';
        }
        else {
          $ret .= sprintf( '<a href="?' . $this->link . '=%d" style="color: #0f4c75">&#171; prev</a>', $this->page - 1 );
        }
        $ret .= ' <span><strong>' . $this->page . '</strong> / ' . $this->totalPages . '</span> ';

        if( $this->page == $this->totalPages ) {
          $ret .= '';
        }
        else {
          $ret .= sprintf( '<a href="?' . $this->link .'=%d" style="color: #0f4c75">next &#187;</a>', $this->page + 1 );
        }
      }
      $ret .= '</div>';
      
      return $ret;
  }
}
```
