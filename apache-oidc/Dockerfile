FROM httpd:2.4.54@sha256:c9eba4494b9d856843b49eb897f9a583a0873b1c14c86d5ab77e5bdedd6ad05d
# "Created": "2022-06-08T18:45:46.260791323Z" , "Version":"2.4.54"

RUN apt-get update \
  && apt-get install -y --no-install-recommends wget ca-certificates libcjose0 libhiredis0.14 apache2-api-20120211 apache2-bin\
  && wget https://github.com/zmartzone/mod_auth_openidc/releases/download/v2.4.11.3/libapache2-mod-auth-openidc_2.4.11.3-1.buster+1_amd64.deb \
  && dpkg -i libapache2-mod-auth-openidc_2.4.11.3-1.buster+1_amd64.deb \
  && ln -s /usr/lib/apache2/modules/mod_auth_openidc.so /usr/local/apache2/modules/mod_auth_openidc.so \
  && rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt \
  && touch /usr/local/apache2/conf/extra/secret.conf \
  && touch /usr/local/apache2/conf/extra/oidc.conf

RUN echo "\n\nLoadModule auth_openidc_module modules/mod_auth_openidc.so\n\nInclude conf/extra/secret.conf\nInclude conf/extra/oidc.conf\n" >> /usr/local/apache2/conf/httpd.conf
