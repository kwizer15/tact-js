# tact-js
Library for bHaptics Haptic Devices

### Prerequisite
bHaptics Player has to be installed (window)


### Examples
* https://elated-noyce-f0332a.netlify.com/

or 

* Open samples/simple/index.html directory in browser (Example code)


### How to setup

You can import the generated bundle to use the whole library generated by this starter:

```javascript
import tactJs from 'tact-js'

tactJs.submit();
```

Additionally, you can import the transpiled modules from `dist/lib` in case you have a modular library:

```javascript
tactJs.addListener(function(msg) {
    if (msg.status === 'Connected') {
        console.log('connected');
    }
});
```


### How to use
1. Dot Mode - submitDot()

* Parameters
  * key: string;
  * position: 'VestFront' | 'VestBack' | 'Head' | 'ForearmL' | 'ForearmR'
  * points: array of object with (index, intensity)
      * index: [0, 19]
      * intensity: [1, 100] 
  * durationMillis: [50, 10000]

* Return Type: ErrorCode

```javascript
var key = 'dot';
var position = 'VestFront'
var points = [{
    index : 10,
    intensity : 100
}];
var durationMillis = 1000; // 1000ms
var errorCode = tactJs.submitDot(key, position, points, durationMillis);
```

2. PathMode - submitPath()

* Parameters
  * key: string;
  * position: 'VestFront' | 'VestBack' | 'Head' | 'ForearmL' | 'ForearmR'
  * points: array of object with (x, y, intensity)
      * x: [0, 1]
      * y: [0, 1]
      * intensity: [1, 100] 
  * durationMillis: [50, 10000]
  
* Return Type: ErrorCode
  
* Example
```javascript
var key = 'dot';
var position = 'VestFront'
var points = [{
    x : 0.5,
    y : 0.5,
    intensity : 100
}];
var durationMillis = 1000; // 1000ms
var errorCode = tactJs.submitPath(key, position, points, durationMillis);
```


3.1. Tact File - submitRegistered()

* Parameters
  * key: string;
  
* Return Type: ErrorCode

* Example
```javascript
var errorCode = tactJs.submitRegistered(key);
```

3.2. Tact File - submitRegisteredWithRotationOption()

* Parameters
  * key: string;
  * object with (offsetAngleX, offsetY)
     * offsetAngleX: [0, 360]
     * offsetY: [-0.5, 0.5]
 
* Return Type: ErrorCode
 
* Example
```javascript
var key = 'key';
var rotationOption = {offsetAngleX: 180, offsetY: 0.2};
var errorCode = tactJs.submitRegisteredWithRotationOption(key, rotationOption);
```

### Error Code
* 0: SUCCESS
* 1: MESSAGE_NOT_DEFINED - Check if parameter is wrong or not 
* 2: CONNECTION_NOT_ESTABLISHED - Check if the bhaptics player is running or not
* 3: FAILED_TO_SEND_MESSAGE - Check if there is problem on sending message to the bhpatics player
* 4: MESSAGE_INVALID - Unknown Message Error
* 5: MESSAGE_INVALID_DURATION_MILLIS - durationMillis [10ms~100,000ms]
* 6: MESSAGE_INVALID_INDEX - index should be [0, 19]
* 7: MESSAGE_INVALID_INTENSITY - intensity should be [0, 100]
* 8: MESSAGE_INVALID_X -  x should be [0, 1]
* 9: MESSAGE_INVALID_Y - y should be [0, 1]
* 10: MESSAGE_INVALID_ROTATION_X - rotationOffsetX should be [0, 360]
* 11: MESSAGE_INVALID_ROTATION_Y - offsetY should be [-0.5, 0.5]
