Simple Shipment
====

As a user I want to be able to edit shipments. I would like to view a list shipments in a grid with the following columns, each column must be sortable.


* Shipment Reference (ID)
* Shipper
* PO Reference
* Port of Loading
* Port of Discharge 
* Carrier
* ETA

I want to click a hyperlink on each shipment reference to show a shipment page (as per UI mockup) and be able to edit any shipment field. All shipment fields can be saved, apart from the shipment reference which cannot be changed.

![UI Mockup](https://s3-eu-west-1.amazonaws.com/warrant-group-files/training/SimpleShipment+Mock+UI.png "UI Mockup")

Requirements
---

* Must use [AngularJS 1.x](https://angularjs.org)
* Must use [Bootstrap 3.x](http://getbootstrap.com)
* Must use [Kendo UI for JQuery](http://demos.telerik.com/kendo-ui/grid/angular) datagrid
* Must interact with a [RESTful server](https://github.com/typicode/json-server) (GET, PUT)
* Optionally use AngularJS [ngRoute](https://docs.angularjs.org/api/ngRoute) for routing, and [ngResource](https://docs.angularjs.org/api/ngResource/service/$resource) to interact with RESTful server  
* All dates must be formatted to dd-mm-yyyy

A [skeleton AngularJS application](app) is included with all dependencies and libraries.

### Installation

You will need to install NodeJS, Git and clone the [training repository](https://github.com/warrantgroup/training). Grunt (Task Runner) will automatically start a HTTP web server on [http://localhost:8000](http://localhost:8000), and RESTful API on [http://localhost:3000/shipments](http://localhost:3000/shipments) depending on port availability.

* Install [NodeJS](https://nodejs.org/en/download)
* Install [Git](https://git-scm.com/downloads)
* Run ``git clone https://github.com/warrantgroup/training.git && cd training/SimpleShipment``
* Run ``npm install``
* Run ``grunt``

If grunt is not found, please run ``npm install -g grunt-cli`` to install grunt-cli globally.

### Finished

When the exercise has been completed, please create a zip, ignoring node_modules directory (as below) and send to ``martin.gill@ingotportal.com, lewis.hides@ingotportal.com, andy.roberts@ingotportal.com``

``
zip -r9 SimpleShipment.zip SimpleShipment/* -x "*/\node_modules/*"
``

### Notes

Please note Angular now uses semantic versioning, therefore the name AngularJS will refer to version 1.x, while Angular refers to any version 2.x and above.  
Please ignore “Kendo for Angular” which refers to Angular version (2.x).  
Shipment `ID` and `reference` are interchangeable.
