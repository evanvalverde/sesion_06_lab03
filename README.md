# sesion_06_lab03
Laboratorio 3, sesión 6 del curso Ansible/AWX: Templates

## Enunciado 

Crearemos un repositorio Github con el nombre sesion_06_lab03. En él añadiremos el inventario y el ansible.cfg que creamos oportuno. 
Crearemos un playbook.yml con las siguientes tareas:
	*Nota: Es una complementación del sesion_06_lab01 por lo que antes deberemos de hacer y dejar funcionando el 	anterior lab
	*Nota: Debemos de revisar las IP de los archivos de configuración y hacerlas coincidir con las nuestras.
- Lanzamos el playbook denominado playbook_04_template de la sesion_06 sobre el nodo_02
- Añadiremos las siguientes lineas al fichero /etc/named.conf

```named.conf
zone "dominio.local" IN {
    type master;
    file "named.dominio.local";
};
```

- Tras eso crearemos un template del archivo /var/named/named.dominio.local:

```named.dominio.local
$TTL    1D
@       IN      SOA     ns.dominio.local. root.dominio.local. (
                            1       ; serial
                            604800  ; refresh
                            86400   ; retry
                            2419200 ; expiration
                            604800  ; TTL negative cache
    );
; Servidores de nombres
                        IN      NS      ns.dominio.local.
; Registros
ns.dominio.local.       IN      A       IP_nodo_01
```

- El template anterior debe ser dinámico y en la inserción de este se tienen que añadir las siguientes lineas al final del 	todo usando variables y bucles. Donde pone nodo_02 debe de tener la IP del nodo_02

web01.dominio.local.  IN      A       nodo_02:80
web02.dominio.local.  IN      A       nodo_02:81
web03.dominio.local.  IN      A       nodo_02:8080
```
- Recargaremos el servicio named con un handler forzado
- Comprobaremos el estado de la zona  y lo registraremos en una variable--> ~$ sudo named-checkzone dominio.local 	/var/named/named.dominio.local
- Tras eso comprobamos si resuelve los nombres y lo registraremos
- Crearemos un archivo con el contenido de los registros anteriores para mostrar el resultado

## OPCIONAL

Crear y configurar la zona inversa como se indica en el siguiente documento

https://comoinstalar.me/como-instalar-el-servidor-dns-bind-en-centos-7/
