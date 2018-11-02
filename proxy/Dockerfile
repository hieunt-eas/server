FROM centos:latest

MAINTAINER "Nguyen Trong Hieu" <tronghieudev@gmail.com>

RUN yum -y install haproxy

COPY ./conf/haproxy.cfg /etc/haproxy/

RUN systemctl enable haproxy \
&& chkconfig haproxy on

CMD ["/sbin/init"]
