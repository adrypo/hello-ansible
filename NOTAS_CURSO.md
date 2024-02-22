
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

tenemos la carpeta galaxy_ng con los ficheros necesarios
url https://ansible.readthedocs.io/projects/galaxy-ng/en/latest/usage_guide/installation/

levantamos el galaxy con 

    docker-compose up

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

# OTROS

Eliminar espacios al final de una línea
    :%s/\s*$//g

API TOKEN Galaxy

    d75439646ccc771765cc0ba9791d94f8140f7298