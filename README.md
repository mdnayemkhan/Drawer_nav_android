# Drawer Navigation Android app

Set up Drawer Navigation in your android app

## xml code
>Step 1.Replace the code on your main_activity.xml file:
```
 <?xml version="1.0" encoding="utf-8"?>
<androidx.drawerlayout.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/drawer_layout"
    tools:context=".MainActivity">

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        >
        <LinearLayout
            android:id="@+id/appBar"
            android:layout_width="match_parent"
            android:layout_height="?actionBarSize"
            android:background="?attr/colorPrimary"
            android:gravity="center_horizontal"
            android:orientation="horizontal"
            android:paddingStart="15dp"
            android:paddingEnd="15dp"
            android:visibility="visible">

            <ImageView
                android:id="@+id/imageMenu"
                android:layout_width="30dp"
                android:layout_height="30dp"
                android:layout_gravity="center"
                android:src="@drawable/ic_menu"
                app:tint="#FFFFFF" />

            <TextView
                android:id="@+id/textTitle"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_gravity="center"
                android:layout_marginLeft="15dp"
                android:text="@string/app_name"
                android:textColor="@color/white"
                android:textSize="18sp"
                android:textStyle="bold" />

        </LinearLayout>
        
    </RelativeLayout>


    <com.google.android.material.navigation.NavigationView
        android:id="@+id/nav_View"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        app:headerLayout="@layout/drawar_top_layout"
        app:menu="@menu/navigation_menu" />

</androidx.drawerlayout.widget.DrawerLayout>
      
```
## Menu
>Step 2.Creat "menu" Directroy res folder and create menu Resorces file "navigation_menu" and Replace the code here:
```
 <?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">

    <group
        android:id="@+id/group1"
        android:checkableBehavior="single">
        <item android:title="Menu">
            <menu>
                <item
                    android:id="@+id/menuHome"
                    android:icon="@drawable/ic_home"
                    android:title="Home" />
                <item
                    android:id="@+id/menuShare"
                    android:icon="@drawable/ic_share"
                    android:title="Share" />
                <item
                    android:id="@+id/menuRate"
                    android:icon="@drawable/ic_rate"
                    android:title="Rate app" />
            </menu>
        </item>
    </group>

    <group
        android:id="@+id/group2"
        android:checkableBehavior="single">
        <item android:title="More App">
            <menu>
                <item
                    android:id="@+id/menushareapp"
                    android:icon="@drawable/ic_share"
                    android:title="Share App" />
                <item
                    android:id="@+id/menuprivacy"
                    android:icon="@drawable/ic_privacy"
                    android:title="Privacy Policy" />
            </menu>
        </item>
    </group> 
</menu>
 
```
## Drawar Top Layout
>Step 3.creat a "drawar_top_layout" in your res>layout derectory and Replace the code:
```
        <?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:app="http://schemas.android.com/apk/res-auto">

    <LinearLayout
        android:layout_marginBottom="15dp"
        android:layout_marginTop="25dp"
        android:id="@+id/drawarHeader"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        >
        <ImageView
            android:layout_marginLeft="10dp"
            android:layout_width="100dp"
            android:layout_height="100dp"
            android:src="@mipmap/ic_launcher"
            />
        <LinearLayout
            android:layout_gravity="center"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical"
            >
            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textColor="?attr/colorPrimary"
                android:textStyle="bold"
                android:text="@string/app_name"
                android:layout_marginLeft="10dp"
                android:textSize="20sp"
                />
            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textColor="#AE000000"
                android:text="@string/app_name"
                android:layout_marginLeft="10dp"
                android:textSize="18sp"
                />
        </LinearLayout>
    </LinearLayout>
    <View
        android:elevation="5dp"
        android:layout_below="@id/drawarHeader"
        android:layout_width="match_parent"
        android:layout_height="2dp"
        android:background="#43000000"
        />
</RelativeLayout>
```
 ## Java 
  >Step 4.Reples this code on your MainActivity.java:
```
  public class MainActivity extends AppCompatActivity {

    DrawerLayout drawerLayout;
    NavigationView navigationView;
    ActionBarDrawerToggle toggle;

    ImageView imageMenu;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Navagation Drawar------------------------------
        drawerLayout = findViewById(R.id.drawer_layout);
        navigationView = findViewById(R.id.nav_View);
        imageMenu = findViewById(R.id.imageMenu);

        toggle = new ActionBarDrawerToggle(MainActivity.this, drawerLayout, R.string.open, R.string.close);
        drawerLayout.addDrawerListener(toggle);
        toggle.syncState();
        //getSupportActionBar().setDisplayHomeAsUpEnabled(true);

        // Drawar click event
        // Drawer item Click event ------
        navigationView.setNavigationItemSelectedListener(new NavigationView.OnNavigationItemSelectedListener() {
            @Override
            public boolean onNavigationItemSelected(@NonNull MenuItem item) {

                switch (item.getItemId()) {
                    case R.id.menuHome:
                        Toast.makeText(MainActivity.this, "Home toast", Toast.LENGTH_SHORT).show();
                        drawerLayout.closeDrawers();
                        break;

                    case R.id.menuShare:
                        Toast.makeText(MainActivity.this, "Share Toast", Toast.LENGTH_SHORT).show();
                        drawerLayout.closeDrawers();
                        break;
                }
                return false;
            }
        });
        //------------------------------

        // ------------------------
        // App Bar Click Event
        imageMenu = findViewById(R.id.imageMenu);

        imageMenu.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                // Code Here
                drawerLayout.openDrawer(GravityCompat.START);
            }
        });
    } // OnCreate Method Close here ==============
}
```
 
