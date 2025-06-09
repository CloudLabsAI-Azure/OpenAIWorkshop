# Ejercicio 1: Crear una canalización de OpenAI para ingerir datos por lotes, realizar operaciones inteligentes y analizar en Synapse

### Duración estimada: 120 minutos

Este laboratorio tiene como objetivo demostrar cómo integrar las funcionalidades de OpenAI en Azure Synapse Analytics para procesar datos por lotes, realizar operaciones inteligentes como el procesamiento del lenguaje natural o el análisis predictivo, y analizar los resultados de forma eficiente en el entorno de Synapse.

## Objetivos del Laboratorio

Será capaz de completar las siguientes tareas:

- Tarea 1: Ingesta de Datos en la Cuenta de Almacenamiento
- Tarea 2: Configurar un área de trabajo de Synapse
- Tarea 3: Consultar Resultados en Nuestra Tabla SQL

## Tarea 1: Ingesta de Datos en la Cuenta de Almacenamiento

### A. Iniciar Azure Cloud Shell

1. En el [Portal de Azure](https://portal.azure.com?azure-portal=true), seleccione el botón **[>_]** (*Cloud Shell*) ubicado en la parte superior de la página a la derecha de la caja de de búsqueda. Se abrirá un panel de Cloud Shell en la parte inferior del portal. 

     ![](images/cli-1.png)

2. La primera vez que abra Cloud Shell, es posible que se le solicite que elija el tipo de Shell que desea usar (*Bash* o *PowerShell*). Seleccione **Bash**. Si no ve esta opción, omita el paso.

3. En el panel Introducción, seleccione **Montar cuenta de almacenamiento (1)**, seleccione su **suscripción de Cuenta de Almacenamiento (2)** del menú desplegable y haga clic en **Aplicar (3)**. 

   ![](images/10-06-2024-01.png)

4. En el panel **Montar cuenta de almacenamiento**, elija **Seleccionar cuenta de almacenamiento existente (1)** y haga clic en **Siguiente (2)**.

   ![](images/10-06-2024(2).png)

5. Dentro del panel **Configuración Avanzada**, ingrese los siguientes detalles:

    - **Suscripción**: Predeterminada- Elija la única suscripción existente asignada para esta práctica de laboratorio (1).
    - **Grupo de Recursos**: Elija **Usar existente** **(2)**
      - openai-<inject key="DeploymentID" enableCopy="false"></inject>
    - **Cuenta de Almacenamiento**: Elija **Usar existente** **(3)**
      - openaistorage<inject key="DeploymentID" enableCopy="false"></inject>
    - **Recurso compartido de archivos**: crear un recurso compartido de archivos **(4)**

      ![](images/10-06-2024(3).png)

1. Establezca el nombre del recurso compartido de archivos como **blob (1)**, y haga clic en **Seleccionar (2)**.

    ![](images/10-06-2024(4).png)

1.  Una vez creada la cuenta de almacenamiento, aparecerá la ventana Bash, tal como se muestra en la siguiente captura de pantalla:
    
    ![](images/cloudshell.png)

    > **Nota**: ignore la advertencia «El ID de suscripción del recurso compartido de archivos de almacenamiento no está registrado en el espacio de nombres Microsoft.CloudShell» y continúe con la siguiente tarea.

### B. Cargar archivos a una cuenta de almacenamiento:

1. Ejecute los siguientes comandos en Cloud Shell para descargar e instalar Miniconda.

     ```bash 
     wget https://repo.anaconda.com/miniconda/Miniconda3-py39_23.1.0-1-Linux-x86_64.sh 
     ```

     ```bash 
     sh Miniconda3-py39_23.1.0-1-Linux-x86_64.sh 
     ```
    
    > **Nota:** Los siguientes comandos funcionan en Bash; asegúrese de utilizar **Bash** en Cloud Shell. 
    
    > **Nota:** Presione la tecla de flecha hacia abajo para leer u omitir el acuerdo de licencia.

1. Pulse **Enter** para continuar con la instalación.

   > **Nota:** Pulse la flecha hacia abajo para leer u omitir el acuerdo de licencia.

   ![](images/pro1-1.png)

1. Escriba **yes** y presione **Enter** para aceptar el acuerdo, y luego presione **Enter** para instalar en la ruta predeterminada. 

   ![](images/cloudshell-accept.png)

1. Escriba **yes** y presione **enter** para inicializar el entorno de conda.

    ![](images/E2T1PBS3.png)

1. Ejecute el siguiente comando para almacenar la ruta de instalación de miniconda en la variable.

    ```bash 
    export PATH=~/miniconda3/bin:$PATH
    ```
1. Ejecuta los siguientes comandos uno por uno para crear y activar el entorno conda en CloudShell.

    ```bash 
    git clone https://github.com/CloudLabsAI-Azure/openaifilesworkshop.git
    ```

    ```bash
    cd openaifilesworkshop/scenarios/openai_batch_pipeline/document_generation
    ```

    ```bash
    conda create -n document-creation
    ```

    ```bash
    conda activate document-creation
    ```

    > **Nota:** Si encuentras el error **"Conda: command not found"** después de ejecutar este comando, cierra tu sesión actual de CloudShell, inicia una nueva sesión de Bash y vuelve a intentar ejecutar los comandos de este **Paso 6**.

    ```bash
    pip install --upgrade pip
    pip install -r reqs.txt
    ```

    > **Nota:** Si encuentras errores al ejecutar los comandos pip anteriores, ejecuta los siguientes comandos:
    >
    >     pip install --user --upgrade pip
    >     pip install --user -r reqs.txt
    
1. Presione la tecla **y** y luego presione Enter para continuar.
    > **Nota:** Continúa con el siguiente paso si no se te solicita esto.

1. En el [Portal de Azure](https://portal.azure.com), navegue hasta su recurso de Cuenta de almacenamiento con el sufijo `functions` seleccionando el grupo de recursos **openai-<inject key="DeploymentID" enableCopy="false"/>** y seleccionando la Cuenta de Almacenamiento de la lista de recursos.

    ![](images/storage-functions.png)
    
1. Cambie a la hoja **Claves de acceso (1)** y seleccione **Mostrar (2)**, el cual está al lado del valor de Cadena de conexión. Seleccione el botón copiar para la primera **cadena de conexión (3)**. Pegue el valor en un editor de texto, como Notepad.exe, a fin de poderlo consultar más adelante. 

   ![](images/E1T1.BS9.png)

1. Vuelva a la sesión de bash de Cloud Shell y ejecute el siguiente comando para cargar los archivos JSON en la cuenta de almacenamiento reemplazando <CONNECTION_STRING> por el valor que copió en el paso anterior. Esto tardará unos minutos en completarse.

    ```bash 
    python upload_docs.py --conn_string "<CONNECTION_STRING>"
    ```

   ![](images/batch_file_upload2.png)

   > **Note**: Ejecute "cd OpenAIWorkshop scenarios/openai_batch_pipeline/document_generation" si no está dentro del directorio OpenAIWorkshop/scenarios/openai_batch_pipeline/document_generation.
   
1. Una vez que haya cargado exitosamente los archivos JSON a la cuenta de almacenamiento, navegue a **Contenedores (1)**, haga clic en **workshop-data (2)**, seleccione la carpeta **cleansed_documents (3)** y verifique que los archivos se hayan cargado.

   ![](images/batch_file_upload-1.png)


   ![](images/pro4-1.png)


> **¡Felicitaciones!** por completar la tarea. Ahora es momento de validarla. Estos son los pasos:
> - Si recibe un mensaje de éxito, puede continuar con la siguiente tarea.
> - De lo contrario, lea atentamente el mensaje de error y vuelva a intentar el paso siguiendo las instrucciones de la guía del laboratorio.
> - Si necesita ayuda, contáctenos en cloudlabs-support@spektrasystems.com. Estamos disponibles 24/7 para ayudarle.

<validation step="ef9a8088-8af2-426f-9672-70c0b0c227b5" />

## Tarea 2: Configurar un área de trabajo de Synapse

### **A. Configurar un área de trabajo de Synapse**

1. En Azure Portal, busque **Synapse** y seleccione **Azure Synapse Analytics**.

   ![](images/image(1).png)

2. En la página **Azure Synapse Analytics**, haga clic en **+ Crear**.
3. Se le dirigirá a la página **Crear Synapse Analytics** donde configurará el espacio de trabajo de Synapse.
4. En la pestaña Conceptos básicos, proporcione los siguientes detalles:

   - **Suscripción**: utilice **Suscripción existente(1)**.
   - **Grupo de recursos**: utilice **openai-<inject key="DeploymentID" enableCopy="false"></inject>(2)**
   - **Nombre del espacio de trabajo**: **synapseworkspace<inject key="DeploymentID" enableCopy="false"></inject>(3)**
   - **Región**: seleccione la región predeterminada (4)
   - **Seleccione Data Lake Storage Gen2**: seleccione **De la suscripción(5)**
   - **Nombre de cuenta**: **asadatalake<inject key="DeploymentID" enableCopy="false"></inject>(6)**
   - **Nombre del sistema de archivos**: **defaultfs(7)**
   - Haga clic en **Siguiente: Seguridad>(8)**

     ![](images/image(03).png)

5. En la pestaña **Seguridad**, asegúrese de que el método de autenticación esté configurado en **Usar autenticación local y de ID de Microsoft Entra** y haga clic en **Siguiente: Networkikng**

   ![](images/image(3).png)

6. En la pestaña de redes, asegúrese de que Red virtual administrada esté **Desactivada(1)** y **Permitir conexiones desde todas las direcciones IP(2)** esté marcada y luego haga clic en **Revisar + Crear** y **Crear*. * para implementar el recurso.

   ![](images/image(4).png)

   > **Nota:** La implementación puede tardar aproximadamente 5 minutos en completarse.


7. Una vez implementado el recurso, haga clic en **Ir al grupo de recursos**

8. Navegue al espacio de trabajo de Synapse que ha creado, en la página **Información general (1)**, haga clic en **Abrir (2)** en Abrir Synapse Studio para navegar a Azure Synapse Studio.

   ![](images/open-synapse-studio.png)

9. En Azure Synapse Studio, navegue a **Manage (1) > SQL pools (2)** y luego haga clic en **+ Nuevo (3)**.

    ![](images/new-sql-pool.png)


10. En la pestaña Conceptos básicos de Nuevo grupo de SQL dedicado, proporcione los siguientes detalles:

    - **Nombre del grupo de SQL dedicado**: **openaisql01**
    - **Nivel de rendimiento**: Reducirlo a **DW100c**
    - Haga clic en **Siguiente: Configuraciones adicionales**

      ![](images/sql-pool-name.png)

      > **Nota:** La implementación puede tardar aproximadamente 10 minutos en completarse.

11. En la página **Revisar + crear**, haga clic en **Crear** y espere a que se complete la implementación.

12. Ahora regrese al espacio de trabajo de synapse<inject key="DeploymentID" enableCopy="false"></inject>, seleccione **Grupos de Apache Spark** en el panel izquierdo debajo de Grupos de análisis y haga clic en **+ Nuevo**.

    ![](images/image(07).png)

13. En la página Nuevo grupo de Apache Spark, proporcione los siguientes detalles y haga clic en **Revisar + Crear** y luego en **Crear** en la pestaña Revisar + Crear para crear el grupo de Apache Spark.

    - **Nombre del grupo de Apache Spark**: **openaisparkpool**
    - **Cómputo aislado**: **Deshabilitado**
    - **Tamaño de nodo**: **Pequeño (4vCores/32GB)**
    - **Escala automática**: **Deshabilitado**
    - **Número de nodos** : **3**
      
      ![](images/image(08).png)

### **B. Crear la Tabla SQL de Destino** 

1. En el [Portal de Azure](https://portal.azure.com), navegue hasta el área de trabajo de Synapse **synapseworkspace<inject key="DeploymentID" enableCopy="false"/>** del grupo de recursos **openai-<inject key="DeploymentID" enableCopy="false"/>**. En la pestaña **Información general (1)**, haga clic en **Abrir (2)** para iniciar el espacio de trabajo de Synapse.

      ![](images/open-synapse-studio.png)

1. Haga clic en la sección **Desarrollar (1)** de Synapse Studio, haga clic en el signo **+ (2)** en la parte superior izquierda y seleccione **Script SQL (3)**. Esto abrirá una nueva ventana con un editor de script SQL. 

      ![](images/synapse3.png)

1. Copie y pegue el siguiente script en el editor **(1)**, luego cambie el valor **Conectar a** seleccionando **openaisql01(2)** del menú desplegable, y en **Usar base de datos**, asegúrese de que **openaisql01(3)** esté seleccionado, y haga clic en el botón **Ejecutar (4)** en la esquina superior izquierda, tal como se muestra en la siguiente imagen. Termine este paso presionando **Publicar todo (5)** justo encima del botón **Ejecutar** para publicar nuestro trabajo hasta el momento.

    ```SQL 
    CREATE TABLE [dbo].[cs_detail]
    (
    interaction_summary varchar(8000),
    sentiment varchar(500),
    topic varchar(500),
    product varchar(500),
    filename varchar(500)
    )
    ```
    
      ![](images/openai-6-1.png)
    
1. A continuación, haga clic en **Publicar** para publicar el script SQL.

      ![](images/publish-sqlscript.png)

### **C. Crear Servicios Vinculados de Origen y Destino**

A continuación, necesitaremos crear dos servicios vinculados: uno para nuestra fuente (los archivos JSON en el Data Lake) y otro para la base de datos SQL Synapse que alberga la tabla que creamos en el paso anterior.

1. Vuelva a hacer clic en la sección **Administrar (1)** en Synapse Studio y haga clic en la opción **Servicios vinculados (2)** debajo de la sección **Conexiones externas**. Luego haga clic en **+ Nuevo (3)** en la esquina superior izquierda.

      ![](images/synapse5.png)
   
1. Comience creando los servicios vinculados para la fuente de nuestros datos, los archivos JSON alojados en el almacenamiento ADLS Gen2 que creamos con nuestra plantilla inicial. En la barra de búsqueda que se abre después de hacer clic en Nuevo, busque **blob (1)**, seleccione **Azure Blob Storage (2)** como se muestra a continuación y haga clic en **Continuar (3)**.

      ![](images/synapse6.png)

1. Indique el nombre de su servicio vinculado como **openailinkedservice (1)**. Cambie el **Tipo de autenticación** a **Clave de cuenta (2)**. A continuación, seleccione la **suscripción (3)** con la que trabaja y, por último, la cuenta de almacenamiento con el sufijo **functions (4)** que creó en la plantilla de inicio y a la que cargó los archivos JSON. A continuación, haga clic en **Probar conexión (5)**. Una vez que la conexión se haya realizado correctamente, haga clic en el botón azul **Crear (6)** en la esquina inferior izquierda de la ventana Nuevo servicio vinculado.

      ![](images/img-6.png)

1. Haga clic en **+ Nuevo** en la esquina superior izquierda. Busque **Synapse (1)**, seleccione **Azure Synapse Analytics (2)** y haga clic en **Continuar (3)**.

      ![](images/synapse8.png)

1. En la ventana *Nuevo servicio vinculado* que se abre, ingrese **synapselinkedservice** **(1)** para el nombre de su servicio vinculado de destino. Seleccione la **suscripción de Azure (2)** con la cual ha estado trabajando. Seleccione **synapseworkspace<inject key="DeploymentID" enableCopy="false"/> (3)** para el **Nombre del servidor** y utilice **openaisql01 (4)** para el **Nombre de la base de datos**. Asegúrese de cambiar el **Tipo de autenticación** a **Identidad Administrada Asignada por el Sistema (5)**, luego desplácese hacia abajo y seleccione la opción **Heredado (6)**, luego haga clic en **Probar conexión (7)** y haga clic en **Crear (8)**. 

    ![](images/new-openai-pro-feb-5-1.png)

1. Una vez que haya creado los dos servicios vinculados, asegúrese de presionar el botón **Publicar todo** en la parte superior para publicar nuestro trabajo. Finalice la creación de los servicios vinculados y haga clic en **Publicar**.

      ![](images/publish-linked.png)
   
### **D. Crear Flujo de Datos en Synapse**

Mientras todavía estamos dentro de Synapse Studio, ahora necesitaremos crear un **flujo de datos** para ingerir nuestros datos JSON y escribirlos en nuestra base de datos SQL. Para este taller, será un flujo de datos muy simple que ingiere los datos, cambia el nombre de algunas columnas y vuelve a escribir la información en la tabla de destino.

1. Primero, queremos volver a la pestaña **Desarrollar (1)**, seleccionar **+ (2)** y luego **Flujo de datos (3)**.

      ![](images/synapse11.png)
   
1. Una vez que se abra el editor de flujo de datos, haga clic en **Agregar origen**. Se abrirá una nueva ventana en la parte inferior de la pantalla. Seleccione **+ Nuevo** en la fila **Conjunto de datos** y deje las otras opciones con los valores predeterminadps.

      ![](images/synapse12.png)

1. Debería abrirse una nueva ventana en el lado derecho de la pantalla. A continuación, busque **blob (1)**, seleccione **Azure Blob Storage (2)** y luego haga clic en **Continuar (3)**.
   
      ![](images/synapse13-1.png)

1. A continuación, seleccione la opción **JSON (1)** ya que nuestros datos entrantes están en formato JSON y haga clic en **Continuar (2)**.

      ![](images/synapse14-1.png)

1. Seleccione el Servicio Vinculado con el nombre **openailinkedservice (1)** que acabamos de configurar en los pasos anteriores. Deberá seleccionar la **Ruta del archivo** adecuada para seleccionar el directorio donde se almacenan nuestros archivos JSON. Debería ser algo parecido a **workshop-data / cleansed_documents (2)**. Haga clic en el botón **Aceptar** para cerrar la ventana.

      ![](images/synapse15.png)
   
1. A continuación, tendremos que ir al panel **Opciones de origen (1)** y desplegar las opciones de **Configuración JSON (2)**. Necesitamos cambiar la opción **Formulario de documento** a la configuración **Array of documents (3)**. Esto permite que nuestro flujo lea cada archivo .JSON como una entrada separada en nuestra base de datos.

      ![](images/synapse16.png)   

1. Habilite la opción sesión de **depuración de flujo de datos** ubicada en la barra de menú superior adyacente al botón de validación y haga clic en **OK** en la ventana emergente *Activar depuración de flujo de datos*.

      >**Nota:** La sesión de **depuración de flujo de datos** tardará uno o dos minutos en habilitarse.

1. Ahora diríjase a la pestaña **Vista previa de datos** y ejecute una previsualización para comprobar su trabajo hasta el momento.
    
      ![](images/dataflow-datapreview.png)

      >**Nota**: Si no puede ver los datos en la pestaña Vista Previa de Datos, por favor haga clic en el botón Actualizar repetidamente hasta que aparezcan los datos.
   
1. A continuación, podemos agregar en nuestro cuadro **Seleccionar** y realizar modificaciones menores antes de escribir los datos en la tabla SQL de Synapse. Para comenzar, haga clic en el pequeño signo **+ (1)** junto a nuestro cuadro de ingesta y elija la opción **Seleccionar (2)**.

      ![](images/synapse17.png)

1. Podemos dejar todas las configuraciones con los valores por defecto. A continuación, agregaremos nuestro cuadro **Receptor**. Este es el paso que escribirá nuestros datos en nuestra base de datos SQL de Synapse. Haga clic en el pequeño signo **+ (1)** junto al cuadro **Seleccionar**. Desplácese hasta el final del menú de opciones y seleccione la opción **Receptor (2)**.

      ![](images/synapse18.png)

1. Una vez que se abra el cuadro **Receptor (1)**, elija **En línea (2)** para el *Tipo de Receptor*. Luego, seleccione **Azure Synapse Analytics (3)** para el *Tipo de conjunto de datos en línea* y, para el **Servicio vinculado**, seleccione **Synapselinkedservice (4)**, el cual fue creado en el paso anterior. Asegúrese de ejecutar **Probar conexión (5)** para el servicio vinculado.

      ![](images/sink-1.png)

      > **Nota**: Si la conexión de prueba tarda más de 3 a 4 minutos, siga los pasos a continuación.

      - Haga clic en **Editar**.

           ![](images/p18.png)    

           - En la ventana Editar servicio vinculado que se abre, seleccione el método de selección de Azure como **Desde la suscripción de Azure** **(1)**. Seleccione la **suscripción de Azure (2)** con la cual ha estado trabajando. Seleccione **asaworkspace<inject key="DeploymentID" enableCopy="false"/> (3)** para el **Nombre de servidor** y **openaisql (4)** como el **Nombre de la base de datos**, luego haga clic en **Probar conexión (5)** y finalice haciendo clic en **Guardar (6)**.

                ![](images/p19.png)

1. Luego tendremos que dirigirnos a la pestaña **Configuración (1)** y ajustar el **Nombre del esquema** y el **Nombre de la tabla**. Si utilizó el script proporcionado anteriormente para crear la tabla de destino, el nombre del esquema es **dbo (1)** y el nombre de la tabla es **cs_detail (2)**.

      ![](images/synapse20.png)

1. Antes de terminar nuestro trabajo en el flujo de datos, debemos obtener una vista previa de nuestros datos. La vista previa de nuestros datos revela que solo tenemos 3 columnas cuando esperamos un total de 5. Hemos perdido nuestras columnas Summary y Sentiment.

      ![](images/data-preview.png)

1. Para corregir esto, usemos nuestro cuadro **Seleccionar (1)** para cambiar los nombres de la siguiente manera para obtener los valores de salida esperados:

     - **Summary**: `interaction_summary` **(2)**
     - **CustomerSentiment**: `sentiment` **(3)**

          ![](images/select-1.png)
    
1. Si volvemos a nuestro cuadro **Receptor (1)** y en **Vista previa de datos (2)** hacemos clic en **Actualizar (3)**, ahora veremos las 5 columnas de salida esperadas.

      ![](images/refresh-sink-1.png)

1. Una vez que haya revisado los datos y esté satisfecho de que todas las columnas se hayan asignado correctamente (debería tener 5 columnas en total, todas mostrando datos en formato de cadena), podemos presionar **Publicar todo** en la parte superior para guardar nuestra configuración actual. Se abrirá una ventana en el lado derecho de la pantalla; presione el botón azul **Publicar** en la parte inferior izquierda para guardar los cambios.

      ![](images/publish-dataflow.png)

1. Su Flujo de Datos completo y guardado tendrá el siguiente aspecto:

      ![](images/completed-dataflow.png)

### **E. Crear Pipeline de Synapse**

1. Una vez que hayamos creado nuestro **Flujo de datos**, necesitaremos configurar un **Pipeline** para alojarlo. Para crear un **Pipeline**, navegue hasta la barra de menú de la izquierda y elija la opción **Integrar (1)**. Luego haga clic en **+ (2)** en la parte superior del menú Integrar para **Agregar un nuevo recurso** y elija **Canalización (3)**.

      ![](images/new-pipeline-1.png)

2. A continuación, debemos agregar un **Flujo de datos** a nuestro Pipeline. Con su nueva **pestaña Pipeline (1)** abierta, vaya a la sección **Actividades** y busque `datos` **(2)**, seleccione la actividad **Flujo de datos (3)** y **arrástrela (4)** hacia su Pipeline.

      ![](images/data-drag-1.png)

3. En la pestaña **Configuración (1)** del **Flujo de datos**, seleccione el menú desplegable **Flujo de datos (2)** y elija el nombre del flujo de datos que creó en el paso anterior.
Luego expanda la sección **Ensayo (3)** en la parte inferior de la configuración y utilice el menú desplegable para el **Servicio vinculado de Staging**. Elija el servicio vinculado **openailinkedservice (4)** que creó. Garantice la conexión realizando una **Prueba de conexión (5)**. A continuación, configure una **carpeta de almacenamiento de prueba** en la parte inferior e ingrese **workshop-data/Staging** **(6)**.

      ![](images/staging-1.png)

4. Luego, haga clic en **Publicar todo** para publicar sus cambios y guardar su progreso.

### **F. Activar el Pipeline de Synapse**

1. Una vez que haya publicado con éxito su trabajo, debemos activar nuestro canal. Para hacer esto, justo debajo de las pestañas en la parte superior de Synapse Studio, hay un ícono de *rayo* que dice **Agregar desencadenador (1)**. Haga clic en él para agregar un activador y seleccione **Desencadenar ahora (2)** para comenzar una ejecución del pipeline; luego, cuando se abra la ventana, haga clic en **OK**.

      ![](images/trigger-1.png)
    
2. Para ver la ejecución del pipeline, navegue hasta el lado izquierdo de la pantalla y elija la opción **Monitorear (1)**. Luego seleccione la opción **Pipeline runs (2)** en la sección **Integration**. Verá la ejecución del pipeline que desencadenó en la sección **Desencadenado (3)** como **pipeline 1 (4)**. Este pipeline debería tomar aproximadamente 4 minutos (si está utilizando los datos cargados para el taller).

      ![](images/pipeline-run-1.png)

      <validation step="3e716f01-6da8-431e-aa81-4041b9054091" />

## Tarea 3: Consultar Resultados en Nuestra Tabla SQL

1. Asegúrese de que el estado de ejecución de su pipeline sea **Exitoso**.

      ![](images/pipline-succeeded.png)

2. Ahora que los datos están en la tabla de destino, están disponibles para su uso ejecutando consultas SQL en ellos o conectando PowerBI y creando visualizaciones. Cargue algunos de los archivos de transcripción en la carpeta generate_documents en su contenedor y vea cómo crea un nuevo archivo en el archivo cleansed_documents.

3. Para consultar los nuevos datos, navegue hasta el menú del lado izquierdo y elija **Desarrollar (1)**. Haga clic en el **Script SQL (2)** existente y reemplace el contenido con el **Código SQL (3)** mostrado a continuación. Luego seleccione el grupo **openaisql (4)** y haga clic en **Ejecutar (5)**.

     ```SQL 
    SELECT sentiment, count(*) as "Sum of Sentiment"
    FROM [dbo].[cs_detail]
    GROUP BY sentiment
    ORDER BY count(*) desc     
     ```

   - Para los resultados de su consulta, si está utilizando los archivos cargados como parte de este repositorio o taller, debería ver **Resultados (6)** similares a los siguientes.

        ![](images/lastpic.png)

## Resumen

En esta práctica de laboratorio, incorporó datos a la cuenta de almacenamiento, configuró Synapse Workspace y generó resultados de consulta en nuestra tabla SQL.

### Ha completado con éxito la práctica de laboratorio. Haga clic en **Siguiente >>** para continuar con el siguiente ejercicio.
