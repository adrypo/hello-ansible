
# Vagrant

Vagrant para levantar rapido maquinas virtuales

vagrant init -h

vagrant init debian/bookworm64
	
    se decomenta config vn network en el VagrantFile

vagrant up

vagrant ssh-config 
	
    fichero para conectarnos a ssh 
	
	
conectarnos a la maquina con 

vagrant ssh 

# REVISION DE CODIGO

yamllint 

    te comprueba que el fichero yml está bien formado

ansiblelint 

    te comprueba que el fichero está bien formado para ansible y no hay ningun error

flake 8 
    
    podemos revisar el codigo de python con flake8, siguiendo las normas pep 8 de buenas practicas de codigo de python

# ANSIBLE GALAXY

Colecciones oficiales

    https://galaxy.ansible.com/ui/

tenemos la carpeta galaxy_ng con los ficheros necesarios
url https://ansible.readthedocs.io/projects/galaxy-ng/en/latest/usage_guide/installation/

levantamos el galaxy con 

    3-compose up

Veremos si está levantado con 

    docker compose ps

vemos los logs con 

    docker compose logs -f

    si hacemos un curl http://localhost.8080 -v veremos que se accede

    si redirigimos la salida de un comando/json con jq podremos verlo bien

Los siguiente comandos están documentados en la url mencionada anteriormente


    Json de respuesta 
        curl -u admin:password -L http://localhost:8080/api/galaxy/pulp/api/v3/status/

        si usamos un | jq lo podremos ver de forma legible

        curl -u admin:password -L http://localhost:8080/api/galaxy/pulp/api/v3/status/ | jq

    Metricas del galaxy 

        curl -u admin:password -L http://localhost:8080/metrics

    Instalar dependencias 

        docker compose exec galaxy_ng pip install django-extensions

Guia de la web

    Collections
        Repositories

    Remotes --- Repositorios remotos, como el de community y modificar que modulos queremos, en edit template (en el comunity) y podemos meter esto

    De esta manera del de community nos descargaremos solo los que queramos
        # Sample requirements.yaml

        collections:
        - name: amazon.aws
        - name: ansible.posix

    Despues de esto podremos ir a Repositorioes - Comunity - Sync para descargarlo

Configuramos un ansible.cfg con la siguiente informacion, podremos encadenarlos por orden y tener los que queramos.


    [galaxy]
    server_list = community,release_galaxy

    [galaxy_server.community]
    url=http://localhost:8080/api/galaxy/content/community/
    token=<put your token here>

    [galaxy_server.release_galaxy]
    url=https://galaxy.ansible.com/

Y despues ejecutamos el siguiente comando:

    ansible-galaxy collection install amazon.aws -vvv


# Collections
Agrupacion de roles y modulos para que la gestion de dichos elementos sea mas facil



La sigueinte estructura es la convencion de ansible

    mkdir collections
    mkdir collections/ansible_collections
    ansible-galaxy collection init NOMBRE (habitualmente es el nombre del usuario)
    ansible-galaxy collection init abanca.ops

Al crearlo veremos el siguiente arbol

    tree
    .
    └── abanca
        └── ops
            ├── docs
            ├── galaxy.yml
            ├── meta
            │   └── runtime.yml
            ├── plugins
            │   └── README.md
            ├── README.md
            └── roles

En el playbook se puede crear un campo collections con las colecciones que se usan, para evitar poner el nombre completo. No es muy recomendable, ya que acabas perdiendo un poco el modulo que estas usando.


# OTROS

Eliminar espacios al final de una línea
    :%s/\s*$//g