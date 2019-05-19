Api Task
====

You are working at Ingot Portal and you have been tasked with creating a restful api in symfony 4. 

### Part One
To begin, you should create doctrine entities for two database tables:

* Containers
    * container_no (String, 11 characters)
    * gross_weight (Decimal, 3 decimal places)
    * nett_weight (Decimal, 3 decimal places)
    * cube (Decimal, 3 decimal places)
    
* Packages
    * container_id (Many-to-One Relationship to Containers Entity, One Container has many Packages)
    * sku_ref (String, could be up to 30 characters)
    * gross_weight (Decimal, 3 decimal places)
    * nett_weight (Decimal, 3 decimal places)
    * cube (Decimal, 3 decimal places)
    
A restful api should then be created to help create, read, update and delete containers and packages.

Additionally, updating packages weights and/or cube should also update the containers weights/cube to be the total weight/cube of the packages assigned to it.

### Part Two
When containers are being loaded onto a ship, there is likely to be a number of containers with all the same details but different load times. 

We would like you to implement an endpoint to your api which creates a number of containers and sets the load times. 

The endpoint will require the following parameters:
* number_containers - The number of parameters the user wants to create.
* load_date - The load date and time of the first container.
* interval - The interval of the containers being loaded. The possible intervals are (hourly, halfHourly, quarterHourly, custom).
* custom_interval_duration - This will only be used if interval is set to custom. It will be set as a number & either hours or minutes ie. 2 hours.

An example of the parameters could look like below:

```
{
    "number_containers" => 5,
    "load_date" => "01/07/19 15:10",
    "interval" => "custom",
    "custom_interval_duration" => "40 minutes"
}
```

The above example would create five containers with the load dates set to:
```
Container 1 - 01/07/19 15:10
Container 2 - 01/07/19 15:50
Container 3 - 01/07/19 16:30
Container 4 - 01/07/19 17:10
Container 5 - 01/07/19 17:50
```

### Further Requirements
We expect your api to be thoroughly tested. It is your decision which tests you feel is appropriate for the task.

We would like your api endpoints to be documented in [Swagger UI](https://swagger.io/tools/swagger-ui/). This can be done using [Open API](https://swagger.io/docs/specification/about/) or [Api Platform](https://api-platform.com/docs/core/swagger/).

We would also like a markdown file titled readme.md to be created, documenting your thoughts on the task, how you found implementing it and any problems you faced.

If you are unable to complete any part of the task, please still submit your attempt and explain the problems you faced in the readme file.

We do not require a database to be submitted with your project. We will be able to create our own database using your doctrine entities.

When the task has been completed, please create a zip, and send to ``martin.gill@ingotportal.com, lewis.hides@ingotportal.com, andy.roberts@ingotportal.com``