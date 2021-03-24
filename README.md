# ISAK_NewCitizen

### General 
- responsive screen 
- premium versus free app 
- tutorial video 

### Map - Salma
- GPS Sensor 
- only present relevant pins in the map 
- Description about location 
- search location/address/city
- save location <br>

This is the code for a basic app that just shows a map and one pin as an example. I did not get the chance to test it as I messed up something and now Android Studio does not want to work... To fix this I need to download something that will take a few hours but meanwhile i would appreciate if someone could test it thank you!
```package com.example.quiz;
import com.google.android.gms.maps.GoogleMap;
import com.google.android.gms.maps.SupportMapFragment;
import com.google.android.gms.maps.model.LatLng;
import com.google.android.gms.maps.model.MarkerOptions;


import android.os.Bundle;
import android.support.v4.app.FragmentActivity;

    private GoogleMap mMap;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.basic_demo);
        setUpMapIfNeeded();
    }

    @Override
    protected void onResume() {
        super.onResume();
        setUpMapIfNeeded();
    }

    private void setUpMapIfNeeded() {
        if (mMap == null) {
            // Try to obtain the map from the SupportMapFragment.
            mMap = ((SupportMapFragment) getSupportFragmentManager().findFragmentById(R.id.map))
                    .getMap();
            if (mMap != null) {
                setUpMap();
            }
        }
    }

    private void setUpMap() {
        mMap.addMarker(new MarkerOptions().position(new LatLng(0, 0)).title("Marker"));
    }
}

```

### Settings & Main Menu - Cathy 
- notifications 
- user feedback messsaging 
- change language feature 
- donation 
- tell a friend 
- privacy and user terms 


### Lessons, badges, immigration guide - Isabel 

**Quiz feature **

**Main Java: **

```package com.example.quiz;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;
import android.view.View;
import android.widget.Toast;

import org.w3c.dom.Text;


public class MainActivity extends AppCompatActivity {

    private Questions Questions = new Questions();
    private TextView ShowQuestion;
    private TextView ShowScore;
    private String answer;
    private int MyScore = 0;
    private int num = 0;
    private Button button1;
    private Button button2;
    private Button button3;
    private Button button4;
    private int questitonlength = Questions.Questions.length;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        //rename the buttons and match them from xml id
        button1 = (Button)findViewById(R.id.button1);
        button2 = (Button)findViewById(R.id.button2);
        button3 = (Button)findViewById(R.id.button3);
        button4 = (Button)findViewById(R.id.button4);
        ShowQuestion = (TextView)findViewById(R.id.Question);
        ShowScore = (TextView)findViewById(R.id.myscore);

        // setting the OnClick listener
        button1.setOnClickListener(new View.OnClickListener(){
            @Override
            public void onClick(View v){

                switch (v.getId()) {
                    case R.id.button1:
                        if(button1.getText() == answer){
                            Toast.makeText(MainActivity.this, "Correct", Toast.LENGTH_SHORT).show();
                            nextQuestion();
                            updateScore(MyScore);

                        }
                        else{
                            Toast.makeText(MainActivity.this, "Incorrect", Toast.LENGTH_SHORT).show();
                            MyScore = MyScore += 1;
                            nextQuestion();
                        }
                    case R.id.button2:
                        if(button2.getText() == answer){
                            Toast.makeText(MainActivity.this, "Correct", Toast.LENGTH_SHORT).show();
                            nextQuestion();
                            updateScore(MyScore);

                        }
                        else{
                            Toast.makeText(MainActivity.this, "Incorrect", Toast.LENGTH_SHORT).show();
                            nextQuestion();
                        }
                    case R.id.button3:
                        if(button3.getText() == answer){
                            Toast.makeText(MainActivity.this, "Correct", Toast.LENGTH_SHORT).show();
                            nextQuestion();
                            updateScore(MyScore);

                        }
                        else{
                            Toast.makeText(MainActivity.this, "Incorrect", Toast.LENGTH_SHORT).show();
                            nextQuestion();
                        }

                    case R.id.button4:
                        if(button4.getText() == answer){
                            Toast.makeText(MainActivity.this, "Correct", Toast.LENGTH_SHORT).show();
                            nextQuestion();
                            updateScore(MyScore);

                        }
                        else{
                            Toast.makeText(MainActivity.this, "Incorrect", Toast.LENGTH_SHORT).show();
                            nextQuestion();
                        }
                }
            }


        //Create method to show next question
        private void nextQuestion(){
            ShowQuestion.setText(Questions.GetQuestion(num));
            button1.setText(Questions.GetChoices1(num));
            button2.setText(Questions.GetChoices2(num));
            button3.setText(Questions.GetChoices3(num));
            button4.setText(Questions.GetChoices4(num));
            answer = Questions.GetAnswer(num);
            num++;

            };
        //Create method to update score
        private void updateScore(int points){
            ShowScore.setText("" + MyScore);
            MyScore ++;

        }
        });
    };
}

```

**Questions.java **

```

package com.example.quiz;

public class Questions {


    public String Questions[]={
        "In which bin does styrofoam go into?", "How do you get rid of large bulk items?"

    };
    public String Choices[][]={
            {"Burnable","Recyclable","Non-burnable","Bulk Garbage"},
            {"Leave it outside","Throw in burnable","Contact local administration","Throw on special days"}
    };
    public String RightChoices[]={
            "Recyclable","Contact local administration"

    };

    public String GetQuestion(int num){
        String question = Questions[num];
        return question;
    }

    public String GetChoices1(int num){
            String Choice = Choices[num][0];
            return Choice;
    }

    public String GetChoices2(int num){
            String Choice = Choices[num][1];
            return Choice;
    }

    public String GetChoices3(int num){
            String Choice = Choices[num][2];
            return Choice;
    }
    public String GetChoices4(int num){
            String Choice = Choices[num][3];
            return Choice;
    }
    public String GetAnswer(int num){
            String answer = RightChoices[num];
            return answer;
    }
}
```

**activity_main.xml**

```
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/container"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#FFFFFF"
    tools:context=".MainActivity"
    android:theme="@style/AppTheme.NoActionBar">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:clipChildren="false"
        android:clipToPadding="false"
        android:orientation="vertical">

        <ImageView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_marginTop="-550dp"
            android:src="@drawable/shape" />

        <ImageView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center_horizontal"
            android:layout_marginTop="-700dp"
            android:src="@drawable/rectanglequestion" />

        <TextView
            android:id="@+id/CurrentQuestion"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginLeft="185dp"
            android:layout_marginTop="-30dp"
            android:text="Q"
            android:textColor="#FFF"
            android:textSize="20dp" />

        <TextView
            android:id="@+id/NumberofQuestion"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginLeft="200dp"
            android:layout_marginTop="-27dp"
            android:text="/10"
            android:textColor="#FFF"
            android:textSize="20dp" />

        <TextView
            android:id="@+id/myscore"
            android:layout_width="wrap_content"
            android:layout_height="30dp"
            android:layout_marginTop="-25dp"
            android:layout_marginLeft="50dp"
            android:text ="Score"
            android:textColor="#FFF"
            android:textSize="20dp"></TextView>
        <TextView
            android:id="@+id/Question"
            android:layout_width="250dp"
            android:layout_height="60dp"
            android:layout_gravity="center_horizontal"
            android:layout_marginTop="60dp"
            android:textColor="#FFF"
            android:gravity="center"
            android:lineSpacingExtra="6dp"
            android:text="Question"
            android:textSize="20dp" />

        <Button
            android:id="@+id/button1"
            android:layout_width="265dp"
            android:layout_height="60dp"
            android:layout_gravity="center"
            android:layout_marginTop="150dp"
            android:background="@drawable/button_background"
            android:text="Button"
            android:textColor = "#FFF"
            android:textSize = '20dp'
            android:gravity = "center"/>

        <Button
            android:id="@+id/button2"
            android:layout_width="265dp"
            android:layout_height="60dp"
            android:layout_marginTop="23dp"
            android:layout_gravity="center"
            android:textSize = '20dp'
            android:background="@drawable/button_background"
            android:text="Button"
            android:textColor = "#FFF"
            android:gravity = "center"/>
        <Button
            android:id="@+id/button3"
            android:layout_width="265dp"
            android:layout_marginTop="23dp"
            android:layout_height="60dp"
            android:textSize = '20dp'
            android:layout_gravity="center"
            android:text = "Button"
            android:textColor = "#FFF"
            android:gravity = "center"
            android:background="@drawable/button_background"/>

        <Button
            android:id="@+id/button4"
            android:layout_width="265dp"
            android:layout_height="60dp"
            android:layout_gravity="center"
            android:textSize = '20dp'
            android:layout_marginTop="23dp"
            android:background="@drawable/button_background"
            android:text="Button"
            android:gravity = "center"
            android:textColor="#FFF"/>

    </LinearLayout>

</FrameLayout>
``` 

buttonbackground.xml 

```
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">
    <size
        android:width="265dp"
        android:height="60dp"/>
    <solid
        android:color="#FEC874"/>
    <corners android:radius="30dp" />
</shape>
``` 

rectanglequestion.xml
 ```
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">
    <solid
        android:color="#0A67B3"/>
    <size
        android:width="130dp"
        android:height="30dp"/>

    <corners android:radius="30dp"/>
</shape>
```

shape.xml

```
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">
    <gradient
        android:startColor="#72CDF3"
        android:endColor="#1F93CD"/>
    <size
        android:width="6dp"
        android:height="5dp"/>
    <corners
        android:bottomLeftRadius="10dp"
        android:bottomRightRadius="10dp"/>
</shape>
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">
    <gradient
        android:startColor="#72CDF3"
        android:endColor="#1F93CD"/>
    <size
        android:width="6dp"
        android:height="5dp"/>
    <corners
        android:bottomLeftRadius="10dp"
        android:bottomRightRadius="10dp"/>
</shape>
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">
    <gradient
        android:startColor="#72CDF3"
        android:endColor="#1F93CD"/>
    <size
        android:width="6dp"
        android:height="5dp"/>
    <corners
        android:bottomLeftRadius="10dp"
        android:bottomRightRadius="10dp"/>
</shape>
```
Android Manifest
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.quiz">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Quiz">
        <activity android:name=".MainActivity"></activity>
        <activity android:name=".QuizMenu">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

Quiz Menu (second activity) 
```
package com.example.quiz;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;
import android.view.View;
import android.widget.Toast;


public class QuizMenu extends AppCompatActivity {
    private Button recyclingquiz;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_quiz_menu2);

        recyclingquiz = (Button) findViewById(R.id.trash_recyling_button);
        recyclingquiz.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                gotofirstquiz();

            }
        });
    }

    private void gotofirstquiz() {
        android.content.Intent intent = new android.content.Intent(this, MainActivity.class);
        startActivity(intent);
    }
}
``` 

activity_quiz.xml
```
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:background = "#FFF"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".QuizMenu">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="55dp"
        android:text = "Lessons"
        android:textSize="25dp"
        android:gravity = "center"
        android:textColor="@color/white"
        android:background = "@color/blue"
        />

    <Button
        android:id = "@+id/trash_recyling_button"
        android:layout_width="361dp"
        android:layout_height="wrap_content"
        android:layout_marginLeft="25dp"
        android:layout_marginTop="80dp"
        android:background="@drawable/lesson_enter_shapes"
        android:gravity="center_vertical"
        android:padding = "15dp"
        android:text="Trash Recyling"
        android:textSize="20dp"
        android:textColor="@color/white"/>

</FrameLayout>
```

Lesson_enter_shapes: 

```
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape = "rectangle">

    <solid android:color="@color/orange"/>
    <size android:width="300dp"
        android:height="70dp"/>

    <corners android:radius = "30dp" />

</shape>
``` 


- Progress bar 
- Notification for new badge 
-  check box 
-  Logic for going to next level 
-  links  
