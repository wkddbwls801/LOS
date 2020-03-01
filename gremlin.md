# gremlin
~~~php
<?php
  include "./config.php";
  login_chk();
  dbconnect();
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[id])) exit("No Hack ~_~"); // do not try to attack another table, database!
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[pw])) exit("No Hack ~_~");
  $query = "select id from prob_gremlin where id='{$_GET[id]}' and pw='{$_GET[pw]}'";
  echo "<hr>query : <strong>{$query}</strong><hr><br>";
  $result = @mysql_fetch_array(mysql_query($query));
  if($result['id']) solve("gremlin");
  highlight_file(__FILE__);
?>
~~~

' or 1=1#이라는 SQL 구문을 사용하였다.   
원래의 query문이 select id from prob_gremlin where id='' and pw=''라고 적혀 있다.   
id 값을 무조건 참으로 만든 후, pw 부분을 주석 처리 하면 된다.   
'(작은 따옴표)로 열려 있으므로 다시 '(작은 따옴표)로 닫은 후 or 1=1으로 만들었다. or을 기준으로 앞부분은 거짓이고 뒷부분은 참이므로 결과적으로는 무조건 참이 된다.(and가 아닌 or이기 때문에) 이후 %23(#)을 통해 주석 처리를 하면 된다.
