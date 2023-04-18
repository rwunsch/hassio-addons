# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

# Execute during the build of the image
ARG QLCPLUS_VERSION BUILD_ARCH

RUN \
	apk update &&\
	apk add --no-cache g++ make git build-essential qtchooser qt5-qmake qtbase5-dev qtbase5-dev-tools qtscript5-dev qtmultimedia5-dev libqt5multimedia5-plugins qttools5-dev-tools fakeroot debhelper devscripts pkg-config libxml2-utils libglib2.0-dev libpulse-dev &&\
	apk add --no-cache libasound2-dev libusb-1.0-0-dev libftdi1-dev libudev-dev libmad0-dev libsndfile1-dev libfftw3-dev

RUN \
    curl -sSLf -o /usr/bin/qlcplus \
    "https://github.com/mcallegari/qlcplus/archive/refs/tags/QLC+_${QLCPLUS_VERSION}.tar.gz"
    
RUN \
    cd /usr/bin/qlcplus &&\
    tar -xf QLC+_${QLCPLUS_VERSION}.tar.gz &&\
    rm QLC+_${QLCPLUS_VERSION}.tar.gz

RUN qmake
RUN make
RUN su -c "make install"

# Copy root filesystem
COPY rootfs /


