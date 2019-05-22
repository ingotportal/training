# Pickup Problem

A customer has asked you to build a simple warehouse system as a REST API to manage containers that are picked up by truck from their warehouse for UK Export.

The customers warehouse will know the haulier and pickup date inadvance from freight forwarder and record the container number and weight after departure.

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
* Container number must be ISO 6364 standard
* Pickup Date must be ISO 8601 standard

| name | required |
|-----------|---------|
| Customer | yes |
| Warehouse | yes |
| Haulier | yes      |
| Pickup Date | yes |
| Container Number | no |
| Container Weight | no |

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
