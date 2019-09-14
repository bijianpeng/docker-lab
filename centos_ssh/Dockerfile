#生成的新镜像以centos镜像为基础
FROM centos:7
MAINTAINER by bjp(bijianpeng@126.com)
#升级系统
RUN yum -y update
#安装openssh-server
RUN yum -y install openssh-server
#安装jdk1.8
RUN yum -y install java-1.8.0-openjdk

#修改/etc/ssh/sshd_config
#RUN sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config

#将密钥文件复制到/etc/ssh/目录中
#ADD ssh_host_rsa_key /etc/ssh/ssh_host_rsa_key
#ADD ssh_host_rsa_key.pub /etc/ssh/ssh_host_rsa_key.pub

#生成需要的密钥
RUN rm -rf ssh*key
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key
RUN ssh-keygen -t ed25519 -f  /etc/ssh/ssh_host_ed25519_key

#宿主机免密登录
RUN mkdir -p /root/.ssh
ADD authorized_keys /root/.ssh/authorized_keys
#将ssh服务启动脚本复制到/usr/local/sbin目录中，并改变权限为755
ADD run.sh /usr/local/sbin/run.sh
RUN chmod 755 /usr/local/sbin/run.sh
#变更root密码为test
RUN echo "root:123456"|chpasswd
#开放窗口的22端口
EXPOSE 22
#运行脚本，启动sshd服务
#CMD ["/usr/local/sbin/run.sh"]
CMD ["/usr/sbin/sshd", "-D"]
