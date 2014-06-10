# openshift-appdynamics-java-appserver-cartridge 

This OpenShift embedded/plugin cartridge will enable AppDynamics monitoring on JBoss 7 Java applications. It will install AppDynamics AppServer Agent on the gear and will report metrics to the configured AppDynamics controller.

## Install ##

Make sure you have the ports enabled for SSL and non-ssl configurations.

```
	rhc add-cartridge -a <app_name> \
				  -e OPENSHIFT_APPD_JAVA_CONTROLLER_HOST=<appd_contr_host> \
				  -e OPENSHIFT_APPD_JAVA_CONTROLLER_PORT=<appd_contr_port> \ 
				  -e OPENSHIFT_APPD_JAVA_CONTROLLER_APP_NAME=<appd_app_name> \ 
				  -e OPENSHIFT_APPD_JAVA_CONTROLLER_TIER_NAME=<appd_tier_name> \
				  -e OPENSHIFT_APPD_JAVA_CONTROLLER_NODE_NAME=<appd_node_name> \
				  -e OPENSHIFT_APPD_JAVA_CONTROLLER_SSL_ENABLED=<true/false>\
				  -c https://raw.githubusercontent.com/Appdynamics/openshift-appdynamics-java-appserver-cartridge/master/metadata/manifest.yml

```

Restart your application 

```
	rhc app restart <your_app_name>
```

## Remove ##

```
	rhc cartridge-remove appdynamics-java-appserver-agent -a <app_name>
```