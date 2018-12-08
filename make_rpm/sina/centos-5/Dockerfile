FROM centos:5.11
MAINTAINER bugwz wenzhuang@staff.weibo.com
COPY ./files/ /etc/yum.repos.d/
RUN cd /etc/yum.repos.d \
    && rm -f CentOS-Sources.repo CentOS-Debuginfo.repo CentOS-Media.repo CentOS-Vault.repo \
    && yum install -y @buildsys-build wget automake libtool gcc gcc-c++ curl curl-devel make rsync tcl which build-essential tk gettext zlib-devel openssl-devel pcre-devel rpm-build \
    && yum localinstall -y --nogpgcheck /etc/yum.repos.d/devtoolset-2-binutils-2.23.52.0.1-10.el5.x86_64.rpm \
    && yum localinstall -y --nogpgcheck /etc/yum.repos.d/devtoolset-2-gcc-4.8.2-15.el5.x86_64.rpm \
    && yum localinstall -y --nogpgcheck /etc/yum.repos.d/devtoolset-2-gcc-c++-4.8.2-15.el5.x86_64.rpm \
    && rm -f /etc/yum.repos.d/devtoolset-2-binutils-2.23.52.0.1-10.el5.x86_64.rpm /etc/yum.repos.d/devtoolset-2-gcc-4.8.2-15.el5.x86_64.rpm /etc/yum.repos.d/devtoolset-2-gcc-c++-4.8.2-15.el5.x86_64.rpm \
    && ln -s /opt/rh/devtoolset-2/root/usr/bin/* /usr/local/bin/ \
    && hash -r \
    && mkdir /data0 \
    && cd /data0 \
    && wget http://cdn.bugwz.com/git-2.9.4.tar.gz \
    && tar xzvf git-2.9.4.tar.gz \
    && cd git-2.9.4 \
    && autoconf \
    && ./configure \
    && make \
    && make install \
    && git config --global user.email "mkrpm@weibo.com" \
    && git config --global user.name "mkrpm" \
    && wget http://cdn.bugwz.com/gperftools-2.7.tar.gz \
    && tar zxvf gperftools-2.7.tar.gz \
    && cd gperftools-2.7 \
    && ./configure \
    && make \
    && make install \
    && cp /usr/local/lib/libtcmalloc.so.4.5.3 /usr/lib64/libtcmalloc.so \
    && mkdir -p ~/rpmbuild/{BUILD,RPMS,S{OURCES,PECS,RPMS}} \
    && echo "%_topdir %(echo $HOME)/rpmbuild" > ~/.rpmmacros \
    && cd / \
    && rm -rf /data0/
