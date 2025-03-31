# Node.js Helloworld API - Pipeline de Integración y Despliegue

Este proyecto es una API sencilla en Node.js que devuelve un mensaje de bienvenida. Además, incluye un pipeline en Jenkins que automatiza la instalación de dependencias, la ejecución de pruebas y el despliegue de la aplicación, culminando con un health check.

## Requerimientos

Antes de ejecutar este pipeline, asegúrate de cumplir con lo siguiente:

1. **Node.js y npm**: Instala Node.js (incluye npm) desde [nodejs.org](https://nodejs.org/).
2. **Jenkins**: Debes tener Jenkins instalado y configurado para trabajar con pipelines.
3. **Plugin de NodeJS para Jenkins**: Configura el toolchain de Node.js en Jenkins para usar el identificador `nodejs`.
4. **Git**: Para clonar el repositorio, asegúrate de tener Git instalado.

## Clonar el Repositorio

Ejecuta el siguiente comando en tu terminal para clonar el repositorio:

```bash
git clone https://github.com/yosoyfunes/nodejs-helloworld-api.git
```

## Instalación de Dependencias

Desde la raíz del proyecto, instala las dependencias necesarias:

```bash
npm install
```

## Ejecución de Pruebas y de la Aplicación

Para asegurar el correcto funcionamiento de la aplicación, ejecuta las pruebas unitarias:

```bash
npm test
```

Luego, inicia la aplicación:

```bash
npm start
```

Realiza una verificación rápida:

```bash
curl http://localhost:3000
```

## Pipeline de Integración Continua (Jenkins)

El proyecto incluye un Jenkinsfile que define el siguiente flujo:

- **Instalación de Dependencias**: Ejecuta `npm install`.
- **Ejecución de Pruebas**: Utiliza `npm test` para correr las pruebas unitarias.
- **Inicio de la Aplicación**: Arranca la API en segundo plano usando `npm start&`.
- **Health Check**: Verifica que la aplicación responda correctamente mediante un `curl` al puerto 3000.

### Configuración del Pipeline

1. **Crear un Job en Jenkins**:
   - Crea un nuevo pipeline en Jenkins.
   - Configura el Pipeline para que apunte al repositorio:  
     `https://github.com/yosoyfunes/nodejs-helloworld-api.git`
   - Selecciona la rama `main` o la que prefieras.
   - Asegúrate de que el entorno tenga configurado el toolchain de Node.js correspondiente al label `nodejs`.

2. **Ejecutar el Pipeline**:
   - Inicia una nueva ejecución para verificar que cada etapa se ejecute correctamente.
   - Revisa la salida en cada etapa para confirmar que la API se instala, prueba, inicia y responde adecuadamente.

## Ejemplos de Ejecución en el Pipeline

### Ejecución Exitosa

1. **Salida en la etapa de dependencias**:
    ```plaintext
    > npm install
    ```
2. **Salida en la etapa de pruebas**:
    ```plaintext
    > npm test
    ```
3. **Salida en la etapa de despliegue**:
    ```plaintext
    > npm start&
    ```
4. **Health Check**:
    ```plaintext
    > curl http://localhost:3000
    Bienvenido a Node.js Helloworld API!
    ```

## Notas Adicionales

- Asegúrate de que el puerto 3000 no esté siendo utilizado por otra aplicación antes de iniciar la API.
- Si quieres personalizar alguno de los pasos del pipeline, modifica el Jenkinsfile según tus necesidades.
- La aplicación está diseñada para funcionamiento simple; para entornos productivos, considera agregar manejo de errores, logging y procesos de gestión de aplicaciones.

¡Disfruta experimentando y mejorando esta API!