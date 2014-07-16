# openshift-appdynamics-jboss-cartridge 

This OpenShift embedded/plugin cartridge will enable AppDynamics monitoring on JBoss AS, JBoss EAP, JBoss EWS applications. It will install AppDynamics AppServer Agent on the gear and will report metrics to the configured AppDynamics controller.

## Install ##

Once you have created a Jboss application (AS,EAP or EWS only) either through the OpenShift Web or RHC command line util, please follow the next step to add the jboss appDynamics cartridge. 



```
	rhc add-cartridge -a <app_name> \
				  -e APPDYNAMICS_CONTROLLER_HOST_NAME=<appd_contr_host> \
				  -e APPDYNAMICS_CONTROLLER_PORT=<appd_contr_port> \ 
				  -e APPDYNAMICS_AGENT_TIER_NAME=<appd_tier_name> \
				  -e APPDYNAMICS_CONTROLLER_SSL_ENABLED=<true/false>\
				  -c https://raw.githubusercontent.com/Appdynamics/openshift-appdynamics-jboss-cartridge/master/metadata/manifest.yml

```

If it is a multi-tenant controller, please pass the accountName and accountKey as well to the above command. 

```
	rhc add-cartridge -a <app_name> \
				  -e APPDYNAMICS_CONTROLLER_HOST_NAME=<appd_contr_host> \
				  -e APPDYNAMICS_CONTROLLER_PORT=<appd_contr_port> \ 
				  -e APPDYNAMICS_AGENT_TIER_NAME=<appd_tier_name> \
				  -e APPDYNAMICS_CONTROLLER_SSL_ENABLED=<true/false>\
				  -e APPDYNAMICS_AGENT_ACCOUNT_NAME=<appd_agent_accountname>
				  -e APPDYNAMICS_AGENT_ACCOUNT_ACCESS_KEY=<appd_agent_account_access_key>
				  -c https://raw.githubusercontent.com/Appdynamics/openshift-appdynamics-jboss-cartridge/master/metadata/manifest.yml

```
Make sure you have the ports opened for SSL (default:8181) and non-ssl (default:8090) configurations.

Please note that the AppDynamics NodeName will be picked up as the Gear UUID and the ApplicationName will be picked up from the user assigned name of the application . 

The application has to be restarted either by using the above restart command or by pushing code which would inherently restart the application. 



```
	rhc app restart <app_name>
```



## Remove ##

```
	rhc cartridge-remove appdynamics-jboss-cart -a <app_name>
```

## Versions Supported ##

AppDynamics AppServerAgent 3.8.4