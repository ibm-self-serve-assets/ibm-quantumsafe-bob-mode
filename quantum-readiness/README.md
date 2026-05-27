### Bob Mode to Evaluate quantum Readiness of a project

#### Binaries
Get the QSE binary from [Software download](https://w3.ibm.com/w3publisher/software-downloads)
1. Download the QSE cli binary: M0V4REN (part-code)
2. Download the QSE VScode extension : M0V4VEN (part-code)

#### Installation
1. QSE CLI binary installation: 
Place the binary in this path `/usr/local/bin/qse-cli-artifacts` and make sure `cli.sh` within the directory has execute permission.

2. QSE VScode extension installation: 
Import the extension to Vscode marketplace using the downloaded .vsix file.

3. Run modified GCM mcp server locally:
check out the following [repo](https://github.ibm.com/ecosystem-engineering-lab/custom-gcm-mcp) to setup and configure mcp server locally.

4. Import the Bob mode to your project placed [here](./qse-export.yaml).

##### Run
Select the mode from drop down and Use the following prompt to invoke the mode.
```sh
Analyse quantum safe readiness in the current project.
```



### Original Prompt to Bob Mode write for generation of this mode
```sh
Here is the example commands to run the quantum safe explorer for the given project

Cryptographic Analytics command:
cd /usr/local/bin/qse-cli-artifacts && ./cli.sh -i /Users/shetty/gsi/quantum/qse/crypto-samples -l .java -cf /Users/shetty/gsi/quantum/qse/crypto-samples -da

API discovery command: cd /usr/local/bin/qse-cli-artifacts && ./cli.sh -i /Users/shetty/gsi/quantum/qse/crypto-samples -l .java 

the following command conatins "/usr/local/bin/qse-cli-artifacts" where the quantum safe explorer is installed and would be configured only once. "./cli.sh" is the script which scans the code for quantum safe readiness and "-i" is the code-base which the default value is current working directory or pwd , -l is the language (possible values .java, .go, .dart, .java, .py, .cpp) -cf is the class_file_path  which is the required field only for  java language and has the default value same as -i and -da is the a mandatory flag for Cryptographic Analytics command and not required for API discoveryThe Cryptographic Analytics scan is only available for Java language and for quantum readiness it needs to run both the scans (Cryptographic Analytics and API discovery). For all the other languages just run the API discovery. After running the scan no additional report needs to be generated.

I want to create a mode which runs quantum safe explorer using the above command structure and gets the required values from the environment and code and constructs the above command and runs the command.

At thr end of current workflow in the mode. i would want to push the findings json file to Quantum cryptographic manager(qcm) using mcp server. 

Use the qcm_api tool to perform the api requests. you need profile id of the qse findings profile to upload/import the profile to qcm. you can use the following service and operation to fect the profile information

```