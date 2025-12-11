# medium_gcp_mcp_fastapi
MCP Server via FastAPI & GCP Cloud Run 

[The complete public article can be found here](https://medium.com/@markwkiehl/deploying-an-mcp-server-on-google-cloud-run-6faebe26500e)

This repository provides a template for the deployment of a Model Context Protocol (MCP) Server on Google Cloud Run. Both the Python client and server scripts are included, as well as batch files to fully automate deployment to the Google Cloud Platform.

# Quick Start

All of the details on installation of Python, Google CLI & SDK, and Docker can be found in my seven-part article series **"Building a Data Platform on GCP"**. The more recent article **"Deploy Your Custom MCP AI Tool to Cloud Run"** also includes simple instructions.

The batch files included in my public GitHub repository contain minor updates in response to recent GCP changes, so be sure to use those versions instead of what was published previously.

1. **Install prerequisites**
   - Install Python, Google CLI & SDK, and Docker.

2. **Prepare your project folder**
   - Download a copy of the GitHub repository contents into an empty folder on your PC.
   - **Do not** name this folder the same as either of the Python scripts.
   - Expand the contents inside this folder — this folder will become your Python virtual environment.

3. **Configure Google Cloud**
   - Log in to (or create) a Google user account.
   - From the Google Admin Console, configure billing.

4. **Edit configuration**
   - Edit the file `gcp_constants.bat`.  
     **You must update this file** with:
     - Your Google account email address (`GCP_USER`)
     - Your Google Cloud Billing Account Number (`GCP_BILLING_ACCOUNT`)
   - If you are not located in the USA, consider updating:
     - `GCP_REGION`
     - `GCP_GS_BUCKET_LOCATION`  
       (See *Geography & Regions*)

5. **Start Docker**
   - Run Docker Desktop. This starts the Docker Engine required by the batch file `gcp_6_docker_build.bat`.

6. **Run the batch files**
   - Open a Windows Command Prompt.
   - Navigate to the folder where you downloaded the GitHub contents.
   - Sequentially execute each batch file:  
     `gcp_1_venv.bat`, `gcp_2_proj.bat`, … `gcp_8_bucket_runsvc.bat`.
   - **Important:** The last batch file, `gcp_8_bucket_runsvc.bat`, will output the URL for the Cloud Run service.  
     Copy that URL and update `api_mcp_fastapi_client.py`.

7. **Verify the Cloud Run deployment**
   - At this point, the Google Cloud Run service will be running your MCP server.
   - Open the Cloud Run service URL in a browser to verify functionality using the `/` endpoint.  
     The expected response is:  
     ```json
     {"status": "ok", "message": "Server is running. See /docs for API schema."}
     ```

8. **Configure the client script**
   - Edit `api_mcp_fastapi_client.py` with the Cloud Run service URL created by `gcp_8_bucket_runsvc.bat`.
   - If you didn’t capture the URL from the command output, you can find it in the Google Cloud Run Console under **Services**.

9. **Run the client**
   - Execute the script `api_mcp_fastapi_client.py`.




