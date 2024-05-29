# onedrive-on-bunsenlabs

I Really need OneDrive in Linux, im switching, but in the meantime, this CHAT GPT conversation might be useful

---

**A.** Puedes darme instrucciones para instalar onedrive en bunsenlabs boron?


ChatGPT

**B.** Para instalar OneDrive en BunsenLabs Boron, puedes seguir estos pasos. BunsenLabs es una distribución basada en Debian, por lo que usaremos un cliente de OneDrive compatible con Debian llamado "onedrive". Este cliente es desarrollado por la comunidad y soporta la sincronización de archivos de OneDrive en Linux.

Paso 1: Instalar Dependencias

Primero, asegúrate de que tu sistema está actualizado e instala las dependencias necesarias.

Abre una terminal.

Actualiza los repositorios de paquetes:

    sh

    sudo apt update

Instala las dependencias necesarias:

    sh

    sudo apt install -y curl git build-essential libcurl4-openssl-dev libsqlite3-dev

Paso 2: Instalar DMD Compiler y libphobos2-ldc

El cliente onedrive está escrito en el lenguaje D, por lo que necesitas el compilador D.

Descarga e instala DMD (D language compiler):

    sh

    sudo apt install -y ldc

Paso 3: Clonar y Compilar el Cliente OneDrive
Clona el repositorio del cliente de OneDrive:

    sh

    git clone https://github.com/abraunegg/onedrive.git

Cambia al directorio del proyecto:

    sh

    cd onedrive

Compila el proyecto:

    sh

    ./configure
    make
    sudo make install

Paso 4: Configuración Inicial de OneDrive
Ejecuta el cliente por primera vez para configurarlo:

    sh

    onedrive

Esto abrirá un enlace en tu navegador donde tendrás que iniciar sesión en tu cuenta de Microsoft y dar permisos al cliente de OneDrive. Después de eso, recibirás un código que deberás ingresar en la terminal.

Paso 5: Ejecutar OneDrive como un Servicio

Para que OneDrive se ejecute automáticamente al iniciar el sistema, configura un servicio systemd:
Crea un archivo de servicio systemd:

    sh

    sudo nano /etc/systemd/system/onedrive.service

Copia y pega el siguiente contenido en el archivo:

    ini

    [Unit]
    Description=OneDrive Free Client
    Documentation=https://github.com/abraunegg/onedrive
    After=network-online.target

    [Service]
    ExecStart=/usr/local/bin/onedrive --monitor
    Restart=on-failure
    User=your-username
    Group=your-group
    Environment="DISPLAY=:0"
    Environment="XAUTHORITY=/home/your-username/.Xauthority"

    [Install]
    WantedBy=multi-user.target

Reemplaza your-username y your-group con tu nombre de usuario y grupo actual.

Guarda y cierra el archivo (Ctrl+O, Enter, Ctrl+X).

Recarga los archivos de configuración del sistema:

    sh

    sudo systemctl daemon-reload

Habilita y inicia el servicio de OneDrive:

    sh

    sudo systemctl enable onedrive
    sudo systemctl start onedrive

Paso 6: Verificar el Estado del Servicio

Puedes verificar si el servicio está corriendo correctamente con:

    sh

    systemctl status onedrive

Configuración Adicional

El cliente de OneDrive tiene varias opciones de configuración que puedes ajustar según tus necesidades. El archivo de configuración se encuentra en ~/.config/onedrive/config.

Para más información y opciones avanzadas, puedes consultar la documentación oficial del cliente de OneDrive.

Con estos pasos, deberías tener OneDrive funcionando en tu sistema BunsenLabs Boron.

**A.** Tengo este problema con el ./configure

    hugo@bunsenlabs:~/onedrive$ ./configure
    checking for a BSD-compatible install... /usr/bin/install -c
    checking for pkg-config... no
    checking for dmd... no
    checking for ldmd2... ldmd2
    checking version of D compiler... 1.30.0
    checking for curl... no
    configure: error: in `/home/hugo/onedrive':
    configure: error: The pkg-config script could not be found or is too old.  Make sure it
    is in your PATH or set the PKG_CONFIG environment variable to the full
    path to pkg-config.

    Alternatively, you may set the environment variables curl_CFLAGS
    and curl_LIBS to avoid the need to call pkg-config.
    See the pkg-config man page for more details.

    To get pkg-config, see <http://pkg-config.freedesktop.org/>.
    See `config.log' for more details


ChatGPT

**B.** El error que estás viendo indica que falta pkg-config en tu sistema, y también que curl no está instalado. Vamos a instalar estas herramientas y sus dependencias necesarias.
Paso 1: Instalar pkg-config y curl

Primero, instala pkg-config y curl:

    sh

    sudo apt update
    sudo apt install -y pkg-config libcurl4-openssl-dev curl

Paso 2: Reinstalar las dependencias básicas

Asegúrate de tener instaladas las dependencias básicas mencionadas anteriormente:

    sh

    sudo apt install -y curl git build-essential libcurl4-openssl-dev libsqlite3-dev

Paso 3: Verificar la Instalación de ldmd2

El error indica que se ha encontrado ldmd2 pero no dmd. Si ldmd2 está instalado y configurado correctamente, debería funcionar.
Paso 4: Volver a Clonar el Repositorio (opcional)

Si prefieres empezar de nuevo para asegurar un entorno limpio, elimina el directorio del proyecto y clónalo de nuevo:

    sh

    cd ..
    rm -rf onedrive
    git clone https://github.com/abraunegg/onedrive.git
    cd onedrive

Paso 5: Ejecutar ./configure Nuevamente

Ahora intenta ejecutar el script de configuración nuevamente:

    sh

    ./configure

Si todo está bien, el script de configuración debería ejecutarse sin errores.
Paso 6: Compilar y Instalar

Si ./configure se ejecuta correctamente, continúa con los siguientes comandos:

    sh

    make
    sudo make install

Verificación Final

Después de la instalación, verifica que el cliente de OneDrive está correctamente instalado ejecutando:

    sh

    onedrive --version

Esto debería mostrar la versión del cliente de OneDrive, indicando que la instalación fue exitosa.

Si aún encuentras problemas, por favor proporciona los nuevos mensajes de error que recibas para que pueda ayudarte a resolverlos.