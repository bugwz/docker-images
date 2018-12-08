FROM centos:7
MAINTAINER bugwz wenzhuang@staff.weibo.com
COPY ./files/ /etc/yum.repos.d/
RUN cd /etc/yum.repos.d \
    && rm -f CentOS-Sources.repo CentOS-Debuginfo.repo CentOS-Media.repo CentOS-Vault.repo CentOS-CR.repo \
    && yum install -y @buildsys-build yum-plugin-ovl automake autoconf libtool make gcc gcc-c++ which sudo wget git libunwind-devel zlib-devel openssl-devel pcre-devel rpm-build \
    && git config --global user.email "mkrpm@weibo.com" \
    && git config --global user.name "mkrpm" \
    && mkdir /data0 \
    && cd /data0 \
    && mv /etc/yum.repos.d/gperftools-2.7.tar.gz /data0/ \
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
