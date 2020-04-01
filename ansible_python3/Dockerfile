RUN yum -y install wget; \
    yum -y groupinstall "Development tools"; \
    yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel libffi-devel; \
    wget https://www.python.org/ftp/python/3.8.0/Python-3.8.0.tgz; \
    tar -zxvf  Python-3.8.0.tgz; \
    cd Python-3.8.0; \
    ./configure --prefix=/usr/local/python3; \
    make && make install; \
    ln -s /usr/local/python3/bin/python3.8 /usr/local/bin/python3; \
    ln -s /usr/local/python3/bin/pip3.8 /usr/local/bin/pip3; \
    pip3 install --upgrade pip && pip3 install openpyxl && pip3 install requests
