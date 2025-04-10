### ✅ 1. **Classe `MultiplicationActivity.java`**

Cette activité contient la logique pour afficher les questions de multiplication dans un `ListView` et envoyer les résultats à une autre activité via un `Intent` lorsque l'utilisateur appuie sur le bouton **Valider**.

```java
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ListView;

import androidx.appcompat.app.AppCompatActivity;

import java.util.ArrayList;
import java.util.Collections;

public class MultiplicationActivity extends AppCompatActivity {

    private ListView listView;
    private MultiplicationAdapter adapter;
    private ArrayList<MultiplicationQuestion> questions;
    private Button validateButton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_multiplication);

        listView = findViewById(R.id.listView);
        validateButton = findViewById(R.id.button_validate);

        // Récupérer la table de multiplication choisie depuis l'Intent précédent
        int table = getIntent().getIntExtra("table", 5);  // Par défaut la table 5

        // Créer les questions pour cette table
        questions = new ArrayList<>();
        for (int i = 1; i <= 10; i++) {
            questions.add(new MultiplicationQuestion(table, i));
        }

        // Mélanger les questions
        Collections.shuffle(questions);

        // Configurer l'adapter pour afficher les questions dans le ListView
        adapter = new MultiplicationAdapter(this, questions);
        listView.setAdapter(adapter);

        // Action du bouton "Valider"
        validateButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // Créer un Intent pour envoyer les résultats
                Intent resultIntent = new Intent(MultiplicationActivity.this, ResultActivity.class);

                // Créer des listes pour les réponses et les tables
                ArrayList<String> answers = new ArrayList<>();
                ArrayList<String> tables = new ArrayList<>();

                // Ajouter les réponses et les tables dans les listes
                for (MultiplicationQuestion question : questions) {
                    answers.add(String.valueOf(question.getUserAnswer())); // Réponse de l'utilisateur
                    tables.add(question.getBase() + " x " + question.getMultiplier()); // Table sous forme de chaîne
                }

                // Ajouter les données à l'Intent
                resultIntent.putStringArrayListExtra("answers", answers);
                resultIntent.putStringArrayListExtra("tables", tables);

                // Démarrer l'activité des résultats
                startActivity(resultIntent);
            }
        });
    }
}
```

### ✅ 2. **Classe `MultiplicationQuestion.java`**

Cette classe représente une question de multiplication avec l'opérande (base et multiplicateur) et la réponse de l'utilisateur.

```java
public class MultiplicationQuestion {

    private int base; // La table de multiplication
    private int multiplier; // Le multiplicateur
    private int userAnswer; // Réponse de l'utilisateur

    public MultiplicationQuestion(int base, int multiplier) {
        this.base = base;
        this.multiplier = multiplier;
        this.userAnswer = -1; // Valeur par défaut avant que l'utilisateur ne réponde
    }

    public int getBase() {
        return base;
    }

    public int getMultiplier() {
        return multiplier;
    }

    public int getUserAnswer() {
        return userAnswer;
    }

    public void setUserAnswer(int userAnswer) {
        this.userAnswer = userAnswer;
    }

    public int getCorrectAnswer() {
        return base * multiplier; // La réponse correcte
    }
}
```

### ✅ 3. **Adapter `MultiplicationAdapter.java`**

L'adapter permet d'afficher chaque question dans le `ListView`. Il prend en charge l'entrée de l'utilisateur pour chaque question.

```java
import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.EditText;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.recyclerview.widget.RecyclerView;

import java.util.ArrayList;

public class MultiplicationAdapter extends RecyclerView.Adapter<MultiplicationAdapter.ViewHolder> {

    private Context context;
    private ArrayList<MultiplicationQuestion> questions;

    public MultiplicationAdapter(Context context, ArrayList<MultiplicationQuestion> questions) {
        this.context = context;
        this.questions = questions;
    }

    @NonNull
    @Override
    public ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(context).inflate(R.layout.item_multiplication_question, parent, false);
        return new ViewHolder(view);
    }

    @Override
    public void onBindViewHolder(@NonNull ViewHolder holder, int position) {
        MultiplicationQuestion question = questions.get(position);
        holder.questionText.setText(question.getBase() + " x " + question.getMultiplier());
        
        holder.answerInput.setText(String.valueOf(question.getUserAnswer()));
        
        holder.answerInput.setOnFocusChangeListener((v, hasFocus) -> {
            if (!hasFocus) {
                try {
                    int userAnswer = Integer.parseInt(holder.answerInput.getText().toString());
                    question.setUserAnswer(userAnswer);
                } catch (NumberFormatException e) {
                    question.setUserAnswer(-1); // Si aucune réponse valide, garder une valeur par défaut
                }
            }
        });
    }

    @Override
    public int getItemCount() {
        return questions.size();
    }

    public static class ViewHolder extends RecyclerView.ViewHolder {

        TextView questionText;
        EditText answerInput;

        public ViewHolder(View itemView) {
            super(itemView);
            questionText = itemView.findViewById(R.id.question_text);
            answerInput = itemView.findViewById(R.id.answer_input);
        }
    }
}
```

### ✅ 4. **Layout `activity_multiplication.xml`**

Le layout principal avec un `ListView` et un bouton **Valider**.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <ListView
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1" />

    <!-- Bouton Valider -->
    <Button
        android:id="@+id/button_validate"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Valider" />
</LinearLayout>
```

### ✅ 5. **Layout `item_multiplication_question.xml`**

Le layout pour chaque question de multiplication dans le `ListView`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="horizontal"
    android:padding="8dp">

    <TextView
        android:id="@+id/question_text"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="2"
        android:textSize="18sp" />

    <EditText
        android:id="@+id/answer_input"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:hint="Réponse"
        android:inputType="number" />
</LinearLayout>
```

### ✅ 6. **Classe `ResultActivity.java`**

Cette activité reçoit les réponses et tables via `putExtra` et les affiche.

```java
import android.os.Bundle;
import android.widget.ListView;
import android.widget.ArrayAdapter;
import androidx.appcompat.app.AppCompatActivity;

import java.util.ArrayList;

public class ResultActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_result);

        // Récupérer les données envoyées depuis l'activité précédente
        ArrayList<String> answers = getIntent().getStringArrayListExtra("answers");
        ArrayList<String> tables = getIntent().getStringArrayListExtra("tables");

        ListView resultListView = findViewById(R.id.result_list_view);

        // Créer un adapter pour afficher les résultats
        ArrayList<String> resultItems = new ArrayList<>();
        for (int i = 0; i < tables.size(); i++) {
            resultItems.add(tables.get(i) + " = " + answers.get(i));
        }

        ArrayAdapter<String> adapter = new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, resultItems);
        resultListView.setAdapter(adapter);
    }
}
```

### ✅ 7. **Layout `activity_result.xml`**

Le layout pour afficher les résultats.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <ListView
        android:id="@+id/result_list_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</LinearLayout>
```

---

Avec cette structure, l'application génère une liste de questions de multiplication mélangées, permet à l'utilisateur de saisir ses réponses et envoie les résultats à une autre activité pour les afficher.