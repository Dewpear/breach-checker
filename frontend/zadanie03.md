docker inspect --format '{{json .Config.Labels}}' marek_giernacki:v1
{"autor":"Marek Giernacki","data":"2026-11-06","maintainer":"imie.nazwisko@example.com"}


docker history marek_giernacki:v1
IMAGE          CREATED              CREATED BY                                      SIZE      COMMENT
f2b5ce21d102   About a minute ago   EXPOSE [80/tcp]                                 0B        buildkit.dockerfile.v0
<missing>      About a minute ago   RUN /bin/sh -c htmlhint /usr/share/nginx/htm…   4.1kB     buildkit.dockerfile.v0
<missing>      About a minute ago   COPY . /usr/share/nginx/html # buildkit         32.8kB    buildkit.dockerfile.v0
<missing>      12 minutes ago       RUN /bin/sh -c apk add --no-cache nodejs npm…   99.3MB    buildkit.dockerfile.v0
<missing>      12 minutes ago       LABEL autor=Marek Giernacki data=2026-11-06     0B        buildkit.dockerfile.v0
<missing>      12 minutes ago       LABEL maintainer=imie.nazwisko@example.com      0B        buildkit.dockerfile.v0
<missing>      18 hours ago         RUN /bin/sh -c set -x     && apkArch="$(cat …   52.4MB    buildkit.dockerfile.v0
<missing>      18 hours ago         ENV ACME_VERSION=0.4.1                          0B        buildkit.dockerfile.v0
<missing>      18 hours ago         ENV NJS_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      18 hours ago         ENV NJS_VERSION=1.0.2                           0B        buildkit.dockerfile.v0
<missing>      19 hours ago         CMD ["nginx" "-g" "daemon off;"]                0B        buildkit.dockerfile.v0
<missing>      19 hours ago         STOPSIGNAL SIGQUIT                              0B        buildkit.dockerfile.v0
<missing>      19 hours ago         EXPOSE map[80/tcp:{}]                           0B        buildkit.dockerfile.v0
<missing>      19 hours ago         ENTRYPOINT ["/docker-entrypoint.sh"]            0B        buildkit.dockerfile.v0
<missing>      19 hours ago         COPY 30-tune-worker-processes.sh /docker-ent…   16.4kB    buildkit.dockerfile.v0
<missing>      19 hours ago         COPY 20-envsubst-on-templates.sh /docker-ent…   12.3kB    buildkit.dockerfile.v0
<missing>      19 hours ago         COPY 15-local-resolvers.envsh /docker-entryp…   12.3kB    buildkit.dockerfile.v0
<missing>      19 hours ago         COPY 10-listen-on-ipv6-by-default.sh /docker…   12.3kB    buildkit.dockerfile.v0
<missing>      19 hours ago         COPY docker-entrypoint.sh / # buildkit          8.19kB    buildkit.dockerfile.v0
<missing>      19 hours ago         RUN /bin/sh -c set -x     && addgroup -g 101…   5.75MB    buildkit.dockerfile.v0
<missing>      19 hours ago         ENV DYNPKG_RELEASE=1                            0B        buildkit.dockerfile.v0
<missing>      19 hours ago         ENV PKG_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      19 hours ago         ENV NGINX_VERSION=1.31.8                        0B        buildkit.dockerfile.v0
<missing>      19 hours ago         LABEL maintainer=NGINX Docker Maintainers <d…   0B        buildkit.dockerfile.v0
<missing>      20 hours ago         CMD ["/bin/sh"]                                 0B        buildkit.dockerfile.v0
<missing>      20 hours ago         ADD alpine-minirootfs-3.24.4-x86_64.tar.gz /…   9.09MB    buildkit.dockerfile.v0


z obrazu bazowego pochodza dolne wiersze z mojego dockerfile 6 pierwszych z gory niektore maja 0B bo dodaja tylko metadane, a nie jakies pliki fizyczne


zawartosc: build.txt
Fri Nov  6 13:41:28 UTC 2026


PS C:\Marek_lab3\brach-checker> docker ps
CONTAINER ID   IMAGE                COMMAND                  CREATED              STATUS              PORTS                                     NAMES
de0891e79c2a   marek_giernacki:v2   "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:8082->80/tcp, [::]:8082->80/tcp   front2
ce7be351d6bc   marek_giernacki:v2   "/docker-entrypoint.…"   2 minutes ago        Up 2 minutes        0.0.0.0:8081->80/tcp, [::]:8081->80/tcp   front1


czas jest taki sam poniewaz zostaje on zapisany podczas tworzenia obrazu a nie kontenera


 root   /usr/share/nginx/html;

 tutaj serwer szuka plikow




 PS C:\Marek_lab3\brach-checker> docker exec front-bad ls /usr/share/nginx/html
50x.html
build.txt
index.html
PS C:\Marek_lab3\brach-checker> docker exec front-bad ls /usr/share/nginx
html
index.html
script.js
style.css
zadanie03.md


htmlhint sprawdzil index.html znajdujacy sie w /usr/share/nginx/html  Jest tam w pelni poprawny plik html zawierajacy podstawowa strone nginx


PS C:\Marek_lab3\brach-checker> docker rmi breach-checker-frontend:latest
Untagged: breach-checker-frontend:latest
PS C:\Marek_lab3\brach-checker> docker images
                                                                                                                                                   i Info →   U  In Use
IMAGE                        ID             DISK USAGE   CONTENT SIZE   EXTRA
breach-checker-frontend:v1   83b6380e8e6f       93.7MB         26.4MB
breach-checker-frontend:v2   e81ccfe3bf56       93.7MB         26.4MB
breach-checker-frontend:v3   e23bcec6e098        225MB         58.2MB
marek_giernacki:bad          1756d16783e9        225MB         58.2MB    U
marek_giernacki:latest       f2b5ce21d102        225MB         58.2MB
marek_giernacki:v1           f2b5ce21d102        225MB         58.2MB
marek_giernacki:v2           5a52845a9f1a        225MB         58.2MB    U
nginx:alpine                 b2f80f8f8814       94.5MB         27.3MB
redis:alpine                 71885d8cc6e4        162MB           40MB
PS C:\Marek_lab3\brach-checker> docker rmi breach-checker-frontend:2
Error response from daemon: No such image: breach-checker-frontend:2
PS C:\Marek_lab3\brach-checker> docker rmi breach-checker-frontend:v2
Untagged: breach-checker-frontend:v2
Deleted: sha256:e81ccfe3bf56071d0045e150d76c49cdd326978bfbc92758744ff3d1f10aa8b5