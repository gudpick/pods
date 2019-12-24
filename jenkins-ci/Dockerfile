FROM  jenkins/jenkins:lts
USER root 
# Plugins 
RUN /usr/local/bin/install-plugins.sh workflow-aggregator && \ 
/usr/local/bin/install-plugins.sh github && \ 
/usr/local/bin/install-plugins.sh ws-cleanup && \ 
/usr/local/bin/install-plugins.sh greenballs && \ 
/usr/local/bin/install-plugins.sh simple-theme-plugin && \ 
/usr/local/bin/install-plugins.sh kubernetes && \ 
/usr/local/bin/install-plugins.sh docker-workflow && \ 
/usr/local/bin/install-plugins.sh kubernetes-cli && \ 
/usr/local/bin/install-plugins.sh github-branch-source 

#install
RUN apt-get update && \
apt-get -y install apt-transport-https \
ca-certificates \
curl \
gnupg2 \
software-properties-common && \
curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
add-apt-repository \
"deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
$(lsb_release -cs) \
stable" && \
apt-get update && \
apt-get -y install docker-ce
RUN apt-get update && \
apt-get install -yq --no-install-recommends wget pwgen ca-certificates && \
apt-get clean && \
rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
apt-get install -y openjdk-8-jdk && \
apt-get install -y ant && \
apt-get clean
RUN apt-get update && \
apt-get install ca-certificates-java && \
apt-get clean && \
update-ca-certificates -f;
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/

RUN export JAVA_HOME

RUN wget http://mirrors.gigenet.com/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
RUN apt-get update -y && apt-get install maven -y



 

# Kubectl 

RUN wget https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x ./kubectl && mv ./kubectl /usr/local/bin/kubectl 


RUN chown -R root "$JENKINS_HOME" /usr/share/jenkins/ref 
