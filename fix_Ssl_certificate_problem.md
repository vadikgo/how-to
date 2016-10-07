#### Исправление ошибки при клонировании git: SSL certificate problem: self signed certificate

При клонировании репозитория по https появляется ошибка:
 
> $ git clone https://sbt-qa-jenkins.example.com/Jupiter/stub_dpcAndWayStub.git
> 
> Cloning into 'stub_dpcAndWayStub'...
> 
> fatal: unable to access 'https://sbt-qa-jenkins.example.com/Jupiter/stub_dpcAndWayStub.git/': SSL certificate problem: self signed certificate
>
 
#### Варианты решения:
 
* Необходимо добавить его сертификат в хранилище сертификатов компьютера или сказать гиту игнорировать ошибки сертификата:
 
`GIT_SSL_NO_VERIFY=1 git clone https://sbt-qa-jenkins.example.com/Jupiter/stub_dpcAndWayStub.git`
 
* Добавить в экспортируемые переменные, например в ~/.bashrc:
 
`export GIT_SSL_NO_VERIFY=1`
 
* Отключить проверку сертификатов в git:
 
`git config http.sslVerify false`
 
* Использовать подключение по ssh

* Добавить сертификат в хранилище сертификатов
 
#### Как добавить сертификат в хранилище сертификатов
 
##### Centos 6
```
yum install ca-certificates
echo | openssl s_client -connect sbt-qa-jenkins.example.com:443 2>/dev/null | openssl x509 > /etc/pki/ca-trust/source/anchors/sbt-qa-jenkins.example.com.crt
update-ca-trust extract
curl https://sbt-qa-jenkins.example.com/ci
```
 
##### Windows
Добавить сертификат в доверенные центры сертификации
