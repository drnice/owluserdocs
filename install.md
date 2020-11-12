# Install

### Default Install

1. Download Release Version
2. Untar zip file
3. Run setup.sh

```bash
wget <https://download_link>
tar -xvf <package.tar>
./setup.sh -port=9000 -owlbase=<install_path> -options=owlagent,owlweb,spark,postgres,zeppelin
```

set license

```bash
./owlmanage.sh setlic=<lic>
```

### Pre Reqs

Requires Java 8

### Docker Install

Reach out to OwlDQ team for docker file.  DockerHub coming soon.

### Configuration Options

| option | value |
| :--- | :--- |
| owlbase | install path |
|  |  |

```bash
EXPORT owlbase = 
EXPORT     
```

## Upgrade



