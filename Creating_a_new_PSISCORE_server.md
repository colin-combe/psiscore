# Web Service reference implementation #
The source code of the PSISCORE web service reference implementation can be found in the [download](http://code.google.com/p/psiscore/downloads/list) or the [source](http://code.google.com/p/psiscore/source/checkout) section of the PSISCORE project site. Please note that you will need to add your own [ScoreCalculator](ScoreCalculator.md) to this reference implementation.

## Building a new PSISCORE service ##
The PSISCORE reference implementation relies on [Apache Maven 2](http://maven.apache.org/) for managing Java dependencies and project settings. In order to build your own PSISCORE server from the source code provided you therefore only need to start the Maven build process. If you do not have a local installation of Maven, you can download the software and extensive documentation on how to use it on the [Maven homepage](http://maven.apache.org/).

Once you installed Maven, you can start compiling the PSISCORE sources. The source code of the reference implementation contains a `pom.xml` file with Maven specific instructions. You can start the build process by issuing the following command in the directory where the `pom.xml` file is located:

`mvn clean install`

Maven will then download all the Java libraries required by the PSISCORE reference implementation, compile the source code, and package it into a web archive (war) file.

## Testing the PSISCORE service ##
Once the Maven build process has finished, you can deploy the web archive into a dedicated servlet container, such as [Apache Tomcat](http://tomcat.apache.org/) or [Jetty](http://jetty.codehaus.org/jetty/).

### Apache Tomcat ###
After placing the war file into the `webapps` folder of your Apache Tomcat installation (see the documentation at  [Apache Tomcat](http://tomcat.apache.org/) for instructions on how to obtain a local server installation), you can start the server and access its test page in your local browser (without changes to its configuration, the URL will be "http://localhost:8080/" followed by the PSISCORE directory name within the webapps directory, for instance "psiscore-ws/". If everything went well, you will see a test page that will contain the web service description of your PSISCORE service.

### Jetty ###
An even easier way, especially for quickly testing your PSISCORE service, is to use the [Jetty](http://jetty.codehaus.org/jetty/) server that is already configured in the PSISCORE Maven configuration file. To start Jetty right after the build process has finished, you need to add `jetty:run` to the build command described above:

`mvn clean install jetty:run`

Again, if you then go to your browser and check your localhost, you can see the aforementioned test page and the web service description of your PSISCORE service.

# Implementing a new scoring routine #
Before you will be able to serve your confidence scores, you will need to write a [ScoreCalculator](ScoreCalculator.md) that knows how to access your data or calculate the scores. Please see the [implementation details](PSISCORE_web_service_implementation_details.md) for detailed instructions, how to adapt the source code of the reference implementation to your needs.