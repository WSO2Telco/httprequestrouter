
# HTTPRequestRouter
This application will use to send the callback from Gateway to Hub.

## How to configure
### Database setup
	Create new database on a MySql .Run the  dbscripts/database.sql . Open the HTTPRequestRouter.war file . Locate the file conf.properties at /WEB-INF/classes/.Edit the jdbc.APP.url,jdbc.APP.username,jdbc.APP.password properties as acordingly.
	jdbc.APP.url=jdbc:mysql://localhost:3306/requestrouter
	jdbc.APP.username=root
	jdbc.APP.password=4321

### Metadata
####	Add records to the headers table

		domain : 	domain or ip 
				Eg :	abc.lk or 10.2.3.4

		urlPrefix :	start part of the url 
				Eg :	http://abc.lk/api/

		header :	header key
				Eg :	Authorization

		headerValue :	value of the header
				Eg :	Bearer dfrd3343dff

		mode : this value indicate how to add the header
				Eg :	REPLACE - if the request contains the same header, requestrouter will replace the that header from new header (RECOMMENDED)
						ADD - Add the new header 
						APPEND - if the request contains the same header, requestrouter append the new header value to the header

####	Add records to the replacebody table 
	Using values in this table we can replace any json value in body. if there is no any value to replace you don't need to add records to this table

		urlKey :	<KEY> value in the request url
				Eg :	MIFE-HUB-USSD
		jsonPath :	json path of the request body
				Eg : 	$.inboundUSSDMessageRequest.responseRequest.notifyURL
		find : 		value to find in request body 
				Eg : * - replace everything				     
		replace :	replace value 
		needURLDecodeRest : this will use the url decode the url in request body
				Eg : 0 -  nothing will url decode
					 1 -  url in the request body will url decode

Start the tomcat and make sure no erros are at the log.

### Gateway configurations
locate mediator-conf.properties file at <ESB-HOME>\repository\conf\ folder. Define property "requestRouterUrl" at the conf.properties file if not exists.
	requestRouterUrl=http://<HOST>:<PORT>/HTTPRequestRouter/route/<KEY>/?org=
		Eg : requestRouterUrl=http://localhost:8080/HTTPRequestRouter/route/MIFE-HUB-USSD/?org=


