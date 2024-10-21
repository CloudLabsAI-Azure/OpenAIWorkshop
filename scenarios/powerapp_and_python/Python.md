# Exercise 3: Build an Open AI application with Python

1. Pesquise e selecione **Azure Synapse Analytics** no portal do Azure.

      ![](images/p2-1.png)

1. Na janela **Azure Synapse Analytics** selecione **asaworkspace<inject key="DeploymentID" enableCopy="false"/>**.   

1. Na lâmina **Visão geral** na seção **Começando**, clique em **Abrir** para abrir o Synapse Studio.
     
     ![](images/open-workspace-1.png)
    
1. Clique em **Desenvolver (1)**, depois clique em **+ (2)** e selecione **Importar (3)**.

    ![](images/import-note-1.png)

1. Navegue até o local `C:\labfile\OpenAIWorkshop\scenarios\powerapp_and_python\python` e selecione `OpenAI_notebook.ipynb` e clique em **Abrir**.

1. Selecione **openaisparkpool** no menu suspenso de **Anexar a**.

    ![](images/openai-sparkpool.png)

1. Execute o notebook passo a passo para concluir este exercício. Clique no botão **Run** ao lado da célula.

     ![](images/run.png)

1. Em **1. Install OpenAI**, clique no botão **Executar** ao lado das primeiras células e clique em **parar sessão**. Aguarde até que os **pools Apache Spark** passem para o estado de parada. 

     ![](images/run-python1.png)

      > **Note**: Pode ser necessário reiniciar o kernel para usar os pacotes atualizados

1. Em **2. Import helper libraries and instantiate credentials** e substitua **AZURE_OPENAI_API_KEY** e **AZURE_OPENAI_ENDPOINT** pela sua chave de API e URL do endpoint.

     ![](images/key-endpoint.png)
   
1. No Portal do Azure, navegue até o grupo de recursos **openaicustom-<inject key="DeploymentID" enableCopy="false"/>** e selecione o recurso **openai-<inject key="DeploymentID" enableCopy="false"/>** do Azure OpenAI.

    ![](images/18-10-24(11).png)

1. Em Gerenciamento de Recursos, selecione **Chaves e Ponto de extremidade (1)** e clique em **Mostrar as Chaves (2)**. Copie **Chave 1 (3)** e **Ponto de extremidade (4)** e substitua **AZURE_OPENAI_API_KEY** e **AZURE_OPENAI_ENDPOINT** pela sua chave de API e URL do Endpoint no script.

   ![](images/18-10-24(12).png)
     
    > **Note:** Se você encontrar o erro "Módulo Openai não encontrado", digite `%` antes de **pip install** na célula Instalar OpenAI e execute o notebook novamente.

1. Para **2. Choose a Model** e substitua o valor do **model** de **text-curie-001** para **demomodel**.

    ![](images/choosemodel.png)

1. Em **temperature**, substitua o valor **motor** de **text-curie-001** para **demomodel**.

     ![](images/temp.png)

1. Em **top_p**, substitua o valor **engine** de **text-curie-001** para **demomodel**.

     ![](images/top-p.png)

1. Para **n**, substitua o valor **engine** de **text-curie-001** para **demomodel**.

     ![](images/n.png)

1. Em **logprobs**, substitua o valor **engine** de **text-curie-001** para **demomodel**.

     ![](images/logprobs.png)

1. Depois de executar o notebook com sucesso, clique em **Publicar tudo**.

     ![](images/publish.png)

1. Em seguida, clique em **Publicar** para salvar as alterações.

    ![](images/publish-1.png)

   <validation step="25c1c315-a610-4974-ae83-c5b3983d798e" />
