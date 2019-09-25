#生成的新镜像以centos镜像为基础
FROM centos:7
MAINTAINER by bjp(bijianpeng@126.com)
#升级系统
RUN yum -y update
#安装openssh-server
RUN yum -y install openssh-server
RUN yum -y install openssh-clients
RUN yum -y install which
#安装jdk1.8
RUN yum -y install java-1.8.0-openjdk-devel

#生成需要的密钥
RUN rm -rf ssh*key
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key
RUN ssh-keygen -t ed25519 -f  /etc/ssh/ssh_host_ed25519_key

#宿主机免密登录
RUN mkdir -p /root/.ssh
ADD authorized_keys /root/.ssh/authorized_keys

#变更root密码为test
RUN echo "root:123456"|chpasswd

#开放窗口的22端口
EXPOSE 22

#运行脚本，启动sshd服务
CMD ["/usr/sbin/sshd", "-D"]
