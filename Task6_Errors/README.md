# Azure Functions Assignment: Task6

## Overview

This project demonstrates creating, testing, and deploying an **Azure Function App** with an **HTTP POST trigger** in C# (.NET). The function accepts a JSON input with two numbers and a name, calculates the sum of the numbers, and returns a formatted message including the name and sum.

---

## Learning Objectives

During this assignment, I learned:

1. **Azure Functions Core Tools**

   * Installed and configured **Azure Functions Core Tools v4** on Ubuntu 22.04 LTS.
   * Verified installation with `func --version`.
   * Ran functions locally using `func start`.

2. **Creating a C# HTTP-triggered Function**

   * Created a function named `HttpSumTrigger`.
   * Used **`HttpRequestData`** to read JSON input.
   * Implemented JSON parsing with **Newtonsoft.Json**.
   * Used **nullable and default values** to safely handle missing fields.
   * Returned a formatted string response including the sum of two integers.

3. **Testing Functions Locally**

   * Tested the function locally with `curl`.

4. **Deploying to Azure Function App**

   * Created a **Function App (Windows, .NET 8, Consumption plan)** in **South East Asia** region.
   * Deployed the local project using **VS Code** with the **Azure Functions extension**.
   * Logged into Azure CLI and VS Code to authenticate.

5. **Testing Deployed Function**

   * Verified the function works remotely on Azure with correct JSON input and output.

6. **Debugging Common Issues**

   * Corrected curl syntax differences between **Windows** and **Linux**.
   * Fixed “Unable to connect to Azure” by installing **Azure CLI** and logging in with `az login`.
   * Installed **.NET 8 SDK and runtime** on Ubuntu 22.04 LTS after removing older versions, since .NET 9 was not supported.

---

## Project Structure

```
Task6/
 ├── HttpSumTrigger.cs       # Main C# function code
 ├── Task6.csproj            # Project file
 ├── host.json               # Function runtime configuration
 └── local.settings.json     # Local environment settings
```

---

## Function Details

### **Function Name:** `HttpSumTrigger`

### **Trigger:** HTTP POST (Anonymous)

### **Input JSON Example:**

```json
{
  "name": "The teacher tests",
  "a": 3,
  "b": 6
}
```

### **Output Example:**

```
Abdul Nizer: Hello The teacher tests. The sum of the numbers 3 and 6 is 9.
```

---

## Tools and Technologies

* **Operating System:** Ubuntu 22.04 LTS
* **IDE:** VS Code
* **Programming Language:** C# (.NET 8)
* **Azure Services:**

  * Azure Functions (Windows host, Consumption plan, South East Asia)
  * Azure Storage Account (required for Function App)
* **Command-line Tools:**

  * Azure CLI (`az`)
  * Azure Functions Core Tools (`func`)
  * curl (HTTP testing)

---

## Steps to Run Locally

1. Install dependencies:

   ```bash
   sudo apt-get install libicu-dev -y
   ```
2. Run function locally:

   ```bash
   func start
   ```
3. Test with curl:

   ```bash
   curl -X POST http://localhost:7012/api/HttpSumTrigger \
   -H "Content-Type: application/json" \
   -d '{"name":"Test","a":3,"b":6}'
   ```

---

## Steps to Deploy to Azure

1. Ensure **Azure CLI** is installed and logged in:

   ```bash
   az login
   ```
2. Open project in **VS Code** with Azure Functions extension.
3. Right-click your **Function App (T6)** in Azure panel → **Deploy to Function App**.
4. Select local project folder **Task6/**.
5. Confirm deployment.
6. Copy **Function URL** from Azure panel → test with curl.

---

## Common Errors and Fixes

* **Unable to connect to Azure:**

  * Ensure Azure CLI is installed and logged in with `az login`.
  * Restart VS Code after login.

* **.NET SDK version issues on Ubuntu 22.04 LTS:**

  * If .NET 9 is unavailable, install **.NET 8 SDK and runtime**:

    ```bash
    sudo apt-get remove --purge 'dotnet-*'
    sudo rm -rf /usr/share/dotnet
    sudo apt-get autoremove
    sudo apt-get update -o Acquire::ForceIPv4=true
    sudo apt-get install -y -o Acquire::ForceIPv4=true dotnet-sdk-8.0
    dotnet --list-sdks
    dotnet --version
    ```

* **curl syntax errors on Linux:**

  * Use `\` for line continuation instead of `^` (Windows CMD).
  * Quote JSON data correctly with single quotes around the entire JSON string.

---

## Conclusion

This assignment taught me:

* How to build **serverless functions** in C# with Azure Functions.
* How to **test locally and deploy to Azure**.
* How to handle **JSON input and output formatting**.
* How to use **VS Code + Azure CLI** for cloud deployment.
* How to resolve **.NET SDK issues** on Ubuntu 22.04 LTS.

The assignment is now **complete**, and the deployed function is fully functional.

---

## Azure Function URL (Submission)

```
https://functionappt6-ccccf6eafxfbgza5.southeastasia-01.azurewebsites.net/api/HttpSumTrigger
```
