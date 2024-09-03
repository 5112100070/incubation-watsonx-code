# Incubation Watsonx Code

## Install Watsonx Code Plugin
Steps to install the extension:

1. Download and Install VSCODE from [official website](https://code.visualstudio.com/download) or [click](https://github.com/5112100070/incubation-watsonx-code/blob/main/bin/VSCodeUserSetup-arm64-1.92.2.exe).

2. Download plugin for [watsonx code](https://github.com/5112100070/incubation-watsonx-code/blob/main/bin/watsonx-code-demo-1.0.1.vsix)

3. Open VSCode.

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/plugin-installation/images-1.png)

3. After that, Go to the Extensions view by clicking on the Extensions icon in the Activity Bar on the side of the window.

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/plugin-installation/images-2.png)

4. Click on the `...` in the top-right corner of the Extensions view and select "Install from VSIX..."

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/plugin-installation/images-3.png)

5. You can check the icon if the installation success

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/plugin-installation/images-4.png)

## How to use Watsonx Code Plugin
1. Create new project on VSCode

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/how-to-use-plugin/images-1.png)

2. Create new file with extension programming language.
Currently plugin only support python, javascript, java, csharp, go, cobol, and php.

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/how-to-use-plugin/images-2.png)

3. type using natural language on vscode with comment value.
![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/how-to-use-plugin/images-3.png)

4. Right click on mouse, and select **Watsonx GenAI Code Demo**, and then **Generate Code**.
![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/how-to-use-plugin/images-4.png)

5. You can check code successfully generated
![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/how-to-use-plugin/images-5.png)

## Implement API on API Connect IBM
1. Login API CONNECT. You can login by [click](https://apim-demo-mgmt-api-manager-tools.apps.66cded8c70150268e8a815ef.ocp.techzone.ibm.com/auth/manager/sign-in/)

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/implement-api-on-apic/images-1.png)

2. Select **Develop API and Products**

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/implement-api-on-apic/images-2.png)

3. Click **Add -> API**

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/implement-api-on-apic/images-3.png)

4. Click **New OpenAPI** and fill this value.
Title: **Get Detail Account**
Base Path: **/**
click **Next**

uncheck **Secure using Client ID** and **CORS**. Last step edit that API.

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/implement-api-on-apic/images-4.png)

5. On Edit API page detail. Remove Base Path

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/implement-api-on-apic/images-5.png)

6. Select **Path** on sub menu. And fill path with this value **/v1/mandiri/account**

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/implement-api-on-apic/images-6.png)

7. Define Operation **get** 

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/implement-api-on-apic/images-7.png)

8. Below method operation, select parameter to define parameter. and fill value
Name: **account_no**
Check: **Required**
Located in: **query**
Type: **string**

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/implement-api-on-apic/images-8.png)

9. Create method **OPTIONS** to handle that path. It is to fix CORS.

10. Open tab **Gateway**

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/implement-api-on-apic/images-9.png)

11. Go to sub menu **Properties -> Target Url** and on property value change the value to **https://ibm-ce.com**

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/implement-api-on-apic/images-10.png)

12. Search **Policies** on sub menu and click **Invoke**.
change URL from: `$(target-url)`
to : `$(target-url)$(request.path)$(request.search)`

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/implement-api-on-apic/images-11.png)

13. Click Save Button

14. Click Sub Menu Test

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/implement-api-on-apic/images-12.png)

## Implementation API Connect using code generator

We will create example implementation of allowing ip using gateway script

1. Generate script using Plugin from VSCode with javascript extentions.
example command: `create javascript code to check allowed ip. list of allowed ip with format 10.131.*.*`
this command will generate code javascript which we can use

![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/hands-on-2/images-1.png)

2. Back to API Connect. Go to your defined api. select **Gateway -> Policies** to open logical modification. 

3. Create policies with this sequence. 
**Set Variable**:
    - Action: set
    - Set: client.isAllowed
    - Type: Boolean

**Gateway Script**:
Paste result from Code Generator to here and add this line of code on below
`context.set('client.isAllowed', checkAllowedIp(context.get('session.clientAddress')));`

**Switch**:
case 0: client.isAllowed
implement otherwise disini

create sequence like this picture:
![](https://github.com/5112100070/incubation-watsonx-code/blob/main/images/hands-on-2/images-2.png)

4. After success implement this case click Save

5. Changes you can check with hit API using **Test** feature or hit using Postman