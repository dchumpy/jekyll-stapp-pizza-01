# Case 2 Pineapple Pizza Static Web App

## Users

For this solution there are created three users; Bob, Dave and Mark.

* Bob has requirements to manage billing for the Pineapple Pizza Website and is the owner of Pineapple Pizza.
  Therefore he is given the ***Owner*** role for the Azure Subscription. Owner role gives permissions to manage all resources and delegate access to other users. He will also be able to see the billing for this subscription.

* Dave has requiements for access to the resources on Azure for the Pineapple Pizza Website, but not overall permissions to the subscription. Based on the principle of least privelege Bob is therefore given the ***Contributor*** role to the resource group.

* Mark requires only read-only permission to the Pineapple Pizza resources. And are therefore given the ***Reader*** role for the resource group. This role gives him read permissions only to the resources within the resource group where the Pineapple Pizza Website are placed.

### User roles diagram



<img title="" src="assets/775412825a0b5e244a99128467a5cc06c98aea2a.png" alt="azureroles.drawio.png" data-align="center" width="398">



## Static Web App With Jekyll

The Static Web App for Pineapple Pizza are deployed using a static site generator called _Jekyll_.
This generator makes it possible to deploy the new changes to the static web app automatically as the new code are pushed. In this case changes to the code are pushed to _GitHub_, and the changes are automatically built and deployed using _GitHub Actions_.

1. **Download**
   
   First Jekyll and prerequisites has to be installed locally using Windows Subsystem for Linux. 
   
   This was done following the tutorial from Jekyll: [Jekyll on Ubuntu | Jekyll • Simple, blog-aware, static sites](https://jekyllrb.com/docs/installation/ubuntu/) 

2. **Create App**
   
   The Jekyll app was created locally.

3. **Push to GitHub**
   
   The repository for the application was then pushed to a GitHub repository.

4. **Create Static Web App in Azure Portal** 
   
   The Static Web App was set up in the Azure Portal and the application repository from GitHub was used.
   
   * First a resource group named for the static web app was created.
   
   * The hosting plan for the web app was sett to Free.
   
   * Source for the deployment was set to GitHub and credentials are provided.
   
   * When the Static Web App is created in the Azure Portal, the repository with the application code are deployed using GitHub Actions.

5. **Changes with GitHub Actions**
   
   GitHub Actions is used for this deployment. Changes to the code are pushed to GitHub and deployed through GitHub Actions.

6. **Azure Front Door**
   
   For Loadbalancing Azure Front Door is provisioned. This Load Balancing service meets the requirements for geo-redundant access. Since the application are to be accessable from London, Oslo, Singapore and Tokyo geo-rendunance is a requirement.

7. **Azure Monitor Alerts**
   
   The Azure service, *Monitor* provides the possibility to set up Alerts to help detect issues and adress these before this becomes a problem for customers and end users. Notifications can be configured to notify when an issue is detected. 
   
   Metrics are used as the source in the Azure Monitor data platform. The alert rule monitors the telemetry data, captures signals and checks to see if these sinals meet the critaria of conditions. If these conditions are met, the alert is triggered and the associated action group triggers the notification. 
   
   The rule requirement is that an email to the owner of Pineapple Pizza, Bob are to be sent if over 100 requests are sent to the Front Door solution.

8. **ARM-templates** 
   
   Azure Resource Manager Templates are downloaded from the Azure Portal. This makes is possible to deploy the application and related services by other developers in case of need. 

### Workflow Diagram

<img title="" src="assets/232b0c4fca81f1df0385e99879106787b971146d.png" alt="workflow.drawio(1).png" width="682" data-align="center">



* Jekyll is used for generating the static site. 

* Visual Studio Code is the IDE used for witing application code.

* The code is then pushed to GitHub.

* Each time new code is pushed, GitHub Actions CI/CD pipeline runs, and if the run is successful the new changes will be deployed to the static web apps in Azure.



## Azure Infrastructure Diagram

<img title="" src="assets/5d130b6b2923fba51947f7b7582999b776edd0e8.png" alt="azuresetup.drawio(2).png" data-align="center" width="374">





Within the subscription the resource group for the static web apps are created. Within this resource group the two Static Web Apps and the Azure Front Door loadbalancer are placed.

## Front Door Routing of user request

![frontdooruser.drawio.png](assets/341454bf291eeee811a4b4d4f139928d0bb4e63e.png)