FROM httpd:2.4

RUN apt-get update \
  && apt-get install -y --no-install-recommends ca-certificates libapache2-mod-auth-openidc \
  && ln -s /usr/lib/apache2/modules/mod_auth_openidc.so /usr/local/apache2/modules/mod_auth_openidc.so \
  && rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt \
  && touch /usr/local/apache2/conf/extra/secret.conf \
  && touch /usr/local/apache2/conf/extra/oidc.conf

RUN echo "\n\nLoadModule auth_openidc_module modules/mod_auth_openidc.so\n\nInclude conf/extra/secret.conf\nInclude conf/extra/oidc.conf\n" >> /usr/local/apache2/conf/httpd.conf
