# mssql-agent-docker
Dockerfile for using MSSQL on Linux Docker Container with the Server Agent activated

# How to use

You can build your own Docker Image or use the one I already built and create a container in the following way:
(changing the defaults for the correct ones for you)

docker create \
-e 'ACCEPT_EULA=Y' \
-e 'SA_PASSWORD=reallySecurePassord' \ 
-e 'MSSQL_PID=Express'  \  
-p 1433:1433 \   
-v sqlvolume:/var/opt/mssql \   
--name db-mssql \ 
nicolasmgaray/mssql-withagent

# Agent still offline?

If the agent is still offline, you should exec the following SQL statements in the DB:

1) Enable showing advance options:

EXEC SP_CONFIGURE 'show advanced options',1
GO
RECONFIGURE
GO
EXEC SP_CONFIGURE 'show advanced options'

2) Enable the SP_CONFIGURE of the agent:

EXEC SP_CONFIGURE 'Agent XPs',1
GO
RECONFIGURE

3) Then  you should be able to start up the Agent from the configuration manager

