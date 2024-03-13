FROM httpd:2.4.57@sha256:a86b8ccb1e65a555a1902bc12a92c908c8f264cc777fda4a6b79d1f9e6fdf78c
# "Created": "2023-04-12T01:47:36.486239565Z" , "Version":"2.4.57"

RUN apt-get update \
  && apt-get install -y --no-install-recommends wget ca-certificates libcjose0 libhiredis0.14 apache2-api-20120211 apache2-bin\
  && wget https://github.com/OpenIDC/mod_auth_openidc/releases/download/v2.4.15.4/libapache2-mod-auth-openidc_2.4.15.4-1.buster_amd64.deb \
  && dpkg -i libapache2-mod-auth-openidc_2.4.15.4-1.buster_amd64.deb \
  && ln -s /usr/lib/apache2/modules/mod_auth_openidc.so /usr/local/apache2/modules/mod_auth_openidc.so \
  && rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt \
  && touch /usr/local/apache2/conf/extra/secret.conf \
  && touch /usr/local/apache2/conf/extra/oidc.conf
RUN echo "\n\nLoadModule auth_openidc_module modules/mod_auth_openidc.so\n\nInclude conf/extra/secret.conf\nInclude conf/extra/oidc.conf\n" >> /usr/local/apache2/conf/httpd.conf