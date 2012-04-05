# Recipe Title
To Add Device's current location to Google Maps

# Problem
Adding Current location of the device on Google maps.

# Solution
Using MyLocationOverlay class, current location of the device can be depicted on the Map.

#Discussion

Add the following permissions to the Android Manifest File:

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```

Adding a mapView to your application, these few lines of code should be present in the XML layout. 
The Id of the map view is 'map'.

```xml
	<com.google.android.maps.MapView
		android:id="@+id/map"
 		android:layout_width="fill_parent"
 		android:layout_height="wrap_content"
		android:layout_below="@id/map_location_button"
		android:layout_above="@+id/use_this_location_button"
 		android:clickable="true"
 		android:apiKey = "Your Key Should be placed here"/>
```

In the Java class for the activity which displays the map View, add a field:

```java
private MyLocationOverlay myLocationOverlay;
```

Also, get a handle to the map view defined in the XML and add a MyLocationOverlay. After that call the invalidate() method. 

```java
mapView = (MapView)findViewById(R.id.map);
myLocationOverlay = new MyLocationOverlay(this, mapView);
mapView.getOverlays().add(myLocationOverlay);
mapView.invalidate();
```

To prevent depletion of battery, in the onPause method of the class, disableMyLocation() method should be called. 

```java
@Override
protected void onPause() {
    super.onPause();
    myLocationOverlay.disableMyLocation();
}

@Override
protected void onResume() {
    super.onResume();
    myLocationOverlay.enableMyLocation();
}
