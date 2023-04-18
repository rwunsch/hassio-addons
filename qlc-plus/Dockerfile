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
		qt5-qtwebchannel \
		qt5-qtwebengine \
		qt5-qtsvg \
		qt5-qtconnectivity \
		qt5-qtcharts \
		qt5-qtvirtualkeyboard \
		qt5-qtlocation \
		qt5-qttools \
		qt5-qtquickcontrols2 \
		qt5-qtwayland \
		qt5-qtxmlpatterns \
		qt5-qtx11extras \
		qt5-qtserialport \
		qt5-qtsensors-dev \
		qt5-qtmultimedia-dev \
		qt5-qtspeechv \
		qt5-qtremoteobjects \
		qt5-qtscript \
		qt5-qtimageformats \
		qt5-qttranslations \
		qt5-qtgraphicaleffects \
		glib-dev \
		libpulse

# missing dependencies: qtchooser libqt5multimedia5-plugins
RUN \
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


