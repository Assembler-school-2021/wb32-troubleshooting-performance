# wb32-troubleshooting-performance

Para instalar:
`bash <(curl -Ss https://my-netdata.io/kickstart.sh)`

Conf de bdd para wordpress:
```
mysql
	create database wordpress;
	grant all privileges on wordpress.* to 'wp_user'@'localhost' identified by 'vahKei4ovah0ieLasohaceiTahxeelae';
	flush privileges;
```
User de wp: enrique/WZ7Q%C$dNP56ib6(dy

> Pregunta 1 : Mira como añadir una sección específica de los logs del wordpress. Se configura en el archivo /usr/lib/netdata/conf.d/go.d/web_log.conf . Si lo has hecho todo bien verás algo así:

![image](https://user-images.githubusercontent.com/65896169/131901427-82febf76-fdd8-4dff-8949-54f39da24c5e.png)


> Pregunta 2 : el script tiene un error. Arréglalo.

El argumento de la función get debe ser $1
```
#!/bin/bash

max="$1"
date
echo "url: $2
rate: $max calls / second"
START=$(date +%s);

get () {
  curl -s -v "$1" 2>&1 | grep "HTTP/1.1" 
}

while true
do
  echo $(($(date +%s) - START)) | awk '{print int($1/60)":"int($1%60)}'
  sleep 1

  for i in `seq 1 $max`
  do
    get $2 &
  done
Done
```

> Mira atentamente en netdata todo atentamente, cpu, ram, load, nginx, mysql ...

> Pregunta 3 : logueate en el wordpress y copia la petición como curl. Cuando lo tengas haz una copia del script de stress y adáptalo para estressar esta petición de login. Observa bien el netdata y todo lo que ocurre.

> Pregunta 4 : realiza lo mismo que en el ejercicio anterior pero con la página principal de backend, el enlace dashboard.

