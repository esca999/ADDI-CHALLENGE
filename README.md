# ADDI-CHALLENGE
The function of this repository is to show the step-by-step challenge for the support position.
Before starting the test you must prepare the test environment in this case it is necessary to virtualize a Linux environment in the hypervisor of your choice in this case it was done using VMware, once the virtual machine is deployed you must install the following:

* Have docker installed
* Have docker compose installed
* Have Git installed

1- You received a message from a person from the Go To Market team that oversee the Stores operation. They need an information from our database and you could help this person to have it by doing a query there. The person requested a list of all the tags that we currently use and how many stores are using each tag. Create a query that allow you to provide this information to the Go To Market team. 

*This is done in the DB administration application of your choice (in this case DBeaver was used).*


Solution: For the realization of this first point, the following query must be created, taking into account that the database is in a .json format and it is also in a PostgreSQL database management system.


-- Inquiry for a list of labels and the number of stores using them:

    

    SELECT
    DISTINCT regexp_split_to_table(data->>'tags', '"?,\s*"?') AS ETIQUETAS,
  
    COUNT(*) AS CONTEO_TIENDAS

    FROM stores
  
    GROUP BY 

    ETIQUETAS; 

![image](https://github.com/esca999/ADDI-CHALLENGE/assets/152576656/08e025dd-564f-4589-a805-40473e8e70b9)


2- We just received a case where the owner of the store with the id 0d4f7a40-651d-44fb-8744-04d9b31ef844 changed to Old-Wolf. They also stopped to sell things related to finanzas and are now working with educacion so they also required a change in their current tags. Since this is urgent we will do that thru a query. Create a query that allow us to do this update in our database.




