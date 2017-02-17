# DRA-Jenkins plugin

This plugin provides customized build steps and statuses so that you can integrate IBM® Cloud DevOps Insights with Jenkins projects.

## Using the plugin 

### Prerequisites

You must have access to a local Jenkins project or to a server that is running a Jenkins project.

### Creating a Bluemix Continuous Delivery toolchain


Before you can integrates DevOps Insights with a Jenkins project, you must create an IBM® Bluemix Continuous Delivery toolchain. Toolchains provide you with a central place to adminster and integrate tools for DevOps projects. If you'd like to learn more about Continuous Delivery, see [its documentation](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html).

Click [here](https://console.ng.bluemix.net/devops/create) to create a toolchain. After you create the toolchain, add the **DevOps Insights** service to it. See [the DevOps Insights documentation](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html) for more about adding the service to your toolchain. 

### Installing the plugin

  Install the DevOps Insights plugin in your Jenkins project:

  1. If you are an IBM employee, download it from [here](https://github.ibm.com/oneibmcloud/Jenkins-IBM-Bluemix-Toolchains/blob/release/target/dra.hpi). Otherwise contact jichen@us.ibm.com or aggarwav@us.ibm.com to get the plugin.
  2. In your Jenkins installation, click **Manage Jenkins**, select **Manage Plugins**, and select the **Advanced** tab.
  3. Click **Choose File** and select the DevOps Insight plugin installation file.
  4. Click **Upload**.
  5. Restart Jenkins and verify that the plugin was installed successfully.

### Integrating DevOps Insights with your Jenkins project

When the plugin is installed, you can integrate DevOps Insights into your Jenkins project. DevOps Insights aggregates and analyzes the results from unit tests, functional tests, and code coverage tools to determine whether your code meets predefined policies at gates in your deployment process. If your code does not meet or exceed a policy, the deployment is halted, preventing risky changes from being released. You can use DevOps Insights as a safety net for your continuous delivery environment, a way to implement and improve quality standards over time, and a data visualization tool to help you understand your project's health.

Go to the [control center](https://control-center.ng.bluemix.net/) to view the dashboard or create a policy for the quality gate that you are going to use for your project.

As a general workflow:

1. Open the configuration of any jobs (build, test, deployment, etc.) that you already have.
2. Add a post-build action with the corresponding type (**Publish build information to DevOps Insights** for build jobs, **Publish test result to DevOps Insights** for test jobs, or **Publish deployment information to DevOps Insights** for deployment jobs) to your job. Complete the required fields. 
 - In the Credential field, choose your Bluemix ID and password. If they are not saved in Jenkins, click the Add button to add and save them. Use the **Test Connection* button to test your connection with Bluemix.
 - In the Build Job Name field, specify your build job's name exactly as it is in Jenkins. If the build occurs together with the test job, leave this field empty. If the build job occurs outside of Jenkins, check **Builds are being done outside of Jenkins** and specify the build number and build URL.
 - For the environment, if the tests are running in build stage, just select the *Build Environment*; if the tests are running in deployment stage, select the *Deploy Environment* and you can specify the environment name in it. Currently two values are supported: **STAGING** and **PRODUCTION**.
 - For the Result File Location field, specify the result file's location. If the test doesn't generate a result file, leave this field empty. The plugin will upload a default result file based on the status of current test job.
 
     Here are some example configurations:
     ![Upload Build Information](https://github.com/imvijay2007/Jenkins-IBM-Bluemix-Toolchains/blob/master/screenshots/Upload-Build-Info.png "Publish Build Information to DRA")
     ![Upload Test Result](https://github.com/imvijay2007/Jenkins-IBM-Bluemix-Toolchains/blob/master/screenshots/Upload-Test-Result.png "Publish Test Result to DRA")
     ![Upload Deployment Information](https://github.com/imvijay2007/Jenkins-IBM-Bluemix-Toolchains/blob/master/screenshots/Upload-Deployment-Info.png "Publish Deployment Information to DRA")

3. _(Optional)_: If you want to have DevOps Insights policy gates to control the downstream deploy job, choose the "Evaluate Gate Policy" option in the **Publish test result to DevOps Insights** post-build action. Choose the policy you want, or add another post-build action with the type **DevOps Insights Gate** and complete the required fields. You can specify the scope of test results for Build, Deploy or all environments. Check **Fail the build based on the policy rules** to let this action to prevent downstream deployments.
    
    Here is an example gate configuration:
    ![DevOps Insights Gate](https://github.com/imvijay2007/Jenkins-IBM-Bluemix-Toolchains/blob/master/screenshots/DRA-Gate.png "DevOps Insights Gate")

4. Click **Apply** and then **Save**.
5. To run the project, click **Build Now** from the project page.
6. After the build runs, go to the [control center](https://control-center.ng.bluemix.net/) to check your build status in the dashboard. If you have gates set up, you can also see DevOps Insights results on the Status page of current build.

## License

Copyright (c)2016 IBM Corporation

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
