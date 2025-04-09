## 🔐 `SharedPreferences` – Stockage clé-valeur simple en Android

### 📘 À quoi servent les `SharedPreferences` ?

- Stocker des **données simples** de manière **persistante** (clé/valeur)
    
- Exemple : nom d’utilisateur, thème choisi, préférences d'affichage, score, etc.
    
- Les données sont **disponibles même après fermeture de l’application**
    

---

## 🧱 Structure

```java
SharedPreferences prefs = getSharedPreferences("nom_du_fichier", MODE_PRIVATE);
SharedPreferences.Editor editor = prefs.edit();
editor.putString("cle", "valeur");
editor.apply(); // ou commit()
```

---

## 🛠️ Lecture et écriture

### ✅ Écriture (sauvegarder une valeur)

```java
SharedPreferences prefs = getSharedPreferences("mes_prefs", MODE_PRIVATE);
SharedPreferences.Editor editor = prefs.edit();

editor.putString("username", "Alice");
editor.putInt("score", 42);
editor.putBoolean("dark_mode", true);

editor.apply(); // Sauvegarde asynchrone (recommandée)
```

### 🔄 Lecture (récupérer une valeur)

```java
SharedPreferences prefs = getSharedPreferences("mes_prefs", MODE_PRIVATE);

String username = prefs.getString("username", "inconnu");
int score = prefs.getInt("score", 0);
boolean darkMode = prefs.getBoolean("dark_mode", false);
```

---

## ❌ Suppression

### Supprimer une clé spécifique

```java
prefs.edit().remove("username").apply();
```

### Supprimer toutes les préférences

```java
prefs.edit().clear().apply();
```

---

## 📍 Exemple complet dans une activité

```java
public class MainActivity extends AppCompatActivity {

    SharedPreferences prefs;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        prefs = getSharedPreferences("mes_prefs", MODE_PRIVATE);

        // Sauvegarde
        prefs.edit().putString("email", "test@example.com").apply();

        // Lecture
        String email = prefs.getString("email", "aucun email");
        Log.d("DEBUG", "Email sauvegardé : " + email);
    }
}
```

---

## 🧪 Où sont stockées les données ?

Sur l'appareil, dans un fichier XML situé dans :

```
/data/data/nom.du.package/shared_prefs/
```

---

## 🧠 Astuces

- Utiliser `apply()` plutôt que `commit()` (apply est **asynchrone**, commit est **synchrone**).
    
- Préférer une **classe utilitaire** pour gérer tous les accès (ex : `PrefsManager`) pour éviter la duplication.
    

---

Souhaites-tu aussi une version avec une **classe helper (PrefsManager)** pour centraliser tous les accès ?