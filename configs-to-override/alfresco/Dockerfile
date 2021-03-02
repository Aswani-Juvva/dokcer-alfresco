ARG ACS_TAG

FROM alfresco/alfresco-content-repository-community:${ACS_TAG}

ARG TOMCAT_SERVER_PORT=7005
ARG TOMCAT_HTTP_PORT=7080
ARG TOMCAT_SSL_PORT=7443
ARG TOMCAT_AJP_PORT=7009
ARG TOMCAT_JPDA_PORT=7000

ARG TOMCAT_DIR=/usr/local/tomcat

#Change to root so that sed command can be executed
USER root

#Update port to 7080 from 8080, 7005 from 8005, 7443 from 8443, 7009 from 8009
RUN sed -i "s/<Server\ port=\"8005\"\ shutdown=\"SHUTDOWN\">/<Server\ port=\"$TOMCAT_SERVER_PORT\"\ shutdown=\"SHUTDOWN\">/g" $TOMCAT_DIR/conf/server.xml ; \
    sed -i "s/port=\"8080\"\ protocol=\"HTTP\/1.1\"/port=\"$TOMCAT_HTTP_PORT\"\ protocol=\"HTTP\/1.1\"/g" $TOMCAT_DIR/conf/server.xml ; \
	sed -i "s/\ <Connector\ port=\"8443\"/\ <Connector port=\"$TOMCAT_SSL_PORT\"/g" $TOMCAT_DIR/conf/server.xml ; \
	sed -i "s/\ <Connector\ port=\"8009\"\ protocol=\"AJP\/1.3\"/\  <Connector\ port=\"$TOMCAT_AJP_PORT\"\ protocol=\"AJP\/1.3\"\ /g" $TOMCAT_DIR/conf/server.xml ; \
	sed -i "s/redirectPort=\"8443\"/redirectPort=\"$TOMCAT_SSL_PORT\"/g" $TOMCAT_DIR/conf/server.xml ; 


#Disable resource caching
RUN sed -i "s|<Context>|<Context>\n<Resources cachingAllowed=\"false\"/> |g" $TOMCAT_DIR/conf/context.xml ;

USER alfresco
