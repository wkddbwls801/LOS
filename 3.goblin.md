# goblin
~~~ php
<?php 
  include "./config.php"; 
  login_chk(); 
  dbconnect(); 
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[no])) exit("No Hack ~_~"); 
  if(preg_match('/\'|\"|\`/i', $_GET[no])) exit("No Quotes ~_~"); 
  $query = "select id from prob_goblin where id='guest' and no={$_GET[no]}"; 
  echo "<hr>query : <strong>{$query}</strong><hr><br>"; 
  $result = @mysql_fetch_array(mysql_query($query)); 
  if($result['id']) echo "<h2>Hello {$result[id]}</h2>"; 
  if($result['id'] == 'admin') solve("goblin");
  highlight_file(__FILE__); 
?>
~~~

preg_match()함수를 보면 '(작은 따옴표)를 필터링하고 있다. 즉 사용할 수 없다는 소리   
일단 id='guest'라고 고정되어 있으므로 or문을 통해 id='guest' and no= 부분을 거짓으로 만든 후, id='admin'#로 query문을 작성하면 된다.   
'(작은 따옴표)를 쓰지 못하므로 char()로 우회하여 사용하였다.   
query를 no=1 or id=char(97,100,109,105,110)%23로 작성하였는데 풀리지 않아 no=2로 바꾸어 보았더니 풀렸다. guest의 no가 1이라서 참이 되어 풀리지 않았던 것 같다.
