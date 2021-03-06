Using Tomcat
----------------

Dependencies
~~~~~~~~~~~~
You must add some libraries inside the ``TOMCAT_HOME/lib`` folder:

-  the JDBC module of the metadata database with its dependencies (if any);
-  the JDBC module of the data database with its dependencies (if any);
-  the module which includes the commonj library with its dependencies (if any):

   -  geronimo-commonj_1.1_spec-1.0.jar,
   -  concurrent.jar,
   -  foo-commonj.jar.
   
You can download here **TODO**

File system resources
~~~~~~~~~~~~~~~~~~~~~~~~

Create the folder ``TOMCAT_HOME/resources``. Such a folder will contain some useful static resources and the indexes for the search engine used by Knowage.

Metadata database connection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a new connection, edit the ``TOMCAT_HOME/conf/server.xml`` and add the information related to the metadata database inside the ``GlobalNamingResources`` tag. Specify: username, password, driver class name and URL. 
We need to create two connection:

- ``jdbc/knowage``:  Knowage metadata 

.. code-block:: xml
		:linenos:
		
		<Resource auth="Container" 
				driverClassName="<JDBC driver>" 
				name="jdbc/knowage"
				password="<password>" 
				type="javax.sql.DataSource" 
				url="<JDBC URL>" 
				username="<user name>"
				maxWait="-1" 
				maxActive="10" 
				maxIdle="1" 
				validationQuery="<validation query>" 
				removeAbandoned="true" 
				removeAbandonedTimeout="3600" 
				logAbandoned="true" 
				testOnReturn="true" 
				testWhileIdle="true" 
				timeBetweenEvictionRunsMillis="10000" 
				minEvictableIdleTimeMillis="60000" 
				factory="org.apache.tomcat.jdbc.pool.DataSourceFactory" /> 

- ``jdbc/cache_ds``: Knowage cache, this must be an emty schema  

.. code-block:: xml
		:linenos:
		
		 <Resource auth="Container" 
				driverClassName="<JDBC driver>" 
				name="jdbc/cache_ds"
				password="<password>" 
				type="javax.sql.DataSource" 
				url="<JDBC URL>" 
				username="<user name>"
				maxWait="-1" 
				maxActive="10" 
				maxIdle="1" 
				validationQuery="<validation query>" 
				removeAbandoned="true" 
				removeAbandonedTimeout="3600" 
				logAbandoned="true" 
				testOnReturn="true" 
				testWhileIdle="true" 
				timeBetweenEvictionRunsMillis="10000" 
				minEvictableIdleTimeMillis="60000" 
				factory="org.apache.tomcat.jdbc.pool.DataSourceFactory" />

Connection to business data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Edit the ``TOMCAT_HOME/conf/server.xml`` and add the information related to the metadata database inside the ``GlobalNamingResources`` tag, specifying username, password, driver class name and URL. 

.. code-block:: xml
	:linenos:
	
	 <Resource auth="Container" 
			driverClassName="<JDBC driver>" 
			name="jdbc/dwh"
			password="<password>" 
			type="javax.sql.DataSource" 
			url="<JDBC URL>" 
			username="<user name>"
			maxWait="-1" 
			maxActive="10" 
			maxIdle="1" 
			validationQuery="<validation query>" 
			removeAbandoned="true" 
			removeAbandonedTimeout="3600" 
			logAbandoned="true" 
			testOnReturn="true" 
			testWhileIdle="true" 
			timeBetweenEvictionRunsMillis="10000" 
			minEvictableIdleTimeMillis="60000" 
			factory="org.apache.tomcat.jdbc.pool.DataSourceFactory" />


Environment variables definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Edit the file ``TOMCAT_HOME/conf/server.xml`` in Tomcat and add the following constants in the ``GlobalNamingResources`` tag, by setting the domain within the ``host_url`` value. That domain will be used by the browser to call Knowage server.

.. code-block:: xml
        :linenos:
        :caption: Tomcat environment variables configuration.

        <Environment name="resource_path" type="java.lang.String" value="${catalina.home}/resources"/>
	<Environment name="sso_class" type="java.lang.String" value="it.eng.spagobi.services.common.FakeSsoService"/>
	<Environment name="service_url" type="java.lang.String" value="http://localhost:8080/knowage"/>
	<Environment name="host_url" type="java.lang.String" value="<server URL which is hosting knowage>"/>            

Such environment variables have the following meaning:

- ``resource_path``: resources folder path,
- ``sso_class``:SSO connector class name,
- ``service_url``:backend services address, typically set to ``http://localhost:8080/knowage``,
- ``host_url``: frontend services address, the one the user types in his browser.

Applications deploy
~~~~~~~~~~~~~~~~~~~~~~
To deploy Knowage you have to copy all the WAR files inside the ``TOMCAT_HOME/webapps`` folder. 
Once the first start is ended each WAR file will be unzipped. It is also possible to unzip the WAR files manually using the unzip utility.


Thread pool defintion
~~~~~~~~~~~~~~~~~~~~~~
You must configure ``TOMCAT_HOME/conf/server.xml`` file and add the settings related to the pool of thread editing the ``GlobalNamingResources`` tag, as shown follow.

.. code-block:: xml
	:linenos:
	
	<Resource auth="Container" factory="de.myfoo.commonj.work.FooWorkManagerFactory" maxThreads="5" name="wm/SpagoWorkManager" type="commonj.work.WorkManager"/> 


Advanced memory settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is recommended to increase the memory dimension used by the application server. This can be done by adjusting some properties. The memory required by each application server depends on many factors: number of users, type of analyses, amount of handled data, etc. The minimum requirements are ``Xms1024m`` and ``Xmx2048m``.

**[LINUX]** Insert at the beginning of the ``TOMCAT_HOME/bin/setenv.sh`` file this command:

.. code-block:: bash
	:linenos:
	
	export JAVA_OPTS="$JAVA_OPTS -Xms1024m -Xmx2048m -XX:MaxPermSize=512m" 


**[WIN]** Insert at the beginning of the ``TOMCAT_HOME/bin/setenv.bat`` file this command:

.. code-block:: bash
	:linenos:
	
	set JAVA_OPTS= %JAVA_OPTS% -Xms1024m Xmx2048m -XX:MaxPermSize=512m
