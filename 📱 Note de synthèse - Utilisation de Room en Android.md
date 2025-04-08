# 📘 Cours Room – Exemple concret : Application de Quiz

---

### 🧩 **Objectif de l’app**

Créer une application Android simple qui :

- Affiche une liste de questions
    
- Permet d’en ajouter
    
- Stocke tout dans une base locale Room (SQLite)
    

---

### 🧱 1. Créer une entité `Question`

> Une entité représente une table dans la base.

```java
// Question.java
import androidx.room.Entity;
import androidx.room.PrimaryKey;

@Entity
public class Question {
    @PrimaryKey(autoGenerate = true)
    public int id;

    public String question;
    public String bonneReponse;
    public String mauvaiseReponse1;
    public String mauvaiseReponse2;

    // Constructeur
    public Question(String question, String bonneReponse, String mauvaiseReponse1, String mauvaiseReponse2) {
        this.question = question;
        this.bonneReponse = bonneReponse;
        this.mauvaiseReponse1 = mauvaiseReponse1;
        this.mauvaiseReponse2 = mauvaiseReponse2;
    }
}
```

---

### 📂 2. Créer le DAO

> DAO = interface qui contient les requêtes SQL vers la base, mais **sous forme de méthodes Java/Kotlin**.

```java
// QuestionDao.java
import androidx.room.Dao;
import androidx.room.Insert;
import androidx.room.Query;

import java.util.List;

@Dao
public interface QuestionDao {

    @Insert
    void insert(Question question);

    @Query("SELECT * FROM Question")
    List<Question> getAll();
}
```

---

### 🧠 3. Créer la base de données

> Une classe abstraite qui donne accès à Room.

```java
// AppDatabase.java
import androidx.room.Database;
import androidx.room.RoomDatabase;

@Database(entities = {Question.class}, version = 1)
public abstract class AppDatabase extends RoomDatabase {
    public abstract QuestionDao questionDao();
}
```

---

### 🛠️ 4. Initialiser la base dans l’activité

```java
// MainActivity.java
import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;
import androidx.room.Room;
import java.util.List;

public class MainActivity extends AppCompatActivity {

    AppDatabase db;
    QuestionDao dao;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        // Crée la base
        db = Room.databaseBuilder(getApplicationContext(),
                AppDatabase.class, "quiz-db").allowMainThreadQueries().build();

        dao = db.questionDao();

        // Ajouter une question
        dao.insert(new Question("Combien font 2+2 ?", "4", "3", "5"));

        // Lire les questions
        List<Question> questions = dao.getAll();

        for (Question q : questions) {
            System.out.println("Q: " + q.question);
        }
    }
}
```

> ⚠️ `allowMainThreadQueries()` est utilisé ici **juste pour le test**, **à éviter en production** → préférer coroutines ou threading.

---

### 🧰 5. Ajouter les dépendances

Dans `libs.versions.toml` :

```toml
[versions]
room = "2.6.1"

[libraries]
room-compiler = { group = "androidx.room", name = "room-compiler", version.ref = "room" }
room-runtime = { group = "androidx.room", name = "room-runtime", version.ref = "room" }
```

Dans `build.gradle (Module)` :

```gradle
dependencies {
    implementation libs.room.runtime
    annotationProcessor libs.room.compiler
}
```

---

### ✅ Résultat

Quand tu lances l’app :

- La base est créée
    
- Une question est ajoutée
    
- Les questions sont récupérées et affichées dans la console/log
    

---

# 📘 Cours Room – Exemple concret : Application de Quiz

---

### 🧩 **Objectif de l’app**

Créer une application Android simple qui :

- Affiche une liste de questions
    
- Permet d’en ajouter
    
- Stocke tout dans une base locale Room (SQLite)
    

---

### 🧱 1. Créer une entité `Question`

> Une entité représente une table dans la base.

```java
// Question.java
import androidx.room.Entity;
import androidx.room.PrimaryKey;

@Entity
public class Question {
    @PrimaryKey(autoGenerate = true)
    public int id;

    public String question;
    public String bonneReponse;
    public String mauvaiseReponse1;
    public String mauvaiseReponse2;

    // Constructeur
    public Question(String question, String bonneReponse, String mauvaiseReponse1, String mauvaiseReponse2) {
        this.question = question;
        this.bonneReponse = bonneReponse;
        this.mauvaiseReponse1 = mauvaiseReponse1;
        this.mauvaiseReponse2 = mauvaiseReponse2;
    }
}
```

---

### 📂 2. Créer le DAO

> DAO = interface qui contient les requêtes SQL vers la base, mais **sous forme de méthodes Java/Kotlin**.

```java
// QuestionDao.java
import androidx.room.Dao;
import androidx.room.Insert;
import androidx.room.Query;

import java.util.List;

@Dao
public interface QuestionDao {

    @Insert
    void insert(Question question);

    @Query("SELECT * FROM Question")
    List<Question> getAll();
}
```

---

### 🧠 3. Créer la base de données

> Une classe abstraite qui donne accès à Room.

```java
// AppDatabase.java
import androidx.room.Database;
import androidx.room.RoomDatabase;

@Database(entities = {Question.class}, version = 1)
public abstract class AppDatabase extends RoomDatabase {
    public abstract QuestionDao questionDao();
}
```

---

### 🛠️ 4. Initialiser la base dans l’activité

```java
// MainActivity.java
import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;
import androidx.room.Room;
import java.util.List;

public class MainActivity extends AppCompatActivity {

    AppDatabase db;
    QuestionDao dao;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        // Crée la base
        db = Room.databaseBuilder(getApplicationContext(),
                AppDatabase.class, "quiz-db").allowMainThreadQueries().build();

        dao = db.questionDao();

        // Ajouter une question
        dao.insert(new Question("Combien font 2+2 ?", "4", "3", "5"));

        // Lire les questions
        List<Question> questions = dao.getAll();

        for (Question q : questions) {
            System.out.println("Q: " + q.question);
        }
    }
}
```

> ⚠️ `allowMainThreadQueries()` est utilisé ici **juste pour le test**, **à éviter en production** → préférer coroutines ou threading.

---

### 🧰 5. Ajouter les dépendances

Dans `libs.versions.toml` :

```toml
[versions]
room = "2.6.1"

[libraries]
room-compiler = { group = "androidx.room", name = "room-compiler", version.ref = "room" }
room-runtime = { group = "androidx.room", name = "room-runtime", version.ref = "room" }
```

Dans `build.gradle (Module)` :

```gradle
dependencies {
    implementation libs.room.runtime
    annotationProcessor libs.room.compiler
}
```

---

### ✅ Résultat

Quand tu lances l’app :

- La base est créée
    
- Une question est ajoutée
    
- Les questions sont récupérées et affichées dans la console/log
    

---

Tu veux que je t’aide à :

- Ajouter une interface graphique (formulaire d’ajout + liste) ?
    
- Refaire ce projet avec des **coroutines** (Kotlin) au lieu de `allowMainThreadQueries()` ?
    
- Ajouter un **RecyclerView** pour afficher les questions ?
    

Dis-moi ce que tu veux faire évoluer et je te le code 😄