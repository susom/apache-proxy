[![Build Status](https://travis-ci.com/susom/apache-proxy.svg?token=esQWdxUhyEmyjhvCqRJJ&branch=master)](https://travis-ci.com/susom/apache-proxy)
[![Docker Hub](https://img.shields.io/docker/pulls/somrit/apache-oidc.svg)](https://hub.docker.com/r/somrit/apache-oidc)

# Authenticating Reverse Proxy (Apache + mod_auth_openidc)

This repository contains a recipe to generate a Docker image useful for acting as a reverse proxy for authentication in front of an application.
It contains a stripped down Apache with minimal modules, and adds the mod_auth_openidc module for performing OpenID Connect authentication.

There are some instructions and sample configuration files in the [apache-oidc-test directory](apache-oidc-test/README.md).
