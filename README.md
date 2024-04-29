# Weather Data Ingestion from OpenWeatherMap API
# An AWS data pipeline for ingesting the Weather data from the OpenWeatherMap into Redshift.

# Prerequisites
* A good understanding of AWS Services: Git and Github basics, AWS Codebuild, S3, VPC, Airflow, Glue, MWAA, IAM and Redshift.
* Good understanding of Python, and SQL.
* Knowledge of AWS security best practices, including IAM (Identity and Access Management) roles and policies.

# Project Motivation
### This project aims to leverage AWS serverless infrastructure to ingest the Weather data from OpenWeatherMap API into Redshift.

# Architecture Diagram
![Architecture Diagram](./Architecture_Watermarked/Architecture_Diagram_Weather_Data_From_API_Ingestion.png?raw=true)

# Architecture Diagram Steps
1. **GitHub Code Repository**: The source code, configurations, and scripts are stored in a GitHub repository.
2. **AWS CodeBuild**: Upon code changes, AWS CodeBuild compiles the source code, runs tests, and produces deployment artifacts.
3. **S3 Data, Airflow Configs, and Scripts**: CodeBuild build will copy all the required artifacts like scripts, DAGs, config files into the S3 bucket.
4. **Apache Airflow DAG**: The DAG file defines the sequence of tasks in the data pipeline.
5. **Extract API Data**: The first task extracts weather data from the OpenWeatherMap API.
6. **Upload to S3**: The extracted JSON weather data is uploaded to an Amazon S3 bucket.
7. **Trigger Transformation DAG**: Another Airflow DAG is triggered for data transformation. This is done to maintain isolation between fetching DAG and the transformation DAG.
8. **AWS Glue ETL**: AWS Glue performs the extract, transform, and load (ETL) operations on the weather data.
9. **Load into Amazon Redshift**: The transformed data is loaded into Amazon Redshift for storage and analysis.

## Steps and Descriptions to build the pipeline
1. **Creating an Empty GitHub Repository**
   - Set up an empty GitHub repository to manage the source code of the CI/CD pipeline.
   ![Create GitHub Repository](./Images_Watermarked/1%20Create%20an%20empty%20github%20repository%20for%20CICD.png?raw=true)

2. **Creating an S3 Bucket for Weather Data**
   - Create an S3 bucket to store weather data fetched from the Open Weather Map API.
   ![Create S3 Bucket](./Images_Watermarked/2%20Create%20an%20empty%20s3%20bucket%20where%20all%20the%20weather%20data%20from%20the%20api%20will%20land%20from%20the%20open%20weather%20map%20api.png?raw=true)

3. **Setting Up CodeBuild for CI/CD**
   - Initialize AWS CodeBuild to automate the CI/CD process for deploying updates.
   ![Setup CodeBuild](./Images_Watermarked/3%20Create%20a%20codebuild%20for%20CICD%201.png?raw=true)

4. **Additional CodeBuild Setup**
   - Further configuration of AWS CodeBuild projects to handle different pipeline stages.
   ![Configure Additional CodeBuild](./Images_Watermarked/4%20Create%20a%20codebuild%20for%20CICD%202.png?raw=true)

5. **Finalizing CodeBuild Configuration**
   - Complete the setup of AWS CodeBuild with necessary build specifications and environment variables.
   ![Finalize CodeBuild Setup](./Images_Watermarked/5%20Create%20a%20codebuild%20for%20CICD%203.png?raw=true)

6. **Additional CI/CD Configurations**
   - Setup additional configurations and hooks for AWS CodeBuild.
   ![Additional CI/CD Configurations](./Images_Watermarked/6%20Create%20a%20codebuild%20for%20CICD%204.png?raw=true)

7. **Complete CI/CD Pipeline Configuration**
   - Finalize all settings for a fully functional CI/CD pipeline using AWS CodeBuild.
   ![Complete CI/CD Configuration](./Images_Watermarked/7%20Create%20a%20codebuild%20for%20CICD%205.png?raw=true)

8. **Script Modifications and Commit**
   - Modify scripts and commit changes to the development branch in preparation for deployment.
   ![Modify and Commit Scripts](./Images_Watermarked/8%20Making%20all%20the%20changes%20to%20the%20scripts%20and%20commiting%20them%20to%20the%20dev%20branch.png?raw=true)

9. **Push Changes to GitHub**
   - Push the updated development branch to GitHub.
   ![Push to GitHub](./Images_Watermarked/9%20pushed%20the%20dev%20branch%20to%20github.png?raw=true)

10. **Creating a Pull Request**
    - Create a pull request to merge changes from the development branch to the main branch.
    ![Create Pull Request](./Images_Watermarked/10%20Creating%20a%20pull%20request%20to%20merge%20dev%20branch%20on%20to%20the%20main%20branch.png?raw=true)

11. **Merging the Pull Request**
    - Approve and merge the pull request to update the main branch with changes.
    ![Merge Pull Request](./Images_Watermarked/11%20Merge%20the%20pull%20request.png?raw=true)

12. **Triggering CodeBuild with Merge**
    - Trigger AWS CodeBuild automatically by merging changes to the main branch.
    ![CodeBuild Triggered by Merge](./Images_Watermarked/12%20Codebuild%20triggered%20by%20the%20merge.png?raw=true)

13. **Viewing CodeBuild Execution Logs**
    - Monitor the execution logs of AWS CodeBuild to track the deployment steps.
    ![CodeBuild Execution Logs](./Images_Watermarked/13%20Codebuild%20logs%20of%20the%20steps%20that%20are%20getting%20executed.png?raw=true)

14. **CodeBuild Success**
    - Confirm the successful completion of the AWS CodeBuild process.
    ![CodeBuild Succeeded](./Images_Watermarked/14%20Codebuild%20Succeded.png?raw=true)

15. **Glue Script Deployment to S3**
    - AWS Glue scripts successfully deployed to the designated S3 bucket by codebuild.
    ![Glue Script in S3](./Images_Watermarked/15%20Glue%20Script%20landed%20in%20the%20s3%20bucket.png?raw=true)

16. **Airflow DAG Deployment to S3**
    - Airflow DAGs successfully placed in the DAGs folder of the S3 bucket for workflow management.
    ![Airflow DAGs in S3](./Images_Watermarked/16%20Airflow%20DAGs%20landed%20in%20the%20DAGs%20folder%20of%20the%20s3%20bucket.png?raw=true)

17. **Deployment of requirements.txt to S3**
    - The `requirements.txt` file for the project successfully landed in the S3 bucket.
    ![requirements.txt in S3](./Images_Watermarked/17%20requirements.txt%20file%20landed%20as%20well.png?raw=true)

18. **Adding API Key to Airflow Variables**
    - Integration of the Open Weather Map API key into the Airflow environment for secure API calls.
    ![API Key in Airflow Variables](./Images_Watermarked/18%20Add%20the%20API%20key%20of%20open%20weather%20map%20into%20the%20Airflow%20Variables.png?raw=true)

19. **Airflow UI Displaying DAGs**
    - Visualization of the newly added DAGs in the Airflow user interface, confirming their availability for execution.
    ![Airflow UI DAGs Display](./Images_Watermarked/19%20The%20dags%20that%20we%20have%20added%20to%20the%20dags%20folder%20visible%20in%20the%20Airflow%20UI.png?raw=true)

20. **Triggering the DAG**
    - Manually triggering the DAG for immediate execution, with an option to schedule daily runs.
    ![Trigger DAG](./Images_Watermarked/20%20Triggering%20the%20dag.%20We%20can%20also%20schedule%20it%20if%20we%20want.%20Currently%20this%20runs%20on%20schedule%20only%20once%20a%20day%20so%20we%20will%20trigger%20it%20now.png?raw=true)

21. **Successful Data Fetch and Store in S3**
    - Confirmation of successful data retrieval and storage in S3, executed by the triggered DAG.
    ![Fetch and Store Success](./Images_Watermarked/21%20Fetching%20and%20Storing%20in%20S3%20successful.png?raw=true)

22. **Second DAG Trigger and Success**
    - The second DAG also triggered successfully and completed its intended tasks.
    ![Second DAG Success](./Images_Watermarked/22%20Second%20DAG%20also%20triggered%20and%20succeded.png?raw=true)

23. **Glue Job Trigger and Success**
     - AWS Glue job triggered by the DAG and executed successfully.
    ![Glue Job Success](./Images_Watermarked/22_2%20Glue%20Job%20triggered%20and%20succeded.png?raw=true)

24. **Data Ingested into Redshift Table**
    - Data successfully ingested into the AWS Redshift table, ready for analysis and reporting.
    ![Data Ingestion into Redshift](./Images_Watermarked/23%20Data%20Ingested%20into%20the%20Redshift%20Table.png?raw=true)


# Potential Next Steps
1. **_Implement Detailed Monitoring:_** Utilize AWS CloudWatch extensively to monitor the performance and health of your CI/CD pipeline and related AWS services like CodeBuild, Airflow, and AWS Glue. Set up custom metrics, alarms, and dashboards to get real-time insights into operational issues and system performance.
2. **_Enhanced Test Automation:_** Incorporate more comprehensive automated tests within your pipeline, including performance, security, and load testing. Utilize tools like AWS CodePipeline’s integration with third-party testing tools or develop custom Lambda functions to perform these tests.
3. **_Blue/Green Deployments:_** Implement blue/green deployment strategies to reduce downtime and risk by ensuring that you have two production environments running simultaneously, which allows easy rollback in case of issues.
4. **_Auto-Scaling:_** Implement auto-scaling capabilities for your Airflow workers based on workload, and for AWS Redshift to handle varying loads seamlessly. This ensures that your system remains responsive and cost-effective under different load conditions.
5. **_Machine Learning Integration:_** Leverage AWS SageMaker to integrate machine learning models directly into your data processing workflows. This could enable more advanced analytics such as predictive analytics on weather data.