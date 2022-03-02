
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

- 
