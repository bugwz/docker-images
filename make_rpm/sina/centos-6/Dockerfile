FROM centos:6
MAINTAINER bugwz wenzhuang@staff.weibo.com
COPY ./files/ /etc/yum.repos.d/
RUN cd /etc/yum.repos.d/ \
    && rm -f CentOS-Media.repo CentOS-Debuginfo.repo CentOS-Vault.repo \
    && yum install -y yum-plugin-ovl yum-presto yum-utils wget git gcc gcc-c++ autoconf automake zlib-devel openssl-devel pcre-devel rpm-build \
    && yum localinstall -y --nogpgcheck devtoolset-2-binutils-2.23.52.0.1-10.el6.x86_64.rpm devtoolset-2-gcc-4.8.2-15.el6.x86_64.rpm devtoolset-2-gcc-c++-4.8.2-15.el6.x86_64.rpm \
    && rm -f devtoolset-2-binutils-2.23.52.0.1-10.el6.x86_64.rpm devtoolset-2-gcc-4.8.2-15.el6.x86_64.rpm devtoolset-2-gcc-c++-4.8.2-15.el6.x86_64.rpm \
    && ln -s /opt/rh/devtoolset-2/root/usr/bin/* /usr/local/bin/ \
    && hash -r \
    && git config --global user.email "mkrpm@weibo.com" \
    && git config --global user.name "mkrpm" \
    && mkdir /data0 \
    && mv /etc/yum.repos.d/gperftools-2.7.tar.gz /data0/ \
    && cd /data0/ \
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
