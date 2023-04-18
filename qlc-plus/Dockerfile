# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

# Execute during the build of the image
ARG QLCPLUS_VERSION BUILD_ARCH

# missing dependencies: debhelper devscripts
RUN \
	apk update &&\
	apk add --no-cache g++ make git dpkg build-base fakeroot pkgconfig libxml2-utils

# missing dependencies: qmake-qt5
RUN apk add --no-cache \
		qt5-qtbase \
		qt5-qtdeclarative \
		qt5-qtwebsockets \
		qt5-qtsvg \
		qt5-qtconnectivity \
		qt5-qtcharts \
		qt5-qttools \
		qt5-qtx11extras \
		qt5-qtserialport \
		qt5-qtremoteobjects \
		qt5-qtscript \
		qt5-qtimageformats \
		qt5-qttranslations \
		glib-dev \
		libpulse

# missing dependencies: qtchooser libqt5multimedia5-plugins
RUN \
	apk add --no-cache \
		alsa-lib-dev \
		libusb \
		libftdi1 \
		eudev \
		libmad \
		libsndfile \
		fftw

RUN \
    mkdir  /tmp/qlcplus-build &&\
    cd /tmp/qlcplus-build
    
RUN \
    curl -sSLf -o /tmp/qlcplus-build/QLC+_${QLCPLUS_VERSION}.tar.gz \
    "https://github.com/mcallegari/qlcplus/archive/refs/tags/QLC+_${QLCPLUS_VERSION}.tar.gz"
    
RUN \
    cd /tmp/qlcplus-build &&\
    tar -xf QLC+_${QLCPLUS_VERSION}.tar.gz &&\
    rm QLC+_${QLCPLUS_VERSION}.tar.gz

RUN qmake
RUN make
RUN su -c "make install"

# Copy root filesystem
COPY rootfs /


