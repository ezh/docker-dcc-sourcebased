FROM buildpack-deps:jessie-curl

COPY *SUMS /opt
COPY entrypoint.sh /

ARG version=1.3.158
ARG dcc_config="--disable-dccm --homedir=/dcc/conf --bindir=/dcc/bin --libexecdir=/dcc/bin"
ENV DEBIAN_FRONTEND=noninteractive
RUN set -x && \
    apt-get update -y && apt-get -y install apt-utils && \
    apt-get install --no-install-recommends --no-install-suggests -y wget \
        gcc ca-certificates libc-dev make && apt-get clean && \
    rm -rf /tmp/* /var/lib/apt/lists/* /var/tmp/* /download/directory && \
    cd /opt && wget -O dcc.tar.Z https://www.dcc-servers.net/dcc/source/old/dcc-${version}.tar.Z && \
    sha256sum -c dcc-${version}.tar.Z_SHA256SUMS && \
    tar xzvf dcc.tar.Z && cd dcc-${version} && \
    ./configure ${dcc_config} && \
    make install && \
    rm -rf /opt/dcc* && cd / && \
    mv /dcc/conf/cgi-bin/ /dcc && \
    mv /dcc/conf/log/ /dcc && \
    apt-get purge -y curl gcc ca-certificates libc-dev make && \
    rm -rf /var/lib/apt/lists/*

VOLUME ["/dcc/cgi-bin", "/dcc/log", "/dcc/conf"]

ENTRYPOINT ["/entrypoint.sh"]

# -tCMN,25,50
CMD [ \
  "/dcc/bin/dccifd", \
  "-tREP,20", \
  "-tCMN,NEVER,MANY", \
  "-l/dcc/log", \
  "-w/dcc/conf/whiteclnt", \
  "-U/dcc/conf", \
  "-SHELO", \
  "-Smail_host", \
  "-SSender", \
  "-SList-ID", \
  "-b", \
  "-p *,10030,127.0.0.0/8" \
]
