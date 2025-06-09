# Exercise 3: Build an Open AI application with Python

### Estimated Duration: 60 minutes

In this lab, participants will develop an application using OpenAI's APIs and Python programming language. The goal is to demonstrate how to implement AI functionalities such as language generation, sentiment analysis, or recommendation systems using Python, leveraging OpenAI's powerful models and tools.

1. Search and select **Azure Synapse Analytics** in the Azure portal.

      ![](images/azure_synapse-1.png)

1. On **Azure Synapse Analytics** window select **asaworkspace<inject key="DeploymentID" enableCopy="false"/>**.   

1. On the **Overview** blade under the **Getting started** section, click **Open** to open Synapse Studio.
     
     ![](images/open-workspace.png)
    
1. Click on **Develop (1)**, then click on **+ (2)**, and select **Import**.

    ![](images/import-note.png)

1. Navigate to the `C:\labfile\OpenAIWorkshop\scenarios\powerapp_and_python\python` location and select `OpenAI_notebook.ipynb`, then click on **Open**.

     ![](images/notebook.png)

1. Select **openaisparkpool** from the drop-down menu of **Attach to**.

    ![](images/openai-sparkpool.png)

1. Click on the **▷ Run** button next to each cell, step-by-step, in the order mentioned below.

     ![](images/run.png)

<!--

1. In **1. Install OpenAI**, click on the **Run** button next to the first cell, and click on the **stop session**. Please wait till **Apache Spark pools** turn to the stop state. 

     ![](images/run-python1.png)

      > **Note**: You may need to restart the kernel to use updated packages
-->

1. Under **1. Install OpenAI**, click on the **Run** button next to the first cell. 

     ![](images/Ex4-RunOpenAI.png)

1. Under **2. Import helper libraries and instantiate credentials**, replace **AZURE_OPENAI_API_KEY** and **AZURE_OPENAI_ENDPOINT** with your API key and endpoint URL. Then, run this cell after updating the required values.

     ![](images/key-endpoint.png)
   
1. From Azure Portal, navigate to the **openaicustom-<inject key="DeploymentID" enableCopy="false"/>** resource group, and select the **asaworkspace<inject key="DeploymentID" enableCopy="false"/>** Azure OpenAI resource.

    ![](images/Ex4b-S7.1.png)

1. Under Resource Management, select **Keys and Endpoint (1)**, and click **Show Keys (2)**. Copy **Key 1 (3)** and **Endpoint (4)**, and replace the **AZURE_OPENAI_API_KEY** and **AZURE_OPENAI_ENDPOINT** with your API key and Endpoint URL in the script.

   ![](images/p22.png)
     
    > **Note:** If you encounter an error "Openai module not found", enter `%` in before the **pip install** in the Install OpenAI cell and re-run the notebook again.

1. For **2. Choose a Model**, replace the **model** value from **text-curie-001** to **demomodel** and **run** this cell.

    ![](images/choosemodel.png)

1. For the cell under **temperature**, replace the **engine** value from **text-curie-001** to **demomodel**, and run this cell.

     ![](images/temp.png)

1. For the cell under **top_p**, replace the **engine** value from **text-curie-001** to **demomodel**, and run this cell.

     ![](images/top-p.png)

1. For the cell under **n**, replace the **engine** value from **text-curie-001** to **demomodel**, and run this cell.

     ![](images/n.png)

1. For the cell under **logprobs**, replace the **engine** value from **text-curie-001** to **demomodel**, and run this cell.

     ![](images/logprobs.png)

1. After running the Notebook cells successfully, click on **Publish all**.

     ![](images/publish.png)

1. Then click on **Publish** to save the changes. 

    ![](images/publish-1.png)

<validation step="25c1c315-a610-4974-ae83-c5b3983d798e" />

## Summary

In this lab, you have successfully developed an application by implementing AI functionalities such as language generation, sentiment analysis, or recommendation systems using Python, leveraging OpenAI's powerful models and tools.

### You have successfully completed the lab
