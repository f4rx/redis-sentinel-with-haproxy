FROM haproxy:2.0.1

RUN apt update && apt install -y python-pip procps && pip install haproxytool
RUN mkdir /var/lib/haproxy/

COPY haproxy.cfg .

CMD [ "haproxy", "-f", "/haproxy.cfg" ]
