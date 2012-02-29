# personal maven repo

## about
This is a maven repo for all artifcats I use but where's no or no current version in the public maven repositories.

I created this repository following [this (my) blog post](http://coffeecoders.de/2011/09/using-github-as-a-personal-maven-repository/).

## What's in the box?

- [thumbnailator](http://code.google.com/p/thumbnailator/): A toolbox for easy image resizing etc.
 - versions [(Changelog)](http://code.google.com/p/thumbnailator/wiki/Changes): 0.4.0

More to come if needed.

## How to use this?

There are two ways to make maven aware of new repositories besides the pre-configured one. Either in `~/.m2/repositories/settings.xml` which would be global for every repository but just for your user account. Or you can add the information into the `pom.xml` of your project. Since we want all developers for this project to easily use the new repository we will use the later.

Open your `pom.xml` and add the following lines for our example. Of course you have to edit the group-id, artifact and version according to your lib.

	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
	    <modelversion>4.0.0</modelversion>
	    <!-- ... more project definition -->
	 
	    <dependencies>
	 
	        <dependency>
			<groupid>net.coobird</groupid>
			<artifactid>thumbnailator</artifactid>
			<version>0.4.0</version>
	        </dependency>
	        <!-- more dependecies... -->
	    </dependencies>
	 
	    <!-- build config etc. ... -->
	 
	    	<repositories>
			<repository>
				<id>stefanhoth-snapshots</id>
				<url>https://raw.github.com/stefanhoth/mavenrepo/master/snapshots</url>
				<releases>
					<enabled>false</enabled>
					<updatepolicy>always</updatepolicy>
					<checksumpolicy>warn</checksumpolicy>
				</releases>
				<snapshots>
					<enabled>true</enabled>
					<updatepolicy>never</updatepolicy>
					<checksumpolicy>fail</checksumpolicy>
				</snapshots>
			</repository>
			<repository>
				<id>stefanhoth-releases</id>
				<releases>
					<enabled>true</enabled>
					<updatepolicy>always</updatepolicy>
					<checksumpolicy>fail</checksumpolicy>
				</releases>
				<snapshots>
					<enabled>false</enabled>
					<updatepolicy>always</updatepolicy>
					<checksumpolicy>warn</checksumpolicy>
				</snapshots>
				<url>https://raw.github.com/stefanhoth/mavenrepo/master/releases</url>
			</repository>
		</repositories>
	</project>
