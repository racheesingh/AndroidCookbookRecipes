#Recipe Title
Creating Overlays for a mapView

# Problem
Demarcating a point on a google map using an image.

# Solution
Use the concept of Map Overlays.

#Discussion

Creating one's own map pverlay is a 2 step process:
1. Extend the Overlay class and implement the required functionality (the type and characteristics of the overlay) in that class.
2. Another class which controls that google map on the screen then instantiates the class that extends Overlay. 

```java
public class AddressOverlay extends Overlay
```
 
 Constructor Initialization in the AddressOverlay class:

```java 
 public AddressOverlay(Context context, Address address, int drawable) {
    super();
    this.context=context;
    this.drawable=drawable;
    assert(null != address);
    this.setAddress(address);
    Double convertedLongitude = address.getLongitude() * 1E6;
    Double convertedLatitude = address.getLatitude() * 1E6;
    
    setGeopoint(new GeoPoint( convertedLatitude.intValue(),
			     convertedLongitude.intValue() ) );
}
```
 
 The draw() method of the Overlay class has to be overriden.
 
```java 
@Override
public boolean draw(Canvas canvas, MapView mapView, boolean shadow, long when) {
    super.draw(canvas, mapView, shadow);
    Point locationPoint = new Point();
    Projection projection = mapView.getProjection();
    projection.toPixels(getGeopoint(), locationPoint);
    
    // Reading the image
    Bitmap markerImage = BitmapFactory.decodeResource(context.getResources(), drawable);
    
    // Drawing the image, keeping the center of the image at the address's location
    canvas.drawBitmap(markerImage,locationPoint.x - markerImage.getWidth() / 2, locationPoint.y - markerImage.getHeight() / 2, null);
    return true;
}
```   

In the java class that is implementing the map View's function, the following lines of code are added to add an Overlay on the map:

```java
List<Overlay> mapOverlays = mapView.getOverlays();
//Instantiating the AddressOverlay class we just defined
//'androidmarker is the name of the image that you wish to place on the map
AddressOverlay addressOverlay = new AddressOverlay(this, address, R.drawable.androidmarker); 
//adding the overlay to the map
mapOverlays.add(addressOverlay);
mapView.invalidate();
```
