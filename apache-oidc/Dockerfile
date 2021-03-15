FROM httpd:2.4.46@sha256:9625118824bc2514d4301b387c091fe802dd9e08da7dd9f44d93ee65497e7c1c
# "Created": "2021-03-12T11:00:17.745973624Z" , "Version":"2.4.46"

RUN apt-get update \
  && apt-get install -y --no-install-recommends wget ca-certificates libcjose0 libhiredis0.14 apache2-api-20120211 apache2-bin\
  && wget https://github.com/zmartzone/mod_auth_openidc/releases/download/v2.4.6/libapache2-mod-auth-openidc_2.4.6-1.buster+1_amd64.deb \
  && dpkg -i libapache2-mod-auth-openidc_2.4.6-1.buster+1_amd64.deb \
  && ln -s /usr/lib/apache2/modules/mod_auth_openidc.so /usr/local/apache2/modules/mod_auth_openidc.so \
  && rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt \
  && touch /usr/local/apache2/conf/extra/secret.conf \
  && touch /usr/local/apache2/conf/extra/oidc.conf

RUN echo "\n\nLoadModule auth_openidc_module modules/mod_auth_openidc.so\n\nInclude conf/extra/secret.conf\nInclude conf/extra/oidc.conf\n" >> /usr/local/apache2/conf/httpd.conf
