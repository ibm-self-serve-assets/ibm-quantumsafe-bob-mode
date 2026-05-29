# ibm-quantumsafe-bob-mode
This repository will hold the code base for several IBM Bob modes meant for Guardium and Quantum Safe accelerators.

### Bob Mode to Evaluate Quantum Readiness of a project
In this mode, Bob does the following activities to analyze the given code base for Quauntum crypto vulnerabilites.
  1. Bob connects to the Quantum Safe Explorer (QSE) instance, executes the command and initiates the source code evalution
  2. QSE identifies all the crypto vulnerable algorithms, libraries and APIs. It records them in a findings file.
  3. Bob now initiates the upload of this file into Guardium Cryptography Manager (GCM) through the connected MCP server.
  4. In GCM the entire crypto posture is made available on a dashboard with detailed inferences.
  5. The developer can now remediate those code vulnerabilities using Bob's Code mode

#### Prerequisites
The following applications need to be installed and configured. All these products can be downloaded from the IBM Partner portal.
1. Guardium Cryptography Manager (GCM) Version 2.0.1.x : This is the application that provides the overall Quantum posture. This needs to be installed in a kubernetes environment. The system requirements for this product is available [here](https://www.ibm.com/docs/en/guardium-cm/2.0.0?topic=system-requirements-prerequisites). For a development environment, a simple single node installation would suffice. Follow the instructions provided in this [documentation](https://www.ibm.com/docs/en/guardium-cm/2.0.0?topic=installing-guardium-cryptography-manager) to install and configure the appliance.  
2. Quantum Safe Explorer (QSE) 2.2.x or 2.3.x: This is the source code scanning product used by Bob to fetch the crypto vulnerabilities. This product is installed in the developer machine. The system requirements for this product is available [here](https://www.ibm.com/docs/en/quantum-safe/quantum-safe-explorer/2.x?topic=quantum-safe-explorer-overview) and installation documentation can be found [here](https://www.ibm.com/docs/en/quantum-safe/quantum-safe-explorer/2.x?topic=installing-uninstalling-quantum-safe-explorer). However, for this automated environment we need to have the command line version of this product as mentioned [here](https://www.ibm.com/docs/en/quantum-safe/quantum-safe-explorer/2.x?topic=quantum-safe-explorer-command-line-interface-cli)
3. Install and configure the  QSE VScode extension in IBM Bob IDE. Instructions for the same is found [here](https://www.ibm.com/docs/en/quantum-safe/quantum-safe-explorer/2.x?topic=installing-uninstalling-quantum-safe-explorer-visual-studio-code-extension). 

#### Execution steps
1. QSE CLI binary installation: As said before, this is required for executing the crypto analysis in a cli mode by IBM Bob
Place the binary in this path `/usr/local/bin/qse-cli-artifacts` and make sure `cli.sh` within the directory has execute permission.

2. QSE VScode extension installation in IBM Bob
Import the VSCode extension using the downloaded .vsix file.

3. Run modified GCM mcp server locally:
Check out the following [repo](quantum-readiness/custom-gcm-mcp-main) to setup and configure mcp server locally. This MCP server holds the api commands to work directly with the installed GCM server in the environment. Configure this MCP server with the URLs and other details pertaining to your GCM server. Once GCM and MCP are up attach the MCP server to IBM Bob from its MCP server settings.

4. Import the Bob mode to your project placed [here](quantum-readiness/qse-export.yaml). The mode name would be "Quantum Safe Explorer".
   
5. Open your code base in the Bob

##### Run
Select the mode from drop down and Use the following prompt to invoke the mode. Once this is done, Bob will execute the steps one by one and the results will be uploaded to GCM. Use this navigation to see the results. Expand the burger menu on top left and navigate to  "Inventory -> Code repositories".

```sh
Analyse quantum safe readiness in the current project.
```



### Original Prompt to Bob Mode written for generation of this mode
The following is the prompt used to write this mode with Bob. Here in this example we are holding our souce code under the master folder "crypto-samples". This folder contains primarily a java code base and we have dealt with execution commands related to the same. 

```sh
Here is the example commands to run the quantum safe explorer for the given project. 

Cryptographic Analytics command:
cd /usr/local/bin/qse-cli-artifacts && ./cli.sh -i /Users/<your folder>/gsi/quantum/qse/crypto-samples -l .java -cf /Users/<your folder>/gsi/quantum/qse/crypto-samples -da

API discovery command: cd /usr/local/bin/qse-cli-artifacts && ./cli.sh -i /Users/shetty/gsi/quantum/qse/crypto-samples -l .java 

The following command contains "/usr/local/bin/qse-cli-artifacts" where the quantum safe explorer is installed and would be configured. The configuration of QSE is an one time activity.  "./cli.sh" is the script that scans the code for quantum safe readiness and "-i" is the code-base which the default value is current working directory or pwd , -l is the language (possible values .java, .go, .dart, .java, .py, .cpp) -cf is the class_file_path  which is the required field only for  java language and has the default value same as -i and -da is the a mandatory flag for Cryptographic Analytics command and not required for API discovery. The Cryptographic Analytics scan is only available for Java language and for quantum readiness it needs to run both the scans (Cryptographic Analytics and API discovery). For all the other languages just run the API discovery. After running the scan no additional report needs to be generated.

I want to create a mode which runs quantum safe explorer using the above command structure and gets the required values from the environment and the code and constructs the above command and runs the command.

At the end of current workflow in the mode, I would want to push the findings json file to Guardium cryptographic manager(qcm) using the mcp server. 

Use the qcm_api tool to perform the api requests. You need profile id of the qse findings profile to upload/import the profile to GCM. you can use the following service and operation to fect the profile information

```
