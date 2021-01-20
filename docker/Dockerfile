# Dockerfile for universalresolver/driver-did-bbu

FROM universalresolver/base-ubuntu

# install dependencies

RUN apt-get -y update && \
    apt-get install -y --no-install-recommends software-properties-common gnupg && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 68DB5E88 && \
    add-apt-repository "deb https://repo.sovrin.org/sdk/deb xenial stable" && \
    apt-get install -y libindy=1.14.0 && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ARG GITHUB_READ_PACKAGES_OWNER
ARG GITHUB_READ_PACKAGES_TOKEN
ARG MAVEN_MASTER

ADD ./settings.xml /root/.m2/
RUN echo "<settingsSecurity><master>${MAVEN_MASTER}</master></settingsSecurity>" > /root/.m2/settings-security.xml

# build driver-did-bbu

ADD . /opt/driver-did-bbu
RUN cd /opt/driver-did-bbu && mvn clean install

# variables

ENV uniresolver_driver_did_bbu_libIndyPath=
# TODO: Update the poolConfigs
ENV uniresolver_driver_did_bbu_poolConfigs=
# TODO: Update the poolVersions
ENV uniresolver_driver_did_bbu_poolVersions=
ENV uniresolver_driver_did_bbu_walletName=default

# done

EXPOSE 8080

RUN chmod a+rx /opt/driver-did-bbu/docker/run-driver-did-bbu.sh
CMD "/opt/driver-did-bbu/docker/run-driver-did-bbu.sh"
