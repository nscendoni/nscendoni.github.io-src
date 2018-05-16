Title: Install Nexus
Date: 2012-12-01 10:02
Category: Maven

```
tar xvfz nexus-2.14.5-02-bundle.tar.gz
cd /nexus-2.14.5-02/bin
./nexus start
```
Change the default password. The default admin/password is admin123

Source: https://dzone.com/articles/getting-started-nexus-maven

# Set pom.xml and setting.xml

Add to pom.xml
```
	<distributionManagement>
		<!-- Publish the versioned releases here -->
		<repository>
			<id>my-company-nexus</id>
			<name>my-company nexus</name>
			<url>dav:http://localhost:8081/nexus/content/repositories/releases</url>
		</repository>

		<!-- Publish the versioned releases here -->
		<snapshotRepository>
			<id>my-company-nexus</id>
			<name>my-company nexus</name>
			<url>dav:http://localhost:8081/nexus/content/repositories/snapshots</url>
		</snapshotRepository>
	</distributionManagement>

	<!-- download artifacts from this repo -->
	<repositories>
		<repository>
			<id>my-company-nexus</id>
			<name>my-company</name>
			<url>http://localhost:8081/nexus/content/groups/public</url>
			<releases>
				<enabled>true</enabled>
			</releases>

			<snapshots>
				<enabled>true</enabled>
			</snapshots>
		</repository>
	</repositories>

	<!-- download plugins from this repo -->
	<pluginRepositories>
		<pluginRepository>
			<id>my-company-nexus</id>
			<name>my-company</name>
			<url>http://localhost:8001/nexus/content/groups/public</url>
			<releases>
				<enabled>true</enabled>
			</releases>
			<snapshots>
				<enabled>true</enabled>
			</snapshots>
		</pluginRepository>
	</pluginRepositories>

```
Add under the build tag:
```
		<extensions>
			<extension>
				<groupId>org.apache.maven.wagon</groupId>
				<artifactId>wagon-webdav</artifactId>
				<version>1.0-beta-2</version>
			</extension>
		</extensions>
```

# Deploy to nexus
Set the password for deployment user from nexus console and set the same in the settings.xml
on the project to deploy tun:
```
mvn deploy
```
# Deploy third party jars to nexus
Prepare a pom.xml like:
```
<project>
   <modelVersion>4.0.0</modelVersion>
   <groupId>oracle</groupId>
   <artifactId>oimclient</artifactId>
   <packaging>pom</packaging>
   <version>11.1.2</version>
   <name>Webdav Deployment POM</name>

   <build>
      <extensions>
         <extension>
            <groupId>org.apache.maven.wagon</groupId>
            <artifactId>wagon-webdav</artifactId>
            <version>1.0-beta-2</version>
         </extension>
      </extensions>
   </build>
</project>
```
Run commands like:
```
mvn deploy:deploy-file -Dfile=..\..\..\..\Operation\dependency-jars\oimclient-11.1.2.jar -D-Durl=dav:http://localhost:8081/nexus/content/repositories/thirdparty -DrepositoryId=my-company-nexus -DgroupId=oracle -DartifactId=oimclient -Dversion=11.1.2 -Dpackaging=jar
```
Reference: [https://www.chrissearle.org/2008/02/10/Deploying_jars_to_third_party_maven_repository_via_WebDAV/]
