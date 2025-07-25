# Azure AI Content Understanding Samples (.NET 8 Console App)

Welcome! Content Understanding is a solution that analyzes and comprehends various media content, such as **documents, images, audio, and video**, transforming it into structured, organized, and searchable data.

- The samples in this repository default to the latest preview API version: **2025-05-01-preview**.
- This repo will provide more samples for new functionalities in Preview.2 **2025-05-01-preview** soon.
- As of 2025/05, 2025-05-01-preview is only available in the regions documented in [Content Understanding region and language support](https://learn.microsoft.com/en-us/azure/ai-services/content-understanding/language-region-support).

---

# Quick Start

You can run this sample in **GitHub Codespaces** or on your **local machine**.

---

## Option 1: GitHub Codespaces

You can run this repo virtually in a cloud-based development environment.

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://github.com/codespaces/new?skip_quickstart=true&machine=basicLinux32gb&repo=YOUR_REPO_ID&ref=main&geo=UsEast&devcontainer_path=.devcontainer%2Fdevcontainer.json)

### Steps:

1. Click the button above to create a new Codespace.
2. Select the `main` branch, your preferred region, and a 2-core machine.
3. Once the Codespace is ready, VS Code will automatically build the Dev Container.
4. Follow the instructions in [Configure Azure AI service resource](#configure-azure-ai-service-resource).
5. Use the integrated terminal to run the project:

```bash
cd {ProjectName}
dotnet build
cd bin/Debug/net8.0/
dotnet {ProjectName}.dll
```
6. For an overview of the available projects in {ProjectName}, refer to the [Features](#features) section. We recommend starting with ContentExtraction as your first project.

---

## Option 2: Run Locally

To run the project locally, please choose one of the setup options below.
For the smoothest experience, we recommend Option 2.1, which provides a hassle-free environment setup.

---

### Option 2.1: Windows / macOS / Linux (using VS Code + Dev Container)

#### Prerequisites

- **Docker**  
    Install [Docker Desktop](https://www.docker.com/products/docker-desktop/) (available for Windows, macOS, and Linux).\
    Docker is used to manage and run the container environment.  
    - Start Docker and ensure it is running in the background.
- **Visual Studio Code**  
    Download and install [Visual Studio Code](https://code.visualstudio.com/).
- **Dev Containers Extension**  
    In the VS Code extension marketplace, install the extension named "Dev Containers".\
    (The extension was previously called "Remote - Containers", but has since been renamed and integrated into Dev Containers.)

#### Steps

1. Clone the repo:

```bash
git clone https://github.com/Azure-Samples/azure-ai-content-understanding-dotnet.git
cd azure-ai-content-understanding-dotnet
```

2. Launch VS Code and open the folder:

```bash
code .
```

3. Press `F1` → select `Dev Containers: Reopen in Container`.

4. Wait for the setup to complete. Follow the instructions in [Configure Azure AI service resource](#configure-azure-ai-service-resource), then use the integrated terminal in Visual Studio Code to run:

```bash
cd {ProjectName}
dotnet build
cd bin/Debug/net8.0/
dotnet {ProjectName}.dll
```

5. For an overview of the available projects in {ProjectName}, refer to the [Features](#features) section. We recommend starting with ContentExtraction as your first project.

---

### Option 2.2: Windows (using Visual Studio 2022 or later)

#### Prerequisites

- [.NET SDK 8.0+](https://dotnet.microsoft.com/en-us/download)
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
- [Azure Developer CLI (azd)](https://aka.ms/install-azd)
- [Git LFS](https://git-lfs.com/)

1. Clone the repo using Git or from Visual Studio:

```
git clone https://github.com/Azure-Samples/azure-ai-content-understanding-dotnet
```

1. Open the `.sln` solution file in **[Visual Studio 2022+](https://visualstudio.microsoft.com/downloads/)**.

1. Ensure the target framework is set to **.NET 8**.

1. Follow the instructions in [Configure Azure AI service resource](#configure-azure-ai-service-resource).

1. We recommend setting **ContentExtraction** as your Startup Project. For an overview of the available projects refer to the [Features](#features) section.

1. Press **F5** or click **Start** to run the console app.

---

## <a name="configure-azure-ai-service-resource">Configure Azure AI service resource</a>
### (Option 1) [UNDER CONSTRUCTION] Use `azd` commands to auto create temporal resources to run sample
1. Make sure you have permission to grant roles under subscription
1. Login Azure
    ```shell
    azd auth login
    ```
    If the previous command doesn’t work, try the following one and follow the on-screen instructions.
    ```
    azd auth login --use-device-code
    ```

1. Setting up environment, following prompts to choose location
    ```shell
    azd up
    ```

### (Option 2) Manually create resources and set environment variables
1. Create [Azure AI Services resource](docs/create_azure_ai_service.md)
1. Go to `Access Control (IAM)` in resource, grant yourself role `Cognitive Services User`
    - It's necessary even you are the owner of the resource
1. Fill **Endpoint** in [appsettings.json](ContentUnderstanding.Common/appsettings.json) with the endpoint from your Azure portal Azure AI Services instance.
1. The SubscriptionKey field in [appsettings.json](ContentUnderstanding.Common/appsettings.json) is optional. It is only needed if you choose not to authenticate using `azd auth login` or `az login`, and instead prefer key-based authentication.
1. If you’re using the recommended identity-based authentication, make sure you’re signed in to Azure by running.
   ```shell
   azd auth login
   ```
   This ensures that your Azure identity is properly authenticated for accessing secured resources.
---
## Features

Azure AI Content Understanding is a new Generative AI-based [Azure AI service](https://learn.microsoft.com/en-us/azure/ai-services/content-understanding/overview), designed to process/ingest content of any type (documents, images, audio, and video) into a user-defined output format. Content Understanding offers a streamlined process to reason over large amounts of unstructured data, accelerating time-to-value by generating an output that can be integrated into automation and analytical workflows.

| Project                     | Key source file                  | Description |
|-----------------------------|----------------------------------|-------------|
| [ContentExtraction](ContentExtraction/) | [ContentExtractionService.cs](ContentExtraction/Services/ContentExtractionService.cs) | In this sample we will show content understanding API can help you get semantic information from your file. For example OCR with table in document, audio transcription, and face analysis in video. |
| [FieldExtraction](FieldExtraction/)   | [FieldExtractionService.cs](FieldExtraction/Services/FieldExtractionService.cs) | In this sample we will show how to create an analyzer to extract fields in your file. For example invoice amount in the document, how many people in an image, names mentioned in an audio, or summary of a video. You can customize the fields by creating your own analyzer template. |
| [Management](Management/)      | [ManagementService.cs](Management/Services/ManagementService.cs) | This sample will demo how to create a minimal analyzer, list all the analyzers in your resource, and delete the analyzer you don't need. |
| [BuildPersonDirectory](BuildPersonDirectory/)      | [BuildPersonDirectoryService.cs](BuildPersonDirectory/Services/BuildPersonDirectoryService.cs) | This sample will demo how to enroll people’s faces from images and build a Person Directory. |

---

## Sample Console Output
Here is an example of the console output from the **ContentExtraction** project.
```
$ dotnet ContentExtraction.dll
Please enter a number to run sample: 
[1] - Extract Document Content
[2] - Extract Audio Content
[3] - Extract Video Content
[4] - Extract Video Content With Face 
1
Document Content Extraction Sample is running...
Use prebuilt-documentAnalyzer to extract document content from the file: ./data/invoice.pdf

===== Document Extraction has been saved to the following output file path =====

./outputs/content_extraction/AnalyzeDocumentAsync_20250714034618.json

===== The markdown output contains layout information, which is very useful for Retrieval-Augmented Generation (RAG) scenarios. You can paste the markdown into a viewer such as Visual Studio Code and preview the layout structure. =====
CONTOSO LTD.


# INVOICE

Contoso Headquarters
123 456th St
New York, NY, 10001

INVOICE: INV-100

INVOICE DATE: 11/15/2019

DUE DATE: 12/15/2019

CUSTOMER NAME: MICROSOFT CORPORATION

SERVICE PERIOD: 10/14/2019 - 11/14/2019

CUSTOMER ID: CID-12345

<<< Truncated for brevity >>>
```

---

## More Samples using Azure Content Understanding
 
- [Azure Content Understanding Samples (Python)](https://github.com/Azure-Samples/azure-ai-content-understanding-python)
- [Azure Search with Content Understanding (Python)](https://github.com/Azure-Samples/azure-ai-search-with-content-understanding-python)
- [Azure Content Understanding with OpenAI (Python)](https://github.com/Azure-Samples/azure-ai-content-understanding-with-azure-openai-python)
 
---
 
## Additional Resources
 
- [Azure Content Understanding Documentation](https://learn.microsoft.com/en-us/azure/ai-services/content-understanding/overview)
- [Region and Language Support](https://learn.microsoft.com/en-us/azure/ai-services/content-understanding/language-region-support)
 
---

## Notes

* **Trademarks** - This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft trademarks or logos is subject to and must follow [Microsoft's Trademark & Brand Guidelines](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general). Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship. Any use of third-party trademarks or logos is subject to those third-party’s policies.

* **Data Collection** - The software may collect information about you and your use of the software and send it to Microsoft. Microsoft may use this information to provide services and improve our products and services. You may turn off the telemetry as described in the repository. There are also some features in the software that may enable you and Microsoft to collect data from users of your applications. If you use these features, you must comply with applicable law, including providing appropriate notices to users of your applications together with a copy of Microsoft’s privacy statement. Our privacy statement is located at https://go.microsoft.com/fwlink/?LinkID=824704. You can learn more about data collection and use in the help documentation and our privacy statement. Your use of the software operates as your consent to these practices.

