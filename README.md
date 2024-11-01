# eth-jmeter-sample
Stress test the RPC interface of the eth chain by implementing `java request`

## Install 

Install Java


``` 
cd /opt
apt install openjdk-17-jre-headless

sudo wget https://download.oracle.com/java/17/archive/jdk-17.0.9_linux-x64_bin.tar.gz 
sudo tar xvf jdk-17_linux-x64_bin.tar.gz 


```
Install Maven


```
cd /opt

sudo wget https://dlcdn.apache.org/maven/maven-4/4.0.0-alpha-12/binaries/apache-maven-4.0.0-alpha-12-bin.tar.gz

sudo tar xvf apache-maven-4.0.0-alpha-12-bin.tar.gz
```

Add Path for Maven and Java to ``maven.sh``

1. Run
```
sudo nano /etc/profile.d/maven.sh
```
2. Add to the end of file
```
export JAVA_HOME=/opt/jdk-17.0.9
export M2_HOME=/opt/apache-maven-4.0.0-alpha-12
export MAVEN_HOME=/opt/apache-maven-4.0.0-alpha-12
export PATH=${M2_HOME}/bin:${PATH}
```
3. Apply changes 
```
source /etc/profile.d/maven.sh
```

4. Check installation
```
echo $JAVA_HOME

mvn -v

```

## Jmx erc20 sampler explanation
Located in ``./eth-jmeter-skale/src/test/jmeter/``

` rpcUrl ` - Url endpoint of node     
` default_private_key ` - Private key of user to refill balances    
` Mnemonic ` - test data    
` size ` - amount of transactions should be sent in the 1 round     
` to ` - Contract address of erc20    
` gasLimit ` - max gas limit for the transaction   
` gasPrice ` - gas price on the network (Default 100000 on Skale)   
` value ` - Amount of Sfuel to send   
` payload ` - data field for ERC20 transfers   


### Edit run for ERC20 transfer

```
cd src/test/jmeter/

```
Copy  ``4-nodes-example.jmx`` file  and replace:      
` to ` - set actual erc20 contract for the provided endpoints     
` gasLimit ` - set expected gasLimit for the transaction (default 21000)    
` payload ` - Set data with erc20 method of transfer or other contract interaction     
Example
```
0x56b8c724000000000000000000000000fe2c5aa110fff89361806ea7ee080bfffba0d3dd0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000006
``` 



## use for run
1. Run all .jmx files in ./src/test/jmeter

```
cd ./eth-jmeter-skale

mvn clean package --file pom.xml jmeter:jmeter 

```

