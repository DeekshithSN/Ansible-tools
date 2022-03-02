
![ja](https://user-images.githubusercontent.com/29688323/156386876-3b288002-f3af-4c96-b360-3a5b115d8b36.png)


JFrog Artifactory is a universal DevOps solution providing end-to-end automation and management of binaries and artifacts through the application delivery process that improves productivity across your development ecosystem


*** This setup works well on Debian / Ubuntu ***


### Install Setup
--------------------

#### Primary Node

- Change directory to /opt/

```
cd /opt
```

- Download jfrog debain file from [here](https://jfrog.com/download-legacy/?product=artifactory&installer=debian)

```
wget https://releases.jfrog.io/artifactory/artifactory-pro-debs/pool/jfrog-artifactory-pro/jfrog-artifactory-pro-7.31.13.deb
```

- set Jfrog Env varibale 

```
echo "export JFROG_HOME=/opt/jfrog" >> ~/.bashrc
echo "export JF_PRODUCT_VAR=/opt/jfrog-var" >> ~/.bashrc
source ~/.bashrc
```
Test whether env variables set or not using ``` echo $JFROG_HOME ```

- In ```/opt``` directory execute dpkg command to install deb file.

```
dpkg -i jfrog-artifactory-pro-7.31.13.deb
```

- Artifactory uses postgres a db, its depedency jar should be placed jfrog directory

download it from [here](https://jdbc.postgresql.org/download.html)
```
wget https://jdbc.postgresql.org/download/postgresql-42.2.18.jar
```

- copy postgres jar to jfrog tomcat folder 

```
cp postgresql-42.2.18.jar $JFROG_HOME/artifcatory/var/bootstrap/artifactory/tomcat/lib
```

- Change the permission to postgres jar, make artifcatory user as owner to postgres jar file

```
cd $JFROG_HOME/artifcatory/var/bootstrap/artifactory/tomcat/lib
chown -R artifcatory:artifcatory postgresql-42.2.18.jar
chmod 755 postgresql-42.2.18.jar
```

- update system.yaml file with postgres db details 

```
vi $JFROG_HOME/artifcatory/var/etc/system.yaml
```
below is the config file

```
configVersion: 1
shared:
  security: 
  database:
    driver: org.postgresql.Driver
    password: password
    type: postgresql
    url: "jdbc:postgresql://<your db url, for example: localhost:5432>/artifactory"
    username: artifactory
  node:
    haEnabled: true
    primary: true
```

- Run install script 

```
sudo $JFROG_HOME/artifcatory/app/bin/installService.sh
```

make  sure system.yaml didnt change much..

- start artifcatory service 

```
systemctl start artifactory.service 
```

- Check the logs whether its working or not 

```
tail -f  $JFROG_HOME/artifcatory/var/log/access.log
```


#### Secondary Node

- Change directory to /opt/

```
cd /opt
```

- Download jfrog debain file from [here](https://jfrog.com/download-legacy/?product=artifactory&installer=debian)

```
wget https://releases.jfrog.io/artifactory/artifactory-pro-debs/pool/jfrog-artifactory-pro/jfrog-artifactory-pro-7.31.13.deb
```

- set Jfrog Env varibale 

```
echo "export JFROG_HOME=/opt/jfrog" >> ~/.bashrc
echo "export JF_PRODUCT_VAR=/opt/jfrog-var" >> ~/.bashrc
source ~/.bashrc
```
Test whether env variables set or not using ``` echo $JFROG_HOME ```

- In ```/opt``` directory execute dpkg command to install deb file.

```
dpkg -i jfrog-artifactory-pro-7.31.13.deb
```

- Artifactory uses postgres a db, its depedency jar should be placed jfrog directory

download it from [here](https://jdbc.postgresql.org/download.html)
```
wget https://jdbc.postgresql.org/download/postgresql-42.2.18.jar
```

- copy postgres jar to jfrog tomcat folder 

```
cp postgresql-42.2.18.jar $JFROG_HOME/artifcatory/var/bootstrap/artifactory/tomcat/lib
```

- Change the permission to postgres jar, make artifcatory user as owner to postgres jar file

```
cd $JFROG_HOME/artifcatory/var/bootstrap/artifactory/tomcat/lib
chown -R artifcatory:artifcatory postgresql-42.2.18.jar
chmod 755 postgresql-42.2.18.jar
```

- update system.yaml file with postgres db details 

```
vi $JFROG_HOME/artifcatory/var/etc/system.yaml
```
below is the config file

```
configVersion: 1
shared:
  security: 
  database:
    driver: org.postgresql.Driver
    password: password
    type: postgresql
    url: "jdbc:postgresql://<your db url, for example: localhost:5432>/artifactory"
    username: artifactory
  node:
    haEnabled: true
    primary: true
```

- Run install script 

```
sudo $JFROG_HOME/artifcatory/app/bin/installService.sh
```

make  sure system.yaml didnt change much..
