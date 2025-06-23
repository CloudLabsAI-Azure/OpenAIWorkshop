# Ejercicio 2: Crear una aplicación de OpenAI con Power App

### Duración estimada: 90 minutos

Este laboratorio se centra en la creación de una aplicación utilizando las funcionalidades de OpenAI integradas con Microsoft Power Apps. Los participantes aprenderán a crear una aplicación funcional que aprovecha la IA para tareas como la comprensión del lenguaje natural, el análisis de datos o la interacción con el cliente dentro del marco de Power Apps.

1. Navegue a https://make.powerapps.com/. En **Bienvenido a Power Apps**, seleccione su **País/Región (1)** y haga clic en **Comenzar (2)**. 

   ![](./images/welcome-1.png)
    
2. Seleccione **Aplicaciones (1)** en la navegación izquierda, haga clic en el menú desplegable **Importar aplicación (2)** y seleccione **Desde paquete (.zip) (3)**. 

    ![](./images/powerapps-import-01.png)

3. En la página **Importar paquete**, haga clic en **Cargar**

    ![](./images/upload-importpackage.png)

4. Navegue a `C:\labfile\OpenAIWorkshop-main\OpenAIWorkshop-main\scenarios\powerapp_and_python\powerapp`. Seleccione la carpeta **OpenAI-Playground_20230302010547.zip (1)** y haga clic en **Abrir (2)**.

     ![](./images/openai-play.png)

5. Una vez cargado el archivo zip, en **Revisar Contenido del Paquete** para **OpenAI Playground**, haga clic en el icono de configuración debajo de **Acción**.

     ![](./images/review-package-content.png)

6. En el panel **Importar configuración**, seleccione **Crear como nueva (1)** del menú desplegable de **Configuración** y haga clic en **Guardar (2)**.

      ![](./images/import-setup-1.png)

7. Repita los Pasos 5 y 6 para **Openaisummarization**.

8. A continuación, haga clic en **Importar** para importar el paquete al entorno de PowerApps.

   ![](./images/import-openai-package.png)

9. Una vez que se complete la importación, haga clic en **Aplicaciones (1)**, luego haga clic en `...` **(2)** junto a **OpenAI Playground** y haga clic en **Editar (3)**.

      ![](./images/powerapps-apps-edit.png)

   >**Nota**: Si no puede ver la opción **OpenAI Playground**, por favor espere 5 minutos y, mientras tanto, intente actualizar la página.

10. Observará que ha importado la aplicación de lienzo Power App y el Power Automate Flow al espacio de trabajo.

      ![](./images/powerapps-apps-view.png)

11. Para navegar hacia atrás, haga clic en **Atrás (1)**, luego haga clic en **Salir (2)**.

      ![](./images/powerapps-apps-exit.png)

12. A continuación, en la pestaña **Flujos (1)**, seleccione **Openaisummarization (2)**, luego haga clic en `...` **(3)** y **Activar (4)** su flujo.

      ![](./images/flow-on.png)

13. Haga clic en **Editar** para Openaisummarization.

      ![](./images/flow-edit.png)

14. Edite el paso HTTP de Power Automate Flow actualizando **https://your-resource-name.openai.azure.com/** con **<inject key="OpenAIEndpoint" enableCopy="true"/>** **(1)**, **deployment-id** con **<inject key="openaimodulename" enableCopy="true"/>** **(2)**, **api-version** con **2023-09-15-preview** **(3)**, **YOUR_API_KEY** con **<inject key="OpenAIKey" enableCopy="true"/>** **(4)**, y haga clic en **Guardar** **(5)**. 

      ![](./images/update-values.png)
   
15. Desde la página **Aplicaciones (1)**, haga clic en la aplicación **OpenAI Playground** para ejecutarla haciendo clic en el botón **Play (2)**.

     ![](./images/canves-play.png)

16. Si aparece una ventana emergente que te pide que inicies una prueba gratuita, haz clic en **Iniciar una prueba gratuita** y, a continuación, en la ventana **Necesitas una licencia de Power Apps para usar esta aplicación**, selecciona **Iniciar una prueba de 30 días**. Selecciona tu región en el menú desplegable y haz clic en el botón **Iniciar mi prueba**. Espera de 2 a 3 minutos. La prueba puede tardar en iniciarse.
    
17. En el **Lienzo**, haga clic en el botón **Summary** **(1)** y verifique el **texto inicial** **(2)**. Luego haga clic en el botón **Submit** **(3)** para obtener el **Resumen** **(4)** deseado.

     ![](./images/canves-output.png)

    > **Nota**: Puede probar las otras opciones disponibles en el portal, es decir, **SQL**, **ClassifyText**, **Parse**, y **Classify**.

## Resumen

En este laboratorio, ha integrado correctamente las API de OpenAI en Power Apps para habilitar funcionalidades como el procesamiento del lenguaje natural, el análisis de sentimientos o las recomendaciones personalizadas, y ha creado una aplicación.

### Ha completado el laboratorio correctamente. Haga clic en **Siguiente >>** para continuar con el siguiente ejercicio.