ARG VERSION

FROM httpd:$VERSION

ARG GLOBAL_LOG
ARG WWW_UID
ARG WWW_USERNAME
ARG WWW_GID
ARG WWW_GROUPNAME

RUN groupadd -g $WWW_GID $WWW_GROUPNAME \
  && useradd -u $WWW_UID -g $WWW_GID -r -s /bin/false $WWW_USERNAME \
  && mv /usr/local/apache2/conf/httpd.conf /usr/local/apache2/conf/httpd.conf.bak \
  && apt-get update \
  && apt-get install -y sudo


# OpenID Connect
# - installation of openidc module first already enabled the needed apache configs
# - after, we just compile and overwrite the module
#RUN apt-get install -y libapache2-mod-auth-openidc

RUN  apt-get install -y git apache2-dev libssl-dev libcurl4-openssl-dev libjansson-dev libcjose-dev libpcre++-dev pkg-config \
    && mkdir /usr/lib/apache2/ \
    && mkdir /usr/lib/apache2/modules \
    && git clone https://github.com/zmartzone/mod_auth_openidc.git \
    && cd mod_auth_openidc/ \
    && git checkout v2.4.1 \
    && ./autogen.sh \
    && autoreconf -fi \
    && ./configure CFLAGS="-g -O0" LDFLAGS="-lrt" \
    && make clean && make test \
    && make install \
    && cp /usr/lib/apache2/modules/mod_auth_openidc.so /usr/local/apache2/modules/




#RUN apt-get install -y libapache2-mod-auth-openidc

#https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=759209
#  && ln -s /etc/apache2/mods-available/auth_openidc.conf /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/auth_openidc.load /etc/apache2/mods-enabled/
#  && ln -s /etc/apache2/mods-available/http2.conf /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/http2.load /etc/apache2/mods-enabled/ \

# auth_form, request, session, session_cookie and session_crypto are needed for apache session support

#RUN ln -s /etc/apache2/mods-available/auth_digest.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/auth_form.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/authz_groupfile.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/expires.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/headers.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/lbmethod_bytraffic.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/proxy.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/proxy_html.conf /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/proxy_html.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/proxy_http.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/proxy_balancer.conf /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/proxy_balancer.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/proxy_wstunnel.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/request.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/session.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/session_cookie.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/session_crypto.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/slotmem_shm.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/socache_shmcb.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/ssl.conf /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/ssl.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/substitute.load /etc/apache2/mods-enabled/ \
#  && ln -s /etc/apache2/mods-available/xml2enc.load /etc/apache2/mods-enabled/ \
#  && sed -i "s@ErrorLog.*@ErrorLog $GLOBAL_LOG/error.log@g" /etc/apache2/apache2.conf \
#  && sed -i "s/Include ports\.conf/#Include ports\.conf/g" /etc/apache2/apache2.conf \
#  && echo 'Include /etc/apache2/_.ansible.server.conf' >> /etc/apache2/apache2.conf \
#  && echo 'Include /etc/apache2/_.ansible.vhost.d/*.conf' >> /etc/apache2/apache2.conf
