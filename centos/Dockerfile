FROM centos:centos7

RUN yum install epel-release -y \ 
    && yum install initscripts -y \
    && yum install openssh-server openssh-clients supervisor -y \

#修改root用户密码
#用以下命令修改密码时，密码中最好不要包含特殊字符，如"!"，否则可能会失败；
    && /bin/echo "123456" | passwd --stdin root \

#生成密钥
    && ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key \
    && ssh-keygen -t rsa -f /etc/ssh/ssh_host_ecdsa_key \
    && ssh-keygen -t rsa -f /etc/ssh/ssh_host_ed25519_key \
    && ssh-keygen -t rsa -f ~/.ssh/id_rsa \

#修改配置信息
    && /bin/sed -i 's/.*session.*required.*pam_loginuid.so.*/session optional pam_loginuid.so/g' /etc/pam.d/sshd \
    && /bin/sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config \
    && /bin/sed -i "s/#UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config

COPY supervisord.conf /etc/supervisord.conf

EXPOSE 22

CMD /usr/bin/supervisord
