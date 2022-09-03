# muniv-m312-vagrant-docker

MongoDB University M312 lab virtual environment for M1 Apple silicon:

> vagrant/virtualbox > docker

## Requisites

- docker
- docker-compose
- .env: copy `.env.template` to `.env` and set your timezone

## Usage

### Start

`docker-compose up -d`<br>
And check `docker logs --tail 3 m312` shows the following result

```
+ apt-get clean all
+ echo DONE
DONE
```

### Shutdown

`docker-compose down`

### Suspend

`docker-compose pause`

### Resume

`docker-compose unpause`

### Storage

`/home/vagrant` is set for general lab environments but subfolders need to be created according to mongod cfg file per each lab scenario.

Lab 2.1 for example, `/home/vagrant/data` should exist to run `mongod -f single.cfg`

### mtools/mgenerate

Use JS version `mgeneratejs` that is included in this setup.

> Python `mgenerat` is not supported any longer.

`mgeneratejs` does not insert docs for itself.

`mongoimport` can be used to actually load generated docs onto DB.

e.g.

```
mgeneratejs /shared/schema.json -n 100 | mongoimport --drop -c=mgencol -d=m312 -h=localhost:30000
```
