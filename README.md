# Ex.No:2(B) - To create a two screens , first screen will take one number input from user. After click on Factorial button, second screen will open and it should display factorial of the same number using Explicit Intents.


## AIM:

To create a two screens , first screen will take one number input from user. After click on Factorial button, second screen will open and it should display factorial of the same number using Explicit Intents.


## EQUIPMENTS REQUIRED:

Latest Version Android Studio

## ALGORITHM:

1. Create a new Android project with two Activities.
2. Design the first screen with an EditText and a Factorial button.
3. Get the number entered by the user and validate the input.
4. Calculate the factorial of the number using a loop.
5. Pass the factorial result to the second Activity using an Explicit Intent.
6. Display the factorial result on the second screen and provide a Home Screen button to return to the first screen.

## PROGRAM:
```
Developed by: LAKSHMIDHAR N
Registration Number  212224230138
```

### MainActivity.java

```java
package com.example.exp2b;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;
import android.widget.Toast;
import com.google.android.material.color.DynamicColors;
import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

import java.math.BigInteger;

public class MainActivity extends AppCompatActivity {
    EditText numberInput;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        DynamicColors.applyToActivitiesIfAvailable(getApplication());

        setContentView(R.layout.activity_main);
        numberInput = findViewById(R.id.editTextText);
    }
    public void newsScreen(View view) {
        String input = numberInput.getText().toString();
        if (input.isEmpty()) {
            Toast t = Toast.makeText(this, "Please enter a number", Toast.LENGTH_SHORT);
            t.show();
            return;
        }
        try {
            int n = Integer.parseInt(input);
            if (n < 0) {
                Toast.makeText(this, "Please enter a non-negative number", Toast.LENGTH_SHORT).show();
                return;
            }
            BigInteger factorial = calculateFactorial(n);

            Intent i = new Intent(MainActivity.this, MainActivity2.class);
            i.putExtra("RESULT", factorial.toString());
            startActivity(i);
        } catch (NumberFormatException e) {
            Toast.makeText(this, "Invalid number", Toast.LENGTH_SHORT).show();
        }
    }
    private BigInteger calculateFactorial(int n) {
        BigInteger result = BigInteger.ONE;
        for (int i = 2; i <= n; i++) {
            result = result.multiply(BigInteger.valueOf(i));
        }
        return result;
    }
}
```

### MainActivity2.java

```java

package com.example.exp2b;
import android.widget.TextView;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity2 extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity2);

        TextView resultTextView =
                findViewById(R.id.resultTextView);

        String result = getIntent().getStringExtra("RESULT");

        if (resultTextView != null && result != null) {
            resultTextView.setText(result);
        }
    }

    public void homeScreen(View view) {
        Intent intent = new Intent(
                MainActivity2.this, MainActivity.class);
        startActivity(intent);
        finish();
    }
}

```

### activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Factorial Calculator"
        android:textSize="24sp"
        app:layout_constraintBottom_toTopOf="@+id/editTextText"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <com.google.android.material.button.MaterialButton
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="200dp"
        android:onClick="newsScreen"
        android:text="Calculate"
        android:textColor="?attr/colorOnPrimary"
        app:backgroundTint="#03A9F4"
        app:cornerRadius="50dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent" />

    <EditText
        android:id="@+id/editTextText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="200dp"
        android:ems="10"
        android:hint="Enter a number"
        android:inputType="number"
        android:text=""
        app:layout_constraintBottom_toTopOf="@+id/button"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.492"
        app:layout_constraintStart_toStartOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>

```

### activity2.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/linearLayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="The Result is"
        android:textSize="24sp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_marginTop="152dp" />

    <TextView
        android:id="@+id/resultTextView"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:text="0"
        android:textAlignment="center"
        android:textSize="24sp"
        app:layout_constraintTop_toBottomOf="@id/textView"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_marginTop="30dp"
        android:layout_marginStart="16dp"
        android:layout_marginEnd="16dp" />

    <com.google.android.material.button.MaterialButton
        android:id="@+id/button2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Home Screen"
        android:onClick="homeScreen"
        app:cornerRadius="50dp"
        app:backgroundTint="?attr/colorPrimary"
        android:textColor="?attr/colorOnPrimary"
        app:layout_constraintTop_toBottomOf="@id/resultTextView"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_marginTop="40dp" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

## OUTPUT

<img width="1917" height="1015" alt="image" src="https://github.com/user-attachments/assets/05101e05-a13e-4fb5-a7e5-f69e54b7b72d" />

<img width="1917" height="1020" alt="image" src="https://github.com/user-attachments/assets/9a6fa8f9-4c5c-49c1-864d-8d5181601a46" />




## RESULT
Thus a Simple Android Application create a Explicit Intents using Android Studio is developed and executed successfully.


