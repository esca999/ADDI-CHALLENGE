# ADDI-CHALLENGE
The function of this repository is to show the step-by-step challenge for the support position.
Before starting the test you must prepare the test environment in this case it is necessary to virtualize a Linux environment in the hypervisor of your choice in this case it was done using VMware, once the virtual machine is deployed you must install the following:

* Have docker installed
* Have docker compose installed
* Have Git installed
* Have Postman installed
* Have Dbeaver

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

* Solution: The consultation was carried out taking into account the stipulations of the previous point.

      Select * from stores where id = '0d4f7a40-651d-44fb-8744-04d9b31ef844';

  This query allows us to list by ID, so we can know where to make the change.

  Then execute this query to replace the requested data: (and repeat the process to replace the tags)

      SELECT 
      replace(data::text, 'Young-Wolf', 'Old Wolf')::jsonb AS ACTUALIZACION
      FROM 
      stores 
      WHERE 
      id = '0d4f7a40-651d-44fb-8744-04d9b31ef844';

Finally, this would be the complete query to update the table with:

    update stores
    set data = replace(data::text, 'finance', 'education')::jsonb
    where id ='0d4f7a40-651d-44fb-8744-04d9b31ef844';


    update stores
    set data = replace(data::text, 'Young-Wolf', 'Old Wolf')::jsonb
    where id ='0d4f7a40-651d-44fb-8744-04d9b31ef844';


![image](https://github.com/esca999/ADDI-CHALLENGE/assets/152576656/373d23db-4c8f-469d-b12b-b6c8cc3191a9)


3- Since we are having a hard time while creating all the store credentials manually thru insert queries we recently received a message from one Software Engineer that build an API that will allow you to create new stores quickly. Currently we don't have system integrated thru this API but we can use it right now. Build an HTTP request to add the store credentials through our API. The id of the store is 1f585fc9-4926-468c-a728-eb34d80e9ea1

Since the credentials used to communicate with our partner are sensitive information, an encryption process must be carried out. This process can be done by making an HTTP request to our API which receives the necessary data and adds the credentials in the stores table. Endpoint documentation can be found attached to this file.

The credentials to add for this new ally are:

    username: aliado_addi
    password: }sxh7_5}BdJ4K:Qf

* Solution: Make the HTTP request through PostMan, taking into account the information provided in the challenge, we already know that the port and ip to which we are going to make the request is: 127.0.0.1:4000.

Information to be considered:
        
        POST /allies/{allyId}/credentials.
        Add communication credentials to an ally.

        Headers: "Content-Type: application/json"

        Parameters:
        allyId(path): identification string of an ally.

    Payload(body): json object, example.
    {
	"username": "addi",
	"password": "123456"
    }

    Responses:
    200: 
    {
	"message": "Credentials added",
	"allyId": "allyId",
	"allyName": "ally name".
    }
    400:
    {
	"message": "ally was not found or request is not successful"
    }
    500:
    {
	"message": "Server error"
    }    

![image](https://github.com/esca999/ADDI-CHALLENGE/assets/152576656/67ced6d7-80b2-4038-94f1-61b429f01617)

Then we repeat the process now with the GET request to verify that we have added the credentials to the requested user (Only deleting the body section for protocol and organization).

![image](https://github.com/esca999/ADDI-CHALLENGE/assets/152576656/b33f066b-0f66-4f55-8c2f-18312dcb470d)

4- After some time people started to complain that their credentials are not working. Probably something happened while other Support Engineers were also using this API. You have access to the server log that have all the previous requests. You should open the log inside the folder log/example.log and find how many requests failed and which are the clients that were impacted.

* Solution:This creates a random event log so we must investigate and perform a filtering to find out which companies were affected by the API bug.

![image](https://github.com/esca999/ADDI-CHALLENGE/assets/152576656/ff37e652-f1e8-40f3-907e-be2b6595714d)

Finally, using Visual Studio Code, we export the event log to perform the search in this case filtering by error 404 and credentials, as these were the companies affected by the API bug

![image](https://github.com/esca999/ADDI-CHALLENGE/assets/152576656/a1448784-3b80-4c16-8dfa-d2c8532f14a7)



Then we copy it to a notes blog to deliver the final filtering and be able to see it in a more organized way, if you want to copy it to another file within VSC.

