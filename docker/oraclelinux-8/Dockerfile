FROM docker.io/oraclelinux:8
MAINTAINER Pacur <contact@pacur.org>

RUN yum -y install oracle-epel-release-el8

RUN yum -y install yum-utils
RUN yum-config-manager --enable ol8_appstream
RUN yum-config-manager --enable ol8_addons
RUN yum-config-manager --enable ol8_codeready_builder

RUN yum -y upgrade
RUN yum -y groupinstall 'Development Tools'
RUN yum -y install tar expect rpm-build rpm-sign openssl createrepo rsync make automake gcc wget zip git mercurial

RUN wget https://golang.org/dl/go1.17.1.linux-amd64.tar.gz
RUN echo "dab7d9c34361dc21ec237d584590d72500652e7c909bf082758fb63064fca0ef go1.17.1.linux-amd64.tar.gz" | sha256sum -c -
RUN tar -C /usr/local -xf go1.17.1.linux-amd64.tar.gz
RUN rm -f go1.17.1.linux-amd64.tar.gz

ENV GOPATH /go
ENV PATH /usr/local/go/bin:$PATH:/go/bin
ENV GO111MODULE off

RUN go get github.com/pacur/pacur

ENTRYPOINT ["pacur"]
CMD ["build", "oraclelinux-8"]
