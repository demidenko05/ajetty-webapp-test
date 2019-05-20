site: https://sites.google.com/site/beigesoftware

Test web-application for A-Jetty.

License:

BSD 2-Clause License
https://sites.google.com/site/beigesoftware/bsd2csl

The best and only lawful way of using A-Jetty is use it as embedded server in standalone WEB-application with precompiled JSP.
See beige-accounting-ajetty and beige-accounting-android for example

It's only for tests purposes!!! It doesn't comply to the latest Android policy (loading executable binaries from outside)!!!

To make this WEB-app with JSP working on non-embedded Android A-Jetty you should:
1. Install A-Tomcat, Apache Ant, Maven ... see https://github.com/demidenko05/a-tomcat-all
2. Precompile JSP to Java Servlets with Ant and A-Tomcat by run in the root of "ajetty-webapp-test":
  $ANT_HOME/bin/ant -Dtomcat.home=$TOMCATA_HOME -Dwebapp.path=target/ajetty-webapp-test/
4. Copy generated Java files to source and copy servlets configuration from generated_web.xml into web.xml
5. install maven project again
5. make DEX file from classes (in target folder):
  * Unpack all jars into WEB-INF/classes folder in proper order to remove duplicates
  * inside WEB-INF run:
     java -jar $ANDROID_HOME/build-tools/[tools-version]/lib/dx.jar --dex --output=dex-classes.jar classes/
  * sing jar "jarsigner dex-classes.jar [yourkeyalias]"
  * check align jar "$ANDROID_HOME/build-tools/[tools-version]/zipalign -c -v 4 dex-classes.jar"
  * align jar if need "$ANDROID_HOME/build-tools/[tools-version]/zipalign -v 4 dex-classes.jar dex-classes-al.jar"
  * move dex-classes-al.jar into WEB-INF/lib
  * remove unneeded classes form WEB-INF/classes, old jars and JSP files
6. place this unpacked web-app into [Android ext.files dir]/A-Jetty/webapps
7. start A-Jetty on Android, your web-app will be listed.
