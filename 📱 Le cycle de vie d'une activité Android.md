# 📘 Cours : Le Cycle de Vie d’une Activité Android

---

### 🔄 1. Introduction

Une **activité** est un écran de l’application. Android gère son **cycle de vie** pour éviter de consommer trop de ressources. Ton rôle : **libérer, restaurer ou sauvegarder ce qui est nécessaire** à chaque étape.

---

### 🧱 2. Les Méthodes Principales

|Méthode|Quand elle est appelée|Que faire ?|
|---|---|---|
|`onCreate()`|Création de l'activité|Initialisation des vues, données, etc.|
|`onStart()`|Activité visible mais pas encore interactive|Préparer à l’affichage|
|`onResume()`|Activité interactive (tout en haut de la pile)|Lancer les animations, écouter les capteurs|
|`onPause()`|Une autre activité va passer devant|Sauvegarder temporairement, libérer les ressources légères|
|`onStop()`|Activité complètement cachée|Sauvegarder de façon plus complète (ex: base de données)|
|`onDestroy()`|Activité détruite définitivement|Libérer toutes les ressources|

---

### 🔁 3. Cycle de vie graphique

Voici un schéma simplifié :

```
       onCreate()
            ↓
         onStart()
            ↓
        onResume()
            ↓
    [Activité visible]
            ↓
        onPause()
            ↓
         onStop()
            ↓
        onDestroy()
```

---

## 🧪 Exemple concret : Jeu de Quiz avec score

---

### 🎯 Objectif

Afficher une question de quiz avec un score et un niveau. Si l’activité est détruite (rotation, etc.), **restaurer ces valeurs**.

---

### 🛠️ 1. Activité avec sauvegarde d’état

```java
public class QuizActivity extends AppCompatActivity {

    private int mCurrentScore = 0;
    private int mCurrentLevel = 1;

    private static final String STATE_SCORE = "score";
    private static final String STATE_LEVEL = "level";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_quiz);

        // 🔁 Restauration si l’activité a été détruite et recréée
        if (savedInstanceState != null) {
            mCurrentScore = savedInstanceState.getInt(STATE_SCORE);
            mCurrentLevel = savedInstanceState.getInt(STATE_LEVEL);
        }

        // 🎮 Mise à jour de l’interface
        updateUI();
    }

    @Override
    protected void onSaveInstanceState(Bundle outState) {
        super.onSaveInstanceState(outState);

        // 💾 Sauvegarde de l'état
        outState.putInt(STATE_SCORE, mCurrentScore);
        outState.putInt(STATE_LEVEL, mCurrentLevel);
    }

    private void updateUI() {
        TextView scoreView = findViewById(R.id.scoreView);
        TextView levelView = findViewById(R.id.levelView);

        scoreView.setText("Score : " + mCurrentScore);
        levelView.setText("Niveau : " + mCurrentLevel);
    }

    // Simule une bonne réponse
    public void bonneReponse(View v) {
        mCurrentScore += 10;
        mCurrentLevel++;
        updateUI();
    }
}
```

---

### 📋 2. Layout XML (`activity_quiz.xml`)

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent" android:padding="24dp">

    <TextView android:id="@+id/scoreView"
        android:text="Score : 0"
        android:textSize="24sp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />

    <TextView android:id="@+id/levelView"
        android:text="Niveau : 1"
        android:textSize="24sp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />

    <Button android:onClick="bonneReponse"
        android:text="Bonne réponse !"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />
</LinearLayout>
```

---

### 🔎 3. Résultat

- Tu réponds à des questions → le score augmente.
    
- Tu fais une **rotation** ou **quittes l'app** → les données sont **restaurées automatiquement**.
    
- Grâce à `onSaveInstanceState()` et `onCreate(Bundle)`.
    

---

## 🧠 Résumé à retenir

|Méthode|Usage|
|---|---|
|`onCreate()`|Initialiser les vues et restaurer l’état|
|`onStart()`|Préparer l’affichage|
|`onResume()`|Démarrer des actions utilisateur|
|`onPause()`|Sauvegarde rapide, stopper animation|
|`onStop()`|Sauvegarde complète (ex : BDD)|
|`onDestroy()`|Nettoyer tout avant destruction|
|`onSaveInstanceState()`|Sauvegarder automatiquement des valeurs simples|
|`onRestoreInstanceState()`|Restaurer manuellement (optionnel)|

---

Tu veux que je t’ajoute un schéma interactif ? Ou une deuxième activité pour voir comment `onPause()` / `onStop()` réagissent quand on change d’écran ?