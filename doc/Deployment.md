# Einfaches Deployment

## Was habe ich getan?

### Public SSH-Key wurde in GitHub zum Profil hinzugefügt
Das habe ich wohl gemacht weil sich ansonsten das Repository
nicht clonen lies.

### Repository clonen um es lokal bearbeitenzu können

```
$ git clone git@github.com:vieten/viwiz.git
```

### Dieses Dokument wurde angelegt ;-)

### Capistrano initialisieren

```
$ cap install
```

### Zeige alle verfügbaren Aufgaben.

```
$ cap -T
```

### Privaten Schlüssel zum authenifizierungs Agent hinzufügen

Der Checkout auf dem Live-Server funktionierte nicht.

```
00:01 git:check
      01 git ls-remote git@github.com:vieten/viwiz.git HEAD
      01 Permission denied (publickey).
      01 fatal: Could not read from remote repository.
      01
      01 Please make sure you have the correct access rights
      01 and the repository exists.
```

Die Lösung war den privaten Schlüssel zum Auth-Agenten hinzuzufügen:

```
$ ssh-add ~/.ssh/id_rsa
```

### Hurra es läuft

```
$ cap production deploy
```

```
00:00 git:wrapper
      01 mkdir -p /tmp
    ✔ 01 vieten@viwiz.de 0.486s
      Uploading /tmp/git-ssh-viwiz-production-norbert.sh 100.0%
      02 chmod 700 /tmp/git-ssh-viwiz-production-norbert.sh
    ✔ 02 vieten@viwiz.de 0.116s
00:00 git:check
      01 git ls-remote git@github.com:vieten/viwiz.git HEAD
      01 b92a1ed29ad78e7ce7424292fe4fe99d93f58771	HEAD
    ✔ 01 vieten@viwiz.de 1.708s
00:02 deploy:check:directories
      01 mkdir -p /var/www/capistrano/viwiz/shared /var/www/capistrano/viwiz/releases
    ✔ 01 vieten@viwiz.de 0.153s
00:03 git:clone
      01 git clone --mirror git@github.com:vieten/viwiz.git /var/www/capistrano/viwiz/repo
      01 Cloning into bare repository '/var/www/capistrano/viwiz/repo'...
    ✔ 01 vieten@viwiz.de 2.496s
00:05 git:update
      01 git remote set-url origin git@github.com:vieten/viwiz.git
    ✔ 01 vieten@viwiz.de 0.205s
      02 git remote update --prune
      02 Fetching origin
    ✔ 02 vieten@viwiz.de 1.638s
00:08 git:create_release
      01 mkdir -p /var/www/capistrano/viwiz/releases/20190127212612
    ✔ 01 vieten@viwiz.de 0.110s
      02 git archive master | /usr/bin/env tar -x -f - -C /var/www/capistrano/viwiz/releases/20190127212612
    ✔ 02 vieten@viwiz.de 0.199s
00:09 deploy:set_current_revision
      01 echo "b92a1ed29ad78e7ce7424292fe4fe99d93f58771" > REVISION
    ✔ 01 vieten@viwiz.de 0.304s
00:09 deploy:symlink:release
      01 ln -s /var/www/capistrano/viwiz/releases/20190127212612 /var/www/capistrano/viwiz/releases/current
    ✔ 01 vieten@viwiz.de 0.162s
      02 mv /var/www/capistrano/viwiz/releases/current /var/www/capistrano/viwiz
    ✔ 02 vieten@viwiz.de 0.127s
00:10 deploy:log_revision
      01 echo "Branch master (at b92a1ed29ad78e7ce7424292fe4fe99d93f58771) deployed as release 20190127212612 by norbert" >> /var/www/capistrano/viwiz/revisions.log
    ✔ 01 vieten@viwiz.de 0.210s
```
