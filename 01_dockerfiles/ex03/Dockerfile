FROM debian

RUN apt update && apt install -y curl openssh-server ca-certificates apt-transport-https tzdata
RUN curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash
RUN apt install gitlab-ce
RUN mkdir -p /etc/gitlab/ssl && chmod 700 /etc/gitlab/ssl
RUN echo "external_url 'https://192.168.99.100'" > /etc/gitlab/gitlab.rb \
&& echo "nginx['redirect_http_to_https'] = true" >> /etc/gitlab/gitlab.rb \
&& echo "nginx['ssl_certificate'] = '/etc/gitlab/ssl/192.168.99.100.crt'" >> /etc/gitlab/gitlab.rb \
&& echo "nginx['ssl_certificate_key'] = '/etc/gitlab/ssl/192.168.99.100.key'" >> /etc/gitlab/gitlab.rb \
&& openssl req -new -x509 -days 365 -nodes -out /etc/gitlab/ssl/192.168.99.100.crt -keyout /etc/gitlab/ssl/192.168.99.100.key -subj "/C=AU/ST=Moscow/L=Some-city/O=Some-company/CN=Some-Unit"
EXPOSE 80 443 22
CMD service ssh restart && (/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl reconfigure && tail -f /dev/null
