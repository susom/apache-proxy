FROM httpd:2.4.59@sha256:73b2e9e2861bcfe682b9a67d83433b6a6b36176459134aa25ec711058075fd47
# "Created": "2024-04-05T21:49:16Z" , "Version":"2.4.59"

RUN apt-get update -o APT::Update::Post-Invoke-Success="" \
  && apt-get install -y --no-install-recommends wget ca-certificates libcjose0 libhiredis0.14 apache2-api-20120211 apache2-bin \
  && wget https://github.com/OpenIDC/mod_auth_openidc/releases/download/v2.4.15.7/libapache2-mod-auth-openidc_2.4.15.7-1.bookworm_amd64.deb \
  && dpkg -i libapache2-mod-auth-openidc_2.4.15.7-1.bookworm_amd64.deb || apt-get install -f -y \
  && ln -s /usr/lib/apache2/modules/mod_auth_openidc.so /usr/local/apache2/modules/mod_auth_openidc.so \
  && rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt \
  && touch /usr/local/apache2/conf/extra/secret.conf \
  && touch /usr/local/apache2/conf/extra/oidc.conf
RUN echo "\n\nLoadModule auth_openidc_module modules/mod_auth_openidc.so\n\nInclude conf/extra/secret.conf\nInclude conf/extra/oidc.conf\n" >> /usr/local/apache2/conf/httpd.conf