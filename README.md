# Gentics Portal.Node Java Demoportal #

## Install Eclipse JEE (Including egit, m2e, m2e-wtp) ##

[Portal.Node Maven IDE Guide](http://www.gentics.com/Portal.Node/guides/maven_ide.html)

## Preparation ##

* Add the license information to your maven profile (settings.xml)

```xml
    <profiles>
        …
        <profile>
            <id>gentics.license</id>
            <properties>
                <gentics.gpn.licensekey>YOUR_LICENSE_KEY</gentics.gpn.licensekey>
            </properties>
        </profile>
        …
    </profiles>
    <activeProfiles>
        <activeProfile>gentics.license</activeProfile>
    </activeProfiles>
```

## Database Setup ##

The following two databases are needed in order to provide demo content for the Demo Portal.

```
# CCR
echo "CREATE DATABASE contentrepository" | mysql -u root -p
mysql -u root -p contentrepository < demoportal/demoportal-config/src/main/sql/contentrepository.sql

# PCR
echo "CREATE DATABASE contentrepository_portal" | mysql -u root -p
mysql -u root -p contentrepository_portal < demoportal/demoportal-config/src/main/sql/contentrepository_portal.sql
```

By default the demoportal tries to access your local mysql server on port 3306 with the login: __root/finger__. You can modify your credentials by updating your __gentics.demoportal__ maven profile.

## Import in Eclipse ##

* Import all projects and invoke project clean

* Create a new Apache Tomcat 8 server instance and add the following webapps:

  * demoportal-webapp
  * demoportal-portalnode-webapp
  * demoportal-genticsimagestore-webapp

* Add the following argument to your Server VM arguments:

```
  -Dworkspace.dir=${workspace_loc}
  -Dcom.gentics.portalnode.confpath=${workspace_loc}/demoportal/demoportal-config/target/portal_configuration
  -Dcatalina.config=file://${workspace_loc}/demoportal/demoportal-config/src/main/eclipse-conf/catalina.properties
```

NOTE: Make sure you are not inserting any linebreaks in the VM arguments.

* Make sure you invoked 'Publish' for your Server in order to update the used Server settings.

## Accessing the Demo

Once the demo server is up and running you can access the webapp via: <http://localhost:8080/Portal.Node/portal>

## Profile Handling

The configuration for prod, dev, test and local (IDE) environments often requires different settings. 
The this project includes example profiles which can be used to build the project using custom settings. 
Maven will use the _local_ profile if an Eclipse IDE environment was detected. Otherwise a profile must be specified to build this project.

Please note that the properties within the _config.*.properties_ file are only be used to replace settings within the configuration files (e.g.: default.portal.xml). 
The settings in those files are not used to configure maven.

## Building 

You may build the whole distribution package which includes all settings and a Apache Tomcat server via maven:

```
mvn -Pprod,\!local clean package
```

You can now use this package file to build your own docker image or deploy it straight to your server.
