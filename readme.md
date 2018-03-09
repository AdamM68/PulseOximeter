# Pulse Oximeter Reader for Android

#### To Use

* Listen too bluetooth scanner service scan result BluetoothScanService.ON_SCAN_RESULT

* Listen too bluetooth scanner service stop event BluetoothScanService.ON_SCAN_RESULT

* Listen to BloodOximeterDevice sercive events by using BloodOximeterDeviceService.ON_EVENT

* Startup the bluetooth scanner service to find any turned on device. In this example the user needs to select the 
scan menu item.
```java
BluetoothScanService.startScan(this);
```
* Once your device is found

* Request the scanner to stop, by calling 
```java
if (scanResult.getDevice().getName() != null && scanResult.getDevice().getName().equals("BerryMed")) {
	Log.d(TAG, "found BerryMed device");
	if ( mDeviceAddress == null || mDeviceAddress.isEmpty()) {
		mDeviceAddress = scanResult.getDevice().getAddress();
		BluetoothScanService.requestStop(MainActivity.this);
	}
}
```

* On the bluetooth scanner service stopping you can then ..

* Start the BloodOximeterService with your found device address:
```java
BloodOximeterDeviceService.requestData(MainActivity.this, mDeviceAddress);
```



