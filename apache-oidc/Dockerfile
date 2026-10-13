FROM httpd:2.4.69@sha256:c842ac797bd1fe8b3cd26d002ac9d948aa2814097544600600b35aef42e6785a
# "Created": "2026-10-06T01:18:54.038574862Z", "Version":"2.4.69", VERSION="13 (trixie)"

RUN apt-get update \
  && apt-get install -y --no-install-recommends wget ca-certificates libcjose0 libhiredis1.1.0 apache2-api-20120211 apache2-bin libldap2 libssl3 libldap-common \
  && apt-get check \
  && wget https://github.com/OpenIDC/mod_auth_openidc/releases/download/v2.4.20.3/libapache2-mod-auth-openidc_2.4.20.3-1.trixie_amd64.deb \
  && dpkg -i libapache2-mod-auth-openidc_2.4.20.3-1.trixie_amd64.deb \
  && ln -s /usr/lib/apache2/modules/mod_auth_openidc.so /usr/local/apache2/modules/mod_auth_openidc.so \
  #&& rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt \
  && touch /usr/local/apache2/conf/extra/secret.conf \
  && touch /usr/local/apache2/conf/extra/oidc.conf
RUN echo "\n\nLoadModule auth_openidc_module modules/mod_auth_openidc.so\n\nInclude conf/extra/secret.conf\nInclude conf/extra/oidc.conf\n" >> /usr/local/apache2/conf/httpd.conf
