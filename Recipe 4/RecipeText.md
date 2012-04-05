# Recipe Title
Creating a Custom Tabbed Dialog

# Problem
The application requires a Dialog-like structure in place of a full-fledged activity to show some information. But the information has to be arranged into categories for it to be easier on the grasp.

# Solution
Creating a Custom Dialog with Tabs. These Tabs within the dialog would allow categories of information. Since everything can be squeezed into a Dialog in place of an entire activity, the application has seems more compact.

# Discussion: 

Custom Dialog Class should extend 'Custom Dialog':
```java
	public class CustomDialog extends Dialog
```

Following lines of code need to be added to the 'customDialog' class:

```
        setTitle("Dialog Title");
        setContentView(R.layout.custom_dialog_layout);
        //On Click listeners for the buttons present in the Dialog
        Button button1 = (Button) findViewById(R.id.button1);
        Button button2 = (Button) findViewById(R.id.button2);
        button1.setOnClickListener(new View.OnClickListener() {
            
            @Override
            public void onClick(View v) {
                dismiss(); //to dismiss the Dialog
            }
        });

		button2.setOnClickListener(new View.OnClickListener() {
            
            @Override
            public void onClick(View v) {
            	//Fire an intent on click of this button
				Intent showQuickInfo = new Intent("com.android.oreilly.QuickInfo");
                showQuickInfo.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
                context.startActivity(showQuickInfo);
            }
        });
```

The XML code in the layout file (present in /res/layout) custom_dialog_layout :

The entire code is enclosed with a linear layout. Within the LinearLayout, a Relative Layout is used to position 2 buttons (which could be denote different options like 'Login' and 'Vote up' etc). Then below the Relative layout, another Relative Layout containing a scroll view is present. 

'android_button' and 'thumbsup' are the names of images in /res/drawable.

```xml
<LinearLayout
        android:orientation="vertical"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:padding="5dp">
        
	 <RelativeLayout
	     android:layout_width="fill_parent"
	     android:layout_height="wrap_content"
	     android:paddingBottom="10dip">
	            <Button
			        android:id="@+id/button1"
			        android:background="@drawable/android_button"
					android:layout_height="80dip"
					android:layout_width="80dip"
					android:layout_alignParentLeft="true" 
					android:layout_marginLeft="10dip"  
					android:gravity="center"/>
					
				<Button
			        android:id="@+id/button2"
			        android:background="@drawable/thumbsup"
			        android:layout_height="80dip"
					android:layout_width="80dip"
					android:layout_alignParentRight="true"
					android:layout_marginRight="10dip"
					android:gravity="center"/>
		</RelativeLayout>	
        
         <RelativeLayout
	     android:layout_width="fill_parent"
	     android:layout_height="wrap_content"
	     android:paddingBottom="10dip">
	     
		       <ScrollView android:id="@+id/ScrollView01"
			       android:layout_width="wrap_content" 
			       android:layout_height="200px">
		       
			       <TextView 
				       android:id="@+id/TextView01"
				       android:text="@string/lorem"
				       android:layout_width="wrap_content" 
				       android:layout_height="wrap_content"
				       android:gravity="center_horizontal"
				       android:paddingLeft="15dip"
				       android:paddingTop="15dip"
				       android:paddingRight="20dip"
				       android:paddingBottom="15dip"/>

		    	</ScrollView>
      </RelativeLayout>
</LinearLayout>
```