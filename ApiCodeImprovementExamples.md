Api Code Review Task
====

You are working at Ingot Portal and you have been tasked with reviewing pull requests. You come across the following code samples. 

Please review each coding sample and write up a review of the code. Please indicate where small improvements could be made or feel free to rewrite the whole function where necessary.


###Sample One

The purpose of this function is to get the next available delivery date for cargo to the warehouse.
The function accepts three parameters:
* $loadDate - The date the cargo is loaded onto the lorry.
* $transitTime - The time it takes to get from the dock to the warehouse. 

The function returns the delivery date.

It should be noted, the warehouse will not be open on Saturday or Sunday so the delivery date cannot fall on those days.

```
private function getNextAvailableDeliveryDate($loadDate, $transitTime)
    {
        $counter = 0;

        $deliveryDate = clone $loadDate;

        while(true) {
            if(in_array(date_format($deliveryDate, 'N'), array(1, 2, 3, 4, 5)){
                break;
            }
            else {
                if((int) date_format($eta, 'N') != 6 and (int) date_format($eta, 'N') != 7){
                    $counter++;
                }
            }
        }

        $calc = $transitTime + $counter;

        date_add($deliveryDate, date_interval_create_from_date_string('+ ' . $calc . ' days'));

        return $deliveryDate;
    }
```

###Sample Two

Below, we have two functions. One is to add packages to containers. The other is to update packages which are attached to containers. Both functions need to update the container weights to the total weights of the packages within the container. What do you think to these classes? Could they be improved in any way?

```

public function post(Container $container, $params) {
    $package = $this->packageRepository->create($params);
    
    $totalGrossWeight = 0;
    $totalNetWight = 0;
    $totalCube = 0;
    
    foreach ($container->getPackages() as $containerPackage) {
        $totalGrossWeight = $totalGrossWeight + $containerPackage->getGrossWeight();
        $totalNetWight = $totalNetWeight + $containerPackage->getNetWeight();
        $totalCube = $totalCube + $containerPackage->getCube();
    }
    
    $container->setGrossWeight($totalGrossWeight);
    $container->setNetWeight($totalNetWeight);
    $container->setCube($totalCube);
    
    $this->containerRepository->save($container);
    
    return $package;
}

public function patch (Container $container, Package $package, $params) {
    $package = $this->packageRepository->update($params);
    
    $totalGrossWeight = 0;
    $totalNetWight = 0;
    $totalCube = 0;
    
    foreach ($container->getPackages() as $containerPackage) {
        $totalGrossWeight = $totalGrossWeight + $containerPackage->getGrossWeight();
        $totalNetWight = $totalNetWeight + $containerPackage->getNetWeight();
        $totalCube = $totalCube + $containerPackage->getCube();
    }
    
    $container->setGrossWeight($totalGrossWeight);
    $container->setNetWeight($totalNetWeight);
    $container->setCube($totalCube);
    
    $this->containerRepository->save($container);
    
    return $package;
}

```


###Sample Three

Below, we have three classes. One for vessels, one for planes and one for hauliers. What do you think to these classes? Could they be improved in any way?

```
class Vessel {
    public $id;
    public $name;
    public $code;
    public $flag;
    public $tonnage;
}

class Plane {
    public $id;
    public $name;
    public $code;
}

class Haulier {
    public $id;
    public $name;
    public $code;
    public $address;
    public $phone;
    public $fax;
}

```

###Sample Four

Below, we have a function which accepts a party id and returns a validator class. Each party have different requirements so need different validators.

```
 public function getPartyValidator($partyId) 
    {
        if ($partyId == 1) {
            return PartyOneValidator();
        } else if ($partyId == 2) {
            return PartyTwoValidator();
        } else if ($partyId == 3) {
            return PartyThreeValidator();
        } else if ($partyId == 4) {
            return PartyFourValidator();
        } else if ($partyId == 5) {
            return PartyFiveValidator();
        } else if ($partyId == 6) {
            return PartySixValidator();
        } else if ($partyId == 7) {
            return PartySevenValidator();
        } else if ($partyId == 8) {
            return PartyEightValidator();
        } else if ($partyId == 9) {
            return PartyNineValidator();
        } else {
            return NULL;
        }
    }
```

###Sample Five

Below, we have a controller function for patching a shipment. If the eta of the shipment is updated, the change will need to be logged and an email sent out to everyone who is subscribed to change of eta notifications. 

```
 public function patchShipmentAction(Request $request, $id)
    {
        $params = $this->getRequestParams($request);

        try {
            $shipment = $this->getOr404($id);
            
            if ($params['eta']) {
                if ($params['eta'] != $shipment->getEta() {
                    //Log change of eta in eta history log table
                    $log = new EtaHistoryLog();
                    $log->setPreviousEta($shipment->getEta());
                    $log->setEta($params['eta'];
                    $log->setShipment($shipment);
                    
                    //Find people subscribed to change of eta notifications
                    $sql = $this->getContainer()->get('doctrine')->prepare("SELECT * from notifications WHERE notifications.notification_type_id = ?");
                    
                    //eta_change notification id is 5;
                    $sql->execute(array(5));
                    $notifications = $sql->fetchAll();
                    
                    foreach ($notifications as $notification){
                        $emailAddress = $notification['emailAddress'];
                        $emailBody = $this->get(ingot_api.email.handler)->getEtaChangedEmailBody;
                        
                        $message = \Swift_Message::newInstance()
                            ->setSubject('Eta Changed')
                            ->setContentType('text/html')
                            ->setFrom('noreply@ingotportal.com')
                            ->setTo($emailAddress)
                            ->setBody($emailBody);
                            
                        $this->get('mailer')->send($message)
                    }
                }
            }
                       
            $shipment = $this->get('ingot_api.shipment.handler')->patch($shipment, $params);

            $routeOptions = array(
                'id' => $shipment->getId(),
                '_format' => $request->get('_format')
            );

            return $this->routeRedirectView('api_1_get_shipment', $routeOptions, Response::HTTP_NO_CONTENT);

        } catch (InvalidFormException $exception) {
            return $this->view($exception->getForm(), 400);
        }
    }

```

###Bonus Task

When containers are being loaded onto a ship, there is likely to be a number of containers with all the same details but different load times. 

For an additional bonus task, we would like you to write a class that accepts an array, creates a number of containers and sets the load times. The array will consist of four parameters:
* number_containers - The number of parameters the user wants to create. Just writing new Container() for each is acceptable.
* load_date - The load date and time of the first container.
* interval - The interval of the containers being loaded. The three possible intervals are (hourly, halfHourly, quarterHourly, custom).
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