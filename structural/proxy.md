# Flyweight Pattern

A proxy is an object that can be used to control access to another object.

A proxy can be instantiated in place of this real subject and allow it to be accessed remotely. It can also delay
instantiation of the real subject until it is actually needed; this is especially useful if the real subject takes a long time to initialize, or is too large to keep in memory when it isn’t needed. Proxies can be very helpful when dealing with classes that are slow to load data to a user interface.

## Diagram
![proxy diagram](http://www.dofactory.com/images/diagrams/javascript/javascript-proxy.jpg)

### Benefits
- can be used to control access to another object
- useful for implementing caching mechanism

### Implementation

```javascript
function GeoCoder() {
 
    this.getLatLng = function(address) {
        
        if (address === "Amsterdam") {
            return "52.3700° N, 4.8900° E";
        } else if (address === "London") {
            return "51.5171° N, 0.1062° W";
        } else if (address === "Paris") {
            return "48.8742° N, 2.3470° E";
        } else if (address === "Berlin") {
            return "52.5233° N, 13.4127° E";
        } else {
            return "";
        }
    };
}
 
function GeoProxy() {
    var geocoder = new GeoCoder();
    var geocache = {};
 
    return {
        getLatLng: function(address) {
            if (!geocache[address]) {
                geocache[address] = geocoder.getLatLng(address);
            }
            log.add(address + ": " + geocache[address]);
            return geocache[address];
        },
        getCount: function() {
            var count = 0;
            for (var code in geocache) { count++; }
            return count;
        }
    };
};
 
// log helper
 
var log = (function() {
    var log = "";
 
    return {
        add: function(msg) { log += msg + "\n"; },
        show: function() { alert(log); log = ""; }
    }
})();
 
function run() {
    var geo = new GeoProxy();
 
    // geolocation requests
 
    geo.getLatLng("Paris");
    geo.getLatLng("London");
    geo.getLatLng("London");
    geo.getLatLng("London");
    geo.getLatLng("London");
    geo.getLatLng("Amsterdam");
    geo.getLatLng("Amsterdam");
    geo.getLatLng("Amsterdam");
    geo.getLatLng("Amsterdam");
    geo.getLatLng("London");
    geo.getLatLng("London");
 
    log.add("\nCache size: " + geo.getCount());
    log.show();
}
```

# References
- [dofactory](http://www.dofactory.com/javascript/proxy-design-pattern)