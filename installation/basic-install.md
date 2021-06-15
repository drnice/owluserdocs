# Basic Install

If you're an existing customer, please see the [upgrade](https://docs.owl-analytics.com/install#upgrade) section.

### Linux Install

1. Download Release Version
2. Untar zip file
3. Run setup.sh

Pre-req - Must have Java 8 installed on the machine

```bash
wget <https://download_link>
tar -xvf <package.tar>
./setup.sh -port=9000 -owlbase=<install_path> -options=owlagent,owlweb,postgres
```

Set license

```bash
./<install_path>/bin/owlmanage.sh setlic=<lic>
```

Install requires Java 8.  Common install path as /opt/owl/.  Default port 9000, must not be in-use by another system.  Make sure you can chmod and own the install dir.  License key comes from OwlDQ. 

## Setup Options

```bash
usage () {
    echo "Usage: $0 [OPTION]..."
    echo "Owl installation script"
    echo ""
    echo "  -non-interactive  skip asking to accept JAVA license agreement"
    echo "  -skipSpark        skips the extraction of spark components"
    echo "  -skipPostgres     skips the asking for the setup of postgres details"
    echo "  -stop             do not automatically start up all components (orient,owl-web)"
    echo "  -port=            set owlweb applicationt to use defined port"
    echo "  -user=            set the postgres user"
    echo "  -owlbase=         set base path to where you want owl installed"
    echo "  -owlpackage=      set owl package directory"
    echo "  -help             display this help and exit"
    echo "  -options=         the different owl components to install (comma separated list)"
    echo "                    example: owlagent,owlweb,zeppelin,orient,spark,postgres"
    echo "  -pgpassword=      password for the postgres metastore "
    echo "  -pgserver=        name of the postgres server example = owl-postgres-host.example.com:5432/owldb"
    echo ""
    echo ""
    echo "example:"
    echo "  ./setup.sh -port=9000 -user=ec2-user -owlbase=/home/ec2-user -owlpackage=/home/ec2-user/packages"
}
```

   

### Docker Install

Reach out to OwlDQ team for docker file.  DockerHub coming soon.

### Configuration Options

| option | value | default value |
| :--- | :--- | :--- |
| owlbase | install path | /opt/owl/ |
| port | web app port | 9000 |

```bash
EXPORT owlbase = /opt/owl/
EXPORT port = 9000    
```

## Upgrade

1. Download Release Version
2. Untar Zip file
3.  Move Owl-\*.jar files into install directory
4. Restart webapp

```bash
wget <https://download_link>
tar -xvf <package.tar>
mv owl-*.jar / <install_path>/bin
/<install_path>/bin/owlmanage.sh start=owlweb
```

## 

