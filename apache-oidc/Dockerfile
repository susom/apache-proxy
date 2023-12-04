FROM httpd:2.4.58@sha256:04551bc91cc03314eaab20d23609339aebe2ae694fc2e337d0afad429ec22c5a
# "Created": "2023-11-21T13:23:10.154145666Z", "Version":"2.4.58"

RUN apt-get update -qq \
    && apt-get install -y --no-install-recommends apt-utils wget ca-certificates libcjose0 libhiredis0.14 apache2-api-20120211 apache2-bin libldap-common \
    && rm -rf /var/lib/apt/lists/* \
    && wget https://github.com/OpenIDC/mod_auth_openidc/releases/download/v2.4.14.4/libapache2-mod-auth-openidc_2.4.14.4-1.bookworm_amd64.deb \
    && dpkg -i libapache2-mod-auth-openidc_2.4.14.4-1.bookworm_amd64.deb \
    && ln -s /usr/lib/apache2/modules/mod_auth_openidc.so /usr/local/apache2/modules/mod_auth_openidc.so \
    && rm libapache2-mod-auth-openidc_2.4.14.4-1.bookworm_amd64.deb \
    && rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt \
    && touch /usr/local/apache2/conf/extra/secret.conf \
    && touch /usr/local/apache2/conf/extra/oidc.conf

RUN echo "\nLoadModule auth_openidc_module modules/mod_auth_openidc.so\nInclude conf/extra/secret.conf\nInclude conf/extra/oidc.conf\n" >> /usr/local/apache2/conf/httpd.conf
