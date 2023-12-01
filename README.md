# ADDI-CHALLENGE
The function of this repository is to show the step-by-step challenge for the support position.
Before starting the test you must prepare the test environment in this case it is necessary to virtualize a Linux environment in the hypervisor of your choice in this case it was done using VMware, once the virtual machine is deployed you must install the following:

* Have docker installed
* Have docker compose installed
* Have Git installed

1- You received a message from a person from the Go To Market team that oversee the Stores operation. They need an information from our database and you could help this person to have it by doing a query there. The person requested a list of all the tags that we currently use and how many stores are using each tag. Create a query that allow you to provide this information to the Go To Market team.

*This is done in the DB administration application of your choice (in this case DBeaver was used).*


Para la realización de este primer punto se debe crear la siguiente consulta, teniendo en cuenta que la BBDD se encuentra en un formato .json y de igual forma se encuentra en un sistema de adminitración de base de datos PostgreSQL.


-- Inquiry for a list of labels and the number of stores using them
