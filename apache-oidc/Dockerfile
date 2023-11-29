FROM httpd:2.4.58@sha256:2f1ec45327a35711f293cf543c2e0efadfd44bc71e8081dcd76a558b99778005
# "Created": "2023-10-19T19:22:10.741880566Z" , "Version":"2.4.58"

RUN apt-get update \
  && apt-get install -y --no-install-recommends apt-utils

RUN apt-get install -y --no-install-recommends wget ca-certificates libcjose0 libhiredis0.14 apache2-api-20120211 apache2-bin libldap-common \
  && wget https://github.com/OpenIDC/mod_auth_openidc/releases/download/v2.4.14.4/libapache2-mod-auth-openidc_2.4.14.4-1.bookworm_amd64.deb \
  && dpkg -i libapache2-mod-auth-openidc_2.4.14.4-1.bookworm_amd64.deb \
  && ln -s /usr/lib/apache2/modules/mod_auth_openidc.so /usr/local/apache2/modules/mod_auth_openidc.so \
  && rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt \
  && touch /usr/local/apache2/conf/extra/secret.conf \
  && touch /usr/local/apache2/conf/extra/oidc.conf

RUN echo "\n\nLoadModule auth_openidc_module modules/mod_auth_openidc.so\n\nInclude conf/extra/secret.conf\nInclude conf/extra/oidc.conf\n" >> /usr/local/apache2/conf/httpd.conf
