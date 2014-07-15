# openshift-appdynamics-jboss-cartridge 

This OpenShift embedded/plugin cartridge will enable AppDynamics monitoring on JBoss AS, JBoss EAP, JBoss EWS applications. It will install AppDynamics AppServer Agent on the gear and will report metrics to the configured AppDynamics controller.

## Install ##

Once you have created a Jboss application (AS,EAP or EWS only) either through the OpenShift Web or RHC command line util, please follow the next step to add the jboss appDynamics cartridge. 

Make sure you have the ports enabled for SSL and non-ssl configurations.

```
	rhc add-cartridge -a <app_name> \
				  -e OPENSHIFT_APPD_JAVA_CONTROLLER_HOST=<appd_contr_host> \
				  -e OPENSHIFT_APPD_JAVA_CONTROLLER_PORT=<appd_contr_port> \ 
				  -e OPENSHIFT_APPD_JAVA_CONTROLLER_APP_NAME=<appd_app_name> \ 
				  -e OPENSHIFT_APPD_JAVA_CONTROLLER_TIER_NAME=<appd_tier_name> \
				  -e OPENSHIFT_APPD_JAVA_CONTROLLER_NODE_NAME=<appd_node_name> \
				  -e OPENSHIFT_APPD_JAVA_CONTROLLER_SSL_ENABLED=<true/false>\
				  -c https://raw.githubusercontent.com/Appdynamics/openshift-appdynamics-jboss-cartridge/master/metadata/manifest.yml

```

The application has to be restarted either by using the above restart command or by pushing code which would inherently restart the application. 



```
	rhc app restart <app_name>
```



## Remove ##

```
	rhc cartridge-remove appdynamics-jboss-cart -a <app_name>
```