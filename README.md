# Automated data pipeline on Azure Data Factory and Synapse Analytics

## Project Scope

- Store the raw data in local and upload manually into **Data Lake Storage Gen2** as csv files.

- Perform data pipeline with **Azure Data Factory(ADF)**  workspace and **Azure Synapse** workspace.
- Create Dataflow and Pipeline in ADF loading data from **Data Lake Storage Gen2** to **Azure SQL Database**.

- Create Dataflow and Pipeline in ADF loading data from **Azure SQL Database** to **Azure Synapse** tables.

- Create Dataflow and Pipeline in ADF loading data from **Data Lake Storage Gen2** to **Azure Synapse** tables.

- Create Dataflow and Pipeline that union current and historical data. The first one is from **Azure Synapse** tables and the second one is from **Data Lake Storage Gen2** file. Also applying some transformation and aggregation steps before loading the output into **Azure Synapse** tables.

### Getting Started
1. Create Azure Subcription and Resource Group on Azure.

2. Create several Azure resources:
    - **Azure Data Lake Gen2** for raw data
    - **Azure SQL Database**
    - **Azure Data Factory**
    - **Azure Synapse Analytics**
    - **Azure Data Lake Gen2** for Synapse

3. In Azure Data Lake Gen2 for raw data:
- Create three directories in this storage container named:
    - **dirpayrollfiles**: upload EmpMaster.csv, AgencyMaster.csv, TitleMaster.csv, nycpayroll_2021.csv
    - **dirhistoryfiles**: upload nycpayroll_2020.csv
    - **dirstaging**: use for staging folder when creating the pipeline.

    <img src="result_images\datalakegen2.png" class="img-responsive" alt=""> </div>

4. In Azure SQL Database:
- Create a database and table for Payroll data in 2021 using SQL Query Editor.
- Add client IP address to the SQL DB firewall.

    <img src="result_images\sqleditor.png" class="img-responsive" alt=""> </div>

5. In Azure Synapse Analytics:
- Create 4 tables corresponding 4 csv files in Data Lake Gen2.

    <img src="result_images\synapse-table.png" class="img-responsive" alt=""> </div>

6. In Azure Data Factory:
- Create three **Linked Services** in Azure Data Factory allowing the connection to Azure SQL Database, Azure Data Lake Gen2, and Azure Synapse.

    <img src="result_images\linkservices.png" class="img-responsive" alt=""> </div>

### Prerequisites for Azure Data Factory
- In order to deploy a pipeline in ADF, we have to create a bunch of components first:

    - **Datasets**: use as a view pointing to files or tables in other resources. Include Source dataset and Destination dataset. 

        <img src="result_images\dataset.png" class="img-responsive" alt=""> </div>

    - **Data Flow**: create a flow from Source to Sink including to apply some of transformations and aggregations.

        <img src="result_images\dataflow.png" class="img-responsive" alt=""> </div>

    - **Pipeline**: create the order running data flow and schedule the time to trigger the pipeline.

        <img src="result_images\pipeline.png" class="img-responsive" alt=""> </div>

### Project instruction

1. Create 9 Datasets in Azure Data Factory:
- 4 csv files in Data Lake Gen2 as Source Dataset.
- 1 table in SQL Database as Source Dataset.
- 4 tables in Synapse as Destination Dataset.

2. Create 5 Data Flows for loading:
- Loading data from 2021 Payroll Data file in Data Storage Gen2 to SQL database.
- Loading 2021 Payroll Data from SQL DB to Synapse table.
- Loading Employee, Title, and Agency files in Data Storage Gen2 into corresponding SQL pool tables on Synapse.

3. Create, Trigger and Monitor 6 Pipelines:
- Select staging folder to dirstaging container in Data Lake Gen2 when creating pipeline.
- Create 1 master pipeline invoking all the Data Flow.
- Create, trigger:

    <img src="result_images\create_trigger_pipeline.png" class="img-responsive" alt=""> </div>

- Monitor:
    <img src="result_images\monitor.png" class="img-responsive" alt=""> </div>

4. Aggregate Data Flow
- Create a Summary table in Synapse.
- Create a new dataset for the Azure Data Lake Gen2 folder that contains the historical files.
- Create new data flow union 2 datasets for 2021 data in Synapse table and 2020 data in Data Lake Gen2 file.

    <img src="result_images\aggregate_flow.png" class="img-responsive" alt=""> </div>

- Apply to filter, derive, aggregate.
- Create Data Flow level parameter and Pipeline level parameter.
- Create, Trigger, Moniter the pipeline.
- Check data in Synapse table.
    <img src="result_images\check_data_synapse.png" class="img-responsive" alt=""> </div>

5. Publish the project to Github
- Login to your Github account and create a new Repo in Github.
- Connect Azure Data Factory to Github.
- Select your Github repository in Azure Data Factory.
- Publish all objects to the repository in Azure Data Factory.

### Azure Architecture ([link]() to draw.io)

<img src="result_images\flowchart.gif" class="img-responsive" alt=""> </div>
