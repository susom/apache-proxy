FROM httpd:2.4.48@sha256:71ef66ba5d278ec4f636412424b8778ce4a8a56083b6e05b10d553a60364758b
# "Created": 2021-09-03T06:56:40.263369583Z , "Version":"2.4.48"

RUN apt-get update \
  && apt-get install -y --no-install-recommends wget ca-certificates libcjose0 libhiredis0.14 apache2-api-20120211 apache2-bin\
  && wget https://github.com/zmartzone/mod_auth_openidc/releases/download/v2.4.9.4/libapache2-mod-auth-openidc_2.4.9.4-1.buster+1_amd64.deb \
  && dpkg -i libapache2-mod-auth-openidc_2.4.9.4-1.buster+1_amd64.deb \
  && ln -s /usr/lib/apache2/modules/mod_auth_openidc.so /usr/local/apache2/modules/mod_auth_openidc.so \
  && rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt \
  && touch /usr/local/apache2/conf/extra/secret.conf \
  && touch /usr/local/apache2/conf/extra/oidc.conf

RUN echo "\n\nLoadModule auth_openidc_module modules/mod_auth_openidc.so\n\nInclude conf/extra/secret.conf\nInclude conf/extra/oidc.conf\n" >> /usr/local/apache2/conf/httpd.conf
