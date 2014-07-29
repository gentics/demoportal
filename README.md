# Gentics Demoportal #

## Install Eclipse Indigo JEE (Including egit, m2e, m2e-wtp) ##

## Preparation ##

* Add the license information to your maven profile (settings.xml)

```xml
    <profiles>
        ...
        <profile>
            <id>gentics.license</id>
            <properties>
                    <gentics.gpn.licensekey>YOUR_LICENSE_KEY</gentics.gpn.licensekey>
            </properties>
        </profile>
        ...
    </profiles>
    <activeProfiles>
        <activeProfile>SDK</activeProfile>
        <activeProfile>gentics.license</activeProfile>
    </activeProfiles>
```

* Import all projects and invoke project clean

* Create a new Apache Tomcat 7 server instance and add the following webapps:

** demoportal-webapp
** demoportal-portalnode-webapp
** demoportal-genticsimagestore-webapp

* Add the following argument to your Server VM Arguments:

```
  -Dworkspace.dir=${workspace_loc}
  -Dcom.gentics.portalnode.confpath=${workspace_loc}/demoportal/demoportal-config/target/portal_configuration
  -Dcatalina.config=file://${workspace_loc}/demoportal/demoportal-config/src/main/eclipse-conf/catalina.properties
```

* Make sure you invoked 'Publish' for your Server in order to update the used Server settings.
