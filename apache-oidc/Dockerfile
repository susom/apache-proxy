FROM httpd:2.4.71@sha256:19310e146a08911733b7a7703ddff97b6d8d510d4bc1e38a252db934e7437447
# "Created": "2026-11-11T23:00:31.856985033Z", "Version":"2.4.71", VERSION="13 (trixie)"

RUN apt-get update \
  && apt-get install -y --no-install-recommends wget ca-certificates libcjose0 libhiredis1.1.0 apache2-api-20120211 apache2-bin libldap2 libssl3 libldap-common \
  && apt-get check \
  && wget https://github.com/OpenIDC/mod_auth_openidc/releases/download/v2.4.20.4/libapache2-mod-auth-openidc_2.4.20.4-1.trixie_amd64.deb \
  && dpkg -i libapache2-mod-auth-openidc_2.4.20.4-1.trixie_amd64.deb \
  && ln -s /usr/lib/apache2/modules/mod_auth_openidc.so /usr/local/apache2/modules/mod_auth_openidc.so \
  #&& rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt \
  && touch /usr/local/apache2/conf/extra/secret.conf \
  && touch /usr/local/apache2/conf/extra/oidc.conf
RUN echo "\n\nLoadModule auth_openidc_module modules/mod_auth_openidc.so\n\nInclude conf/extra/secret.conf\nInclude conf/extra/oidc.conf\n" >> /usr/local/apache2/conf/httpd.conf
