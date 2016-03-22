# openshift-appdynamics-jboss-cartridge 

This OpenShift embedded/plugin cartridge will enable AppDynamics monitoring on JBoss AS, JBoss EAP, JBoss EWS applications. It will install AppDynamics AppServer Agent on the gear and will report metrics to the configured AppDynamics controller.

## Install ##

Once you have created a Jboss application (AS,EAP or EWS only) either through the OpenShift Web or RHC command line util, please follow the next step to add the jboss appDynamics cartridge. 



```
	rhc add-cartridge -a <app_name> \
				  -e APPDYNAMICS_CONTROLLER_HOST_NAME=<appd_contr_host> \
				  -e APPDYNAMICS_CONTROLLER_PORT=<appd_contr_port> \ 
				  -e APPDYNAMICS_AGENT_APPLICATION_NAME=<appd_application_name> \
				  -e APPDYNAMICS_AGENT_TIER_NAME=<appd_tier_name> \
				  -e APPDYNAMICS_CONTROLLER_SSL_ENABLED=<true/false>\
				  -c http://cartreflect-claytondev.rhcloud.com/github/Appdynamics/openshift-appdynamics-jboss-cartridge

```

## SAAS environment ## 

If it is a dedicated or a multi-tenant controller, please pass the accountName and accountKey as well to the above command. 

```
	rhc add-cartridge -a <app_name> \
				  -e APPDYNAMICS_CONTROLLER_HOST_NAME=<appd_contr_host> \
				  -e APPDYNAMICS_CONTROLLER_PORT=<appd_contr_port> \ 
				  -e APPDYNAMICS_AGENT_APPLICATION_NAME=<appd_application_name> \
				  -e APPDYNAMICS_AGENT_TIER_NAME=<appd_tier_name> \
				  -e APPDYNAMICS_CONTROLLER_SSL_ENABLED=<true/false>\
				  -e APPDYNAMICS_AGENT_ACCOUNT_NAME=<appd_agent_accountname>
				  -e APPDYNAMICS_AGENT_ACCOUNT_ACCESS_KEY=<appd_agent_account_access_key>
				  -c http://cartreflect-claytondev.rhcloud.com/github/Appdynamics/openshift-appdynamics-jboss-cartridge

```
Make sure you have the right ports opened for SSL  and non-ssl  configurations.


Please note that the AppDynamics NodeName will be picked up as the Gear UUID..


The application has to be restarted either by using the above restart command or by pushing code which would inherently restart the application. 



```
	rhc app restart <app_name>
```



## Remove ##

```
	rhc cartridge-remove appdynamics-jboss-cart -a <app_name>
```


## To generate the RPM ##

Use fpm utility
```
	git clone https://github.com/jordansissel/fpm
  	gem install fpm
```
Generate version 1.0-3 rpm using fpm

```
	fpm --iteration=3 -s dir -t rpm -n appdynamics-jboss-cart ~/openshift-appdynamics-jboss-cartridge
```

## Update Agent Version in this cartridge ##

To use a specific version of the AppDynamics agent, follow these steps:

 1. Fork this repository in your GitHub account
 2. Go to /metadata/manifest.yml and update the agent versions in these two places
 ![AgentVersion](https://github.com/Appdynamics/openshift-appdynamics-jboss-cartridge/blob/master/images/agentVersion.png)
 3. Use -c parameter to point to your forked github repo
   -c http://cartreflect-claytondev.rhcloud.com/github/{YourGitHubID}/openshift-appdynamics-jboss-cartridge
 4. Install the cartridge using the above -c parameter
 
```
	rhc add-cartridge -a <app_name> \
				  -e APPDYNAMICS_CONTROLLER_HOST_NAME=<appd_contr_host> \
				  -e APPDYNAMICS_CONTROLLER_PORT=<appd_contr_port> \ 
				  -e APPDYNAMICS_AGENT_APPLICATION_NAME=<appd_application_name> \
				  -e APPDYNAMICS_AGENT_TIER_NAME=<appd_tier_name> \
				  -e APPDYNAMICS_CONTROLLER_SSL_ENABLED=<true/false>\
				  -c http://cartreflect-claytondev.rhcloud.com/github/{YourGithubID}/openshift-appdynamics-jboss-cartridge

```
