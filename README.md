#  apoll_zip
### 携程apollo修改后的安装包（支持windows  linux  docker）
主要修改docker-compose.yml中  image镜像拉取不到的问题 无此（apollo-quick-start）镜像
version: '2'
services:
  apollo-quick-start:
    image: nobodyiam/apollo-quick-start
    #image: apollo-quick-start
    container_name: apollo-quick-start
    depends_on:
      - apollo-db
    ports:
      - "8080:8080"
      - "8070:8070"
    links:
      - apollo-db

  apollo-db:
    image: mysql:5.7
    container_name: apollo-db
    environment:
      TZ: Asia/Shanghai
      MYSQL_ALLOW_EMPTY_PASSWORD: 'yes'
    depends_on:
      - apollo-dbdata
    ports:
      - "13306:3306"
    volumes:
      - ./sql:/docker-entrypoint-initdb.d
    volumes_from:
      - apollo-dbdata

  apollo-dbdata:
    image: alpine:latest
    container_name: apollo-dbdata
    volumes:
      - /var/lib/mysql
----------------------------------
[root@localhost ~]# docker search apollo
NAME                               DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
apolloauto/apollo                  Apollo                                          14                                      
gmod/apollo                        Builds https://github.com/gmod/apollo           4                                       [OK]
apollos/redhat6.5                                                                  3                                       
idoop/docker-apollo                Docker image for Ctrip Apollo.携程阿波罗配置…          3                                       [OK]
sagan/apache-apollo                Apache Apollo                                   1                                       [OK]
nobodyiam/apollo-quick-start       Apollo Quick Start                              1                                       
lmaag/apollo                       Install an apollo message brocker               1                                       
remind101/buildpack-apollo                                                         1                                       
riz247/apollo                                                                      0                                       
apollo13/rabbitmq-server           RabbitMQ server for Apollo13 environment.       0                                       [OK]
apitreecz/apollo13-serverless                                                      0                                       
apollo3/spring-boot-based-server                                                   0                                       
ilegra/apollomq                    apollomq                                        0                                       
apitreecz/apollo13-backend                                                         0                                       
apollo13/realitor-frontend-local   Realitor frontend - local development enviro…   0                                       [OK]
chinclubi/apollo                                                                   0                                       
apollo13/ubuntu                    Ubuntu server for Apollo 13 environment.        0                                       [OK]
mikesuggitt/apollo                 WRapper                                         0                                       [OK]
logzio/apollo                                                                      0                                       
md5hashbrowns/apollo-cloud-tor     Apollo Cloud with Tor support                   0                                       [OK]
chinsky/apollo_base                                                                0                                       
njohn/apollo-workshop                                                              0                                       
pypi/apollo                        apollo PyPi package based on python:3           0                                       [OK]
nathandunn/apollo                  Apollo images                                   0                                       
siteshjalan/apollo-workshop         
