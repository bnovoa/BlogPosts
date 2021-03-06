title: Docker: Simple script with Java8, Jetty, Scala, Git
tags: docker

We'll run this from ubuntu trusty.

    FROM ubuntu:trusty-20160711
    # Install ubuntu instllation tools and the java 8 repo
    RUN apt-get update && apt-get -y install software-properties-common && add-apt-repository -y ppa:webupd8team/java
    # Auto accept the java 8 licence
    RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
    RUN echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections
    # Install java8, git and wget
    RUN apt-get update && apt-get -y install oracle-java8-installer git wget vim
    # Download and install scala 2.11.8
    RUN wget http://downloads.lightbend.com/scala/2.11.8/scala-2.11.8.deb && dpkg -i scala-2.11.8.deb
    # Download the jetty runner web server
    RUN wget http://central.maven.org/maven2/org/eclipse/jetty/jetty-runner/9.4.0.M0/jetty-runner-9.4.0.M0.jar
    # Ignore this if you don't want something run on every container start
    ENTRYPOINT /bin/bash -c "ls /"
