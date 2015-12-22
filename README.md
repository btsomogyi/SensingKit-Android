# SensingKit-Android Library

An Android library that provides Continuous Sensing functionality to your applications. For more information, please refer to the [project website](http://www.sensingkit.org).


## Supported Sensors

The following sensor modules are currently supported in SensingKit-Android, (listed in [SKSensorModuleType](SensingKitLib/src/main/java/org/sensingkit/sensingkitlib/SKSensorModuleType.java) enum):

- Accelerometer
- Gravity
- Linear Acceleration
- Gyroscope
- Rotation
- Magnetometer
- Ambient Temperature
- Step Detector
- Step Counter
- Light
- Location
- Activity
- Battery
- Screen Status
- Audio Recorder
- Audio Level
- Bluetooth
- Humidity
- Air Pressure

## Configuring the Library

- Build the library using the command:

```
./gradlew build
```

- Create an app/libs directory inside your project and copy the generated SensingKitLib/build/outputs/aar/SensingKitLib-release.aar (or the equivalent debug) file there.

- Edit your app/build.gradle file and add a flatDir entry as shown bellow:

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
}
```


- In the same app/build.gradle file, add SensingKitLib as a dependency as shown below:

```
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'org.sensingkit:SensingKitLib-release@aar'
    compile 'com.android.support:appcompat-v7:23.0.0’
    compile 'com.google.android.gms:play-services-location:7.8.0'
}
```


## How to Use this Library

- The imports you will need are:

```java
import org.sensingkit.sensingkitlib.SKException;
import org.sensingkit.sensingkitlib.SKSensorType;
import org.sensingkit.sensingkitlib.SensingKitLib;
import org.sensingkit.sensingkitlib.SensingKitLibInterface;  //Document:  needed to add this to init SensingKit
import org.sensingkit.sensingkitlib.data.SKSensorData;
import org.sensingkit.sensingkitlib.SKSensorDataListener;
```

- Init SensingKit in your Activity class as shown below:

```java
//You will need a try..catch block around this code
SensingKitLibInterface mSensingKitLib = SensingKitLib.getSensingKitLib(this);
```


- Register a sensor module (e.g. a Light sensor) as shown below:

```java
//You will need a try..catch block around this code
mSensingKitLib.registerSensor(SKSensorType.LIGHT);
```


- Subscribe a sensor data listener:

```java
//You will need a try..catch block around this code
mSensingKitLib.subscribeSensorDataListener(SKSensorType.LIGHT, new SKSensorDataListener() {
    @Override
    public void onDataReceived(final SKSensorType moduleType, final SKSensorData sensorData) {
        System.out.println(sensorData.getDataInCSV());  // Print data in CSV format
    }
});
```


- You can cast the data object into the actual sensor data object in order to access all the sensor data properties:
 
```java
SKLightData lightData = (SKLightData)sensorData;
```



- You can Start and Stop the Continuous Sensing using the following commands:

```java
//You will need try..catch blocks around these statements
mSensingKitLib.startContinuousSensingWithSensor(SKSensorType.LIGHT);
mSensingKitLib.stopContinuousSensingWithSensor(SKSensorType.LIGHT);
```


For a complete description of our API, please refer to the [project website](http://www.sensingkit.org).

## License

```
Copyright (c) 2014. Queen Mary University of London
Kleomenis Katevas, k.katevas@qmul.ac.uk.

This file is part of SensingKit-Android library.
For more information, please visit http://www.sensingkit.org.

SensingKit-Android is free software: you can redistribute it and/or modify
it under the terms of the GNU Lesser General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

SensingKit-Android is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License
along with SensingKit-Android.  If not, see <http://www.gnu.org/licenses/>.
```

This library is available under the GNU Lesser General Public License 3.0, allowing to use the library in your applications.

If you want to help with the open source project, contact hello@sensingkit.org.
