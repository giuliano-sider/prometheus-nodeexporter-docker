FROM gcr.io/google-appengine/debian9
ENV NODEEXPORTER_VERSION 1.0.0

ENV C2D_RELEASE=${NODEEXPORTER_VERSION}

ENV NODEEXPORTER_URL="https://github.com/prometheus/node_exporter/releases/download/v$NODEEXPORTER_VERSION/node_exporter-$NODEEXPORTER_VERSION.linux-amd64.tar.gz"
ENV NODEEXPORTER_SHA256 fae88be0aa33c8ae22340723f9b4a4e519e67d2969da7a27751e755db7e75788

RUN set -x && \
    apt-get update && apt-get install -qq -y wget && \
    mkdir nodeexporter-files && cd nodeexporter-files && \
    wget -O nodeexporter.tar.gz "$NODEEXPORTER_URL" && \
    echo "$NODEEXPORTER_SHA256 nodeexporter.tar.gz" | sha256sum -c - && \
    tar xfvz nodeexporter.tar.gz --strip-components=1 && \
    mv node_exporter /bin/ && \
    mkdir -p /usr/share/doc/nodeexporter && \
    mv LICENSE /usr/share/doc/nodeexporter && \
    cd - && rm -r nodeexporter-files

EXPOSE      9100
USER        nobody
ENTRYPOINT  [ "/bin/node_exporter" ]

