FROM httpd:2.4.60@sha256:86f9a3c03c32767e24c54013ffb63e314b4d2e267b28de5e8d7b7a42cf7202fc
# "Created": "2024-07-01T11:31:13Z" , "Version":"2.4.60"

RUN apt-get update \
  && apt-get install -y --no-install-recommends wget ca-certificates libcjose0 libhiredis0.14 apache2-api-20120211 apache2-bin libldap-2.5-0 libssl3 libldap-common \
  && apt-get check \
  && wget https://github.com/OpenIDC/mod_auth_openidc/releases/download/v2.4.15.7/libapache2-mod-auth-openidc_2.4.15.7-1.bookworm_amd64.deb \
  && dpkg -i libapache2-mod-auth-openidc_2.4.15.7-1.bookworm_amd64.deb \
  && ln -s /usr/lib/apache2/modules/mod_auth_openidc.so /usr/local/apache2/modules/mod_auth_openidc.so \
  #&& rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt \
  && touch /usr/local/apache2/conf/extra/secret.conf \
  && touch /usr/local/apache2/conf/extra/oidc.conf
RUN echo "\n\nLoadModule auth_openidc_module modules/mod_auth_openidc.so\n\nInclude conf/extra/secret.conf\nInclude conf/extra/oidc.conf\n" >> /usr/local/apache2/conf/httpd.conf
