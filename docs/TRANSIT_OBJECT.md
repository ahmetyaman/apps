# Transit Object

On players that run a Transit Adapter APK, OnSign TV players inject a Javascript object, named `transit` into all running Apps, which is accessible via the Window object.

This object contains information regarding the vehicle and routes, which are needed to build public transit Apps.

> Please, note that the `transit` object is not available on all platforms, during app previewing or app thumbnailing. Therefore, all uses need to be protected with the standard `try {} catch {}`.

### Transit Object Model:

```javascript
  {
  "last_update": 1541691472,
  "provider": "provider_id",
  "version": 1,
  "vehicle": {
    "id": "bus_322",
    "apc_count": 12,
    "operator_id": "Jones",
    "stop_requested": true,
    "heading": 45,
    "speed": 80,
    "coordinates": {
      "lat": 32.7157,
      "long": 117.1611
    }
  },
  "trip": {
    "id": "t3B8d-sl17-p173-r86D",
    "label": "Central Station",
    "route_id": 1234,
    "route_short_name": "12",
    "route_long_name": "Highland Avenue",
    "deviation": 65
  }
}
```

## Transit Object API

The following methods are available on the `transit` object:

  * [`transit.getData(name)`](#getData)
  * [`transit.addEventListener(event, func)`](#addEventListener)
  * [`transit.removeEventListener(event)`](#removeEventListener)

**Note: this object can be expanded in the future to contain other types of information.**

***
#### <a name="getData"></a>transit.getData(name)
> **Requires: Android Player 9.3.X**

Returns the correspondent value of transit object model, specified by key `name`.

An empty query like `transit.getData('')` returns the entire transit object model.

Example:

```javascript
  // In the example below, it is important to wrap the code using a try/catch statement since the transit object might not be available;
  try {
    // Get entire transit object model representation from transit object.
    var transitObject = transit.getData('');
    // Log entire transit object:
    console.log(transitObject);
    // Log the trip object:
    console.log(transitObject.trip);
  } catch (ex) {
    console.error('Transit object not available');
  }
```

Also, values can be accessed separately, for example:

* `vehicle.id`
* `vehicle.coordinates`
* `trip.route_id`
* `trip.route_long_name`

Example:

```javascript
  // In the example below, it is important to wrap the code using a try/catch statement since the transit object might not be available;
  try {
    // Get an object representing the `vehicle` data from the transit object.
    var vehicle = transit.getData('vehicle.id');
    // Log the vehicle id:
    console.log(vehicle.id);
    // Get an string representing the `route_long_name` data from the transit.trip object.
    var trip_route_long_name = transit.getData('trip.route_long_name');
    // Log the trip route long name:
    console.log(trip_route_long_name);
  } catch (ex) {
    console.error('Transit object not available');
  }
```

***
#### <a name="addEventListener"></a>transit.addEventListener(event, func)
> **Requires: Android Player 9.3.X**

Adds an event listener to observe data changes for an specific value of transit model. When data for type `event` changes, the correspondent function `func` will be called.

Example:

```javascript
  // In the example below, it is important to wrap the code using a try/catch statement since the transit object might not be available;
  try {
   console.log('Add event listener for vehicle.coordinates:') 
   f = function(key,value){ console.log(key, value); }
   transit.addEventListener('vehicle.coordinates', f);
  } catch (ex) {
    console.error('Transit object not available');
  }
```

***
#### <a name="removeEventListener"></a>transit.removeEventListener(event)
> **Requires: Android Player 9.3.X**

Removes an associated event listener of type `event` that was previously added.

Example:

```javascript
  // In the example below, it is important to wrap the code using a try/catch statement since the transit object might not be available;
  try {
    console.log('Remove event listener for vehicle.coordinates');
  transit.removeEventListener('vehicle.coordinates'));
  } catch (ex) {
    console.error('Transit object not available');
  }
```
