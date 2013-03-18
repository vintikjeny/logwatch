# Description #
This is a set of custom filters and settings for monitoring different services with **logwatch** (http://sourceforge.net/projects/logwatch/). Copy this files in your _/etc/logwatch/_ directory.
# Services #
## Tomcat 7 ##
This service able to accumulate and summarize information about Errors in _catalina.out_ log file.
It has 2 modes:

*	**short** (logwatch detail level is LOW) - produse only information about total errors count and unique errors count
*	**full** (logwatch detail level is MED or HIGH) - additionally, produce error messages for every unique error

### Example ###
Short mode:
	
	
	--------------------- Tomcat 7 Begin ------------------------  	
	Unique errors: 2
	Total num of Errors: 18
	--------------------- Tomcat 7 End ------------------------

Full mode:
	
	--------------------- Tomcat 7 Begin ------------------------
	Message: SEVERE: Terminal error:
	java.lang.ClassCastException: java.util.Collections$UnmodifiableSet cannot be cast to java.lang.Boolean
	Count: 14
	-------------------------------
	Message: SEVERE: Terminal error:
	com.vaadin.event.ListenerMethod$MethodException: Invocation of method buttonClick in com..admin.ui.view.pe.process.ProcessInstancesView$2 failed.
	Caused by: java.lang.NullPointerException
	Count: 4
	-------------------------------
	Unique errors: 2
	Total num of Errors: 18
	--------------------- Tomcat 7 End ------------------------
	
