
# Tutorial - Reporte de Actividades de Usuarios en DSpace

Este parche implementa un reporte estadístico que permite al administrador visualizar un resumen general de las métricas del repositorio, incluyendo la cantidad total de usuarios, envíos, revisiones, aprobaciones, rechazos y retiros.

----------

## 1. Aplicando el Parche en el Backend

Descarga el archivo `users-report-8c.diff` (ubicado en la carpeta `scripts/`) al directorio raíz de tu instalación de DSpace (código fuente del backend). Abre una terminal en la raíz del proyecto y ejecuta el siguiente comando:



```
git apply --reject --whitespace=fix users-report-8c.diff

```

## 2. Realizando el Build

Después de aplicar el parche con éxito, ejecuta el comando de Maven para compilar el proyecto:



```
mvn clean package

```

Una vez que finalice la compilación, navega hasta la carpeta del instalador generado y ejecuta la actualización a través de Ant:



```
cd dspace/target/dspace-installer
ant update

```

Finalmente, **reinicia tu servidor** (por ejemplo, Tomcat).

----------


## 3. Aplicando el Parche en el Frontend (DSpace Angular)

Ahora, descarga el archivo correspondiente al frontend en el directorio raíz de tu instalación de DSpace Angular. Abre una terminal en la raíz del proyecto Angular y ejecuta el siguiente comando:



```
git apply --reject --whitespace=fix users-report-front-8c.diff

```

Una vez aplicado el parche, instala las nuevas dependencias ejecutando:



```
npm install

```

En caso de que la instalación anterior falle o presente problemas, instala específicamente la librería de gráficos ejecutando:



```
npm install apexcharts

```

----------

## ⚠️ Observaciones Importantes para el Frontend

-   **Incompatibilidad de Imports (DSpace 8 y 9):** En versiones anteriores a DSpace 10 (como la 8 y la 9), el alias `@dspace` en los imports no es compatible. Después de aplicar el parche, será necesario abrir los archivos afectados y corregir las rutas de los imports manualmente.
    
-   **Conflictos en Archivos de Traducción (i18n):** Es probable que los archivos de traducción generen errores o rechazos durante la aplicación del parche. Si el `git apply` falla en estos archivos y termina creando un archivo de traducción nuevo o un archivo `.rej`, necesitarás corregirlo manualmente. Simplemente abre el archivo generado por el parche, copia las nuevas claves de traducción y pégalas directamente en tus archivos de traducción originales (como `en.json5` o `es.json5`).