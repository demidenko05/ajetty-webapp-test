site: http://www.beigesoft.org
or https://sites.google.com/site/beigesoftware

Test web-application for A-Jetty.

Licenses:

GNU General Public License version 2
http://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html

The best way of using A-Jetty is use it as embedded server in standalone WEB-application with precompiled JSP.
See https://github.com/demidenko05/beige-software beige-accounting-ajetty and beige-accounting-android for example

To make this WEB-app with JSP working on non-embedded Android A-Jetty you should:
1. Install A-Tomcat, Apache Ant, Maven ... see https://github.com/demidenko05/a-tomcat-all
2. Precompile JSP to Java Servlets with Ant and A-Tomcat by run in the root of "ajetty-webapp-test":
  $ANT_HOME/bin/ant -Dtomcat.home=$TOMCATA_HOME -Dwebapp.path=target/ajetty-webapp-test/
4. Compile generated Java files and copy servlets configuration from generated_web.xml into web.xml
5. make DEX file from classes:
  * Unpack all jars into WEB-INF/classes folder in proper order to remove duplicates
  * inside WEB-INF run:
     java -jar $ANDROID_HOME/build-tools/[tools-version]/lib/dx.jar --dex --output=dex-classes.jar classes/
  * move dex-classes.jar into WEB-INF/lib
  * remove unneeded classes form WEB-INF/classes, old jars and JSP files
6. place this web-app into [Android ext.files dir]/A-Jetty/webapps
7. start A-Jetty on Android, your web-app will be listed.
