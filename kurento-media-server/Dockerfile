FROM kurento/kurento-media-server:6.8.0-xenial

RUN apt-get update \
  && apt-get install -y software-properties-common \
  && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 5AFA7A83 \
  && add-apt-repository "deb http://ubuntu.openvidu.io/dev xenial kms6" \
  && cd /tmp \
  && apt-get update \
  && deps=" \
          build-essential \
          cmake \
          software-properties-common \
          autotools-dev \
          cdbs \
          dh-autoreconf \
          libglib2.0-dev \
          gtk-doc-tools \
          libgnutls-dev \
          kms-elements-dev \
          openwebrtc-gst-plugins-dev \
          libssl-dev \
      " \
  && apt-get install -y --no-install-recommends --no-install-suggests \
          $deps curl \
  # Install custom libnice
  && wget -O libnice.tar.gz https://github.com/alexlapa/libnice/archive/master.tar.gz \
  && tar -xvzf libnice.tar.gz \
  && cd libnice-master \
  && ./autogen.sh \
  && ./configure --libdir=/usr/lib/x86_64-linux-gnu/ \
  && make -j8 \
  && make install \
  && cd /tmp \
  # Install custom kms recorder endpoint
  && wget -O kms-elements.tar.gz https://github.com/alexlapa/kms-elements/archive/master.tar.gz \
  && tar -xvzf kms-elements.tar.gz \
  && cd kms-elements-master \
  && mkdir build \
  && cd build \
  && cmake .. \
  && make -j8 \
  && mv -f src/gst-plugins/recorderendpoint/librecorderendpoint.so /usr/lib/x86_64-linux-gnu/gstreamer-1.5/librecorderendpoint.so \
  # Cleanup unnecessary stuff
  && apt-get clean \
  && apt-get purge -y --auto-remove \
                    -o APT::AutoRemove::RecommendsImportant=false \
              $deps \
  && rm -rf /var/lib/apt/lists/* \
             /tmp/*