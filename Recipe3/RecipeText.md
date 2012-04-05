# Recipe
Doing a location search using Google Maps.

# Solution

The location to be searched can be entered into an EditText. The query is searched and the search results are extracted. The best out of the location search results is displayed as a toast (This is a sample, many other activities can be done using the location search result).

# Discussion

This method obtains text from an EditText named: addressText. Then this text is searched for using the getFromLocationName() method of the Geocoder class. From the search results obtained the first result is extracted and displayed as a Toast. If the string returned is of size=0, an appropriate message is displayed. 

# Solution

The location to be searched can be entered into an EditText. The query is searched and the search results are extracted. The best out of the location search results is displayed as a toast (This is a sample, many other activities can be done using the location search result).
Discussion

This method obtains text from an EditText named: addressText. Then this text is searched for using the getFromLocationName() method of the Geocoder class. From the search results obtained the first result is extracted and displayed as a Toast. If the string returned is of size=0, an appropriate message is displayed.

'''java
protected void mapCurrentAddress() {
	  String addressString = addressText.getText().toString();
	  Geocoder g = new Geocoder(this);
	  List<Address> addresses;
	  try {
	  
	      addresses = g.getFromLocationName(addressString, 1);
	      String add = "";
	      if (addresses.size() > 0) {

	      	 address = addresses.get(0);
		 for (int i=0; i<address.getMaxAddressLineIndex();i++)
		     add += address.getAddressLine(i) + "\n";
		 Toast.makeText(getBaseContext(), add, Toast.LENGTH_SH	ORT).show();
	      } 
	      else
		   Toast.makeText(getBaseContext(),"We failed to locate this address.", Toast.LENGTH_SHORT).show();
           } catch (IOException e)
	           e.printStackTrace();

}
'''
