# iaw
Repositorio Implantación de Aplicaciones Web
--------------------------------------------
Práctica 2 · Radio Marea (UD4, UD5 y UD6).

El enunciado completo, con «Cómo se evalúa», está en la web de la asignatura,
en «🏋️ Practicar» (con la contraseña del curso): as1r20:26
https://jmfiorisies.github.io/iaw/practicas/p2-radio-marea/
Allí también se descarga el kit.
El trabajo se hace en tu repositorio de GitHub:
carpeta p2-radio-marea/ de tu repositorio IAW, en main, con un commit por apartado.
Avances: A lun 9/11 · B lun 16/11 · C lun 23/11. Defensa: lunes 30/11.
Qué entregas aquí: el enlace a tu repositorio de GitHub, antes del viernes 27/11 a las 23:59. Se corrige lo que tengas subido en GitHub en ese momento.

P2 . Radio Marea
----------------

Lanza las órdenes desde la carpeta de la práctica (p2-radio-marea/),
la misma de la que lanzas el mando.
Trabaja en la rama main. Compruébalo con git branch --show-current:
tiene que decir main. Si dice otra cosa, git switch main.Se corrige lo que hay en main.
El mensaje empieza por el número de la actividad y dice qué has hecho.
✅ A1: Nginx pasa los .php a PHP-FPM · ❌ cambios, update, practica.
Si la actividad se queda a medias, haz el commit igual y dilo: A2: a medias, falta probarlo.
Un commit por actividad, no uno enorme al final. Si haces más, mejor: guardar de más no quita nada.
Cómo saber si ha subido bien:
git status                # tiene que decir que no hay nada para confirmar
y que estás al día con origin/main
git log --oneline -3      # tus tres últimos commits

Al terminar cada actividad ✍️ guardas tu trabajo en Git.
Es obligatorio y siempre es igual: tres órdenes.
Al final de cada actividad las tienes ya escritas en un recuadro verde 💾,
listas para copiar y pegar en la terminal.
Para qué: el profesor sigue tu avance actividad a actividad en tu repositorio,
cuenta para la nota (el apartado «Git» de cada bloque) y, si algo se rompe,
puedes volver a la última versión que funcionaba.

---------------------------------------------
09-11: Empezando p2-radio-marea/ -> este es mi dir.principal en repo iaw(público)

A partir de aquí, un commit al acabar cada actividad: te los encontrarás en los recuadros 💾.

Las pruebas no se tocan

Se corrige con las copias originales del profesor: cambiar comprobador/ no sirve de nada.
💻 Trabajar en otro ordenador (y si empezaste con el kit antiguo)

📖 Lo que no está en Git no viaja. Cuando clonas tu repositorio en otro ordenador (en casa, en otra aula), solo te llega lo que subiste con git push. Hay dos ficheros que tu .gitignore deja fuera a propósito, porque son secretos:
Fichero 	Qué es 	Por qué no va a Git 	Qué pasa si falta
certs/lab.key 	La llave privada del certificado HTTPS 	Con la llave, cualquiera podría hacerse pasar por tu servidor 	Nginx no arranca
servidor/radio.env 	Las contraseñas y la SECRET_KEY 	Una contraseña en Git queda para siempre en el historial 	Ni la web ni la API pueden entrar en la base de datos

Así funciona también en una empresa: el código va al repositorio y los secretos se ponen a mano en cada servidor (o se crean nuevos allí). La base de datos tampoco viaja: vive en un volumen de Docker de cada ordenador.

El kit nuevo ya lo tiene en cuenta: si falta el certificado, ./practica.sh arrancar hace uno nuevo (es de prueba, sirve cualquiera para *.iaw.local), y si falta radio.env, se para y te dice qué hacer. El kit antiguo no lo hacía: Nginx no arrancaba y no se entendía por qué.

✍️ Si empezaste con el kit antiguo, hazlo una vez (en cualquier ordenador; luego ya viaja con Git):

    Descarga otra vez el kit desde esta página (la contraseña de siempre) y descomprímelo fuera de tu repositorio, por ejemplo en Descargas. No lo descomprimas encima: machacarías tu trabajo.
    Sustituye solo practica.sh de tu p2-radio-marea/ por el del kit nuevo. Nada más: tus ficheros de servidor/, web/, app/ y sql/ se quedan como están.

    Guárdalo en Git para tenerlo ya en todos tus ordenadores (desde p2-radio-marea/):

    git add practica.sh
    git commit -m "P2: practica.sh del kit nuevo (rehace el certificado)"
    git push

✍️ En cada ordenador nuevo (después de git clone o git pull):

    radio.env: si no está, copia servidor/radio.env del kit a tu servidor/ y rellena otra vez:
        SECRET_KEY: genera una nueva (UD5, apartado 7.3). No hace falta que sea la de antes: solo se cierran las sesiones abiertas.
        DB_USER y DB_PASS: los de tu sql/usuarios.sql.

    Arranca (el certificado se hace solo) y crea tus usuarios en la base de datos de este ordenador:

    ./practica.sh arrancar
    ./practica.sh sql
    ./practica.sh comprobar      # lo que tenías en verde, tiene que seguir en verde

✅ Cómo comprobarlo: git status --short no enseña ni radio.env ni lab.key (siguen fuera de Git), y ./practica.sh comprobar da el mismo resultado que en tu otro ordenador.

Que no se te ocurra «arreglarlo» subiendo los secretos

Quitar *.key o radio.env del .gitignore para no tener que rehacerlos es justo lo que trabajas en el bloque C: los secretos, fuera de Git. Rehacerlos en cada ordenador es lo correcto.

