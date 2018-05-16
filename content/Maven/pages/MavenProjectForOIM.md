Title: Setup of Maven project for OIM
Category: Maven
Date: 2017-04-03 23:16

1. Install & configure Apache Maven
```
wget http://www.us.apache.org/dist/maven/maven-3/3.3.3/binaries/apache-maven-3.3.3-bin.tar.gz
export PATH=/opt/apache-maven-3.3.3/bin:$PATH

vi ~/.m2/settings.xml
<settings>
  <proxies>
     <proxy>
        <id>nvs-proxy</id>
        <active>true</active>
        <protocol>http</protocol>
        <host>proxy.nscendoni.net</host>
        <port>2011</port>
      </proxy>
   </proxies>
</settings>
```
2. Generate the Maven project:
```
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```
3. Import some required jar to develop for OIM:
```
mvn install:install-file -Dfile=/opt/oracle/product/fmw/11.1.2/oracle_iam/designconsole/lib/oimclient.jar -DgroupId=oracle -DartifactId=oimclient -Dversion=11.1.2 -Dpackaging=jar
mvn install:install-file -Dfile=/opt/oracle/product/fmw/11.1.2/oracle_iam/designconsole/lib/oimclient.jar -DgroupId=oracle -DartifactId=oimclient -Dversion=11.1.2 -Dpackaging=jar
mvn install:install-file -Dfile=/opt/oracle/product/fmw/11.1.2/oracle_wls/server/lib/wlfullclient.jar -DgroupId=oracle -DartifactId=wlfullclient -Dversion=11.1.2 -Dpackaging=jar
mvn install:install-file -Dfile=/opt/oracle/product/fmw/11.1.2/oracle_iam/server/apps/was/lib/oracle.iam.ui.view/jrf-api.jar -DgroupId=oracle -DartifactId=jrf-api.jar -Dversion=11.1.2 -Dpackaging=jar
mvn install:install-file -Dfile=/opt/oracle/product/fmw/11.1.2/oracle_iam/server/client/ext/spring.jar -DgroupId=oracle -DartifactId=spring -Dversion=11.1.2 -Dpackaging=jar
mvn install:install-file -Dfile=/opt/oracle/product/fmw/11.1.2/oracle_iam/server/client/ext/commons-logging.jar -DgroupId=oracle -DartifactId=common-logging -Dversion=11.1.2 -Dpackaging=jar
mvn install:install-file -Dfile=/opt/oracle/product/fmw/11.1.2/oracle_iam/server/client/ext/commons-logging.jar -DgroupId=oracle -DartifactId=common-logging -Dversion=11.1.2 -Dpackaging=jar
```
