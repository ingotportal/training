# Pickup Problem

A customer has asked you to build a simple warehouse system as a REST API to manage containers that are picked up by hauliers from their warehouse for UK Export.

The customer wants to allow nominated freight forwarders access to the REST API to provide haulier, container type and pickup date inadvance while warehouse staff will update the container number and weight after pickup has occurred.

### Information

You are free to use any PHP libraries or modules in order to complete the challenge. You may choose either MySQL (recommended), MariaDB or MongoDB as your data layer.

**The challenge must be completed using [Symfony Framework 4.x](https://symfony.com/download)**

#### Bonus Points

* Use PHPUnit, Codeception or Behat for your unit tests
* Use Swagger for API documentation

### Requirements

* List all pickups
* Create a single pickup
* Create multiple pickups for a pre-defined number of containers and interval in minutes ie: hourly, half hourly, quarter-hourly
* Update pickup with container number and weight
* Delete pickup

### Authentication

Only authenticated users can create, update or delete a pickup. No authentication is required to retrieve or list.

### Data

* All pickups must have timestamp fields (created_at, modified_at)
* Container number must be valid [ISO 6346](https://www.containercontainer.com/ISO6346) identifier
* Container type must be valid [ISO 6346](https://www.containercontainer.com/ISO6346) code
* Pickup Date must be valid [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date-time

| name | required |
|-----------|---------|
| Customer | yes |
| Warehouse | yes |
| Haulier | yes      |
| Pickup Date | yes |
| Container Number | no |
| Container Type | yes |
| Container Weight | no |

Example seed data has been provided in [pickups.json](pickups.json) and ISO container size and type in [iso-container-types.csv](iso-container-types.csv)

### Finished

When the challenge has been completed, please create a zip, ignoring vendor directory (as below) and send to hello@ingotportal.com

```
zip -r9 PickupProblem.zip PickupProblem/* -x "*/\vendor/*"
```

For full transparency, the coding challenge will be scored according to the following:

* REST architectural style
* Ability to understand requirements
* Use of Symfony Framework
* Use of services, controllers, and models
* Object oriented practices
* Unit testing

