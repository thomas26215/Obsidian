Voici une **note en Markdown**, orientée **code et développement Android**, avec les **informations utiles uniquement** pour t’aider à coder :

---

# 📱 Android - Développement Mobile (R4 Real 11)

## 🛠 Environnement

- **Android Studio** (basé sur IntelliJ) – IDE officiel  
    📎 [https://developer.android.com/studio/](https://developer.android.com/studio/)
    
- **Langages supportés** :
    
    - Java (avec VM **Dalvik** puis **ART**, `.dex`)
        
    - Kotlin (depuis 2017)
        

---

## 📦 Structure d’une app Android

- Archive `.apk` = code compilé + ressources
    
- Chaque app tourne dans :
    
    - son **propre processus**
        
    - sa **propre VM**
        
    - un utilisateur Linux avec accès **uniquement à ses fichiers**
        

---

## 🧱 Composants essentiels

### 🧩 Activité (`Activity`)

- Une **fenêtre** de l’app, avec UI + logique
    
- Étend `Activity`, `AppCompatActivity`, etc.
    

```java
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main); // lie le XML
        // findViewById() + écouteurs
    }
}
```

---

## 🖼 Interfaces Utilisateur (UI)

### 🔗 Hiérarchie de vues

- Toute UI = arborescence de `View` et `ViewGroup`
    
- Définie via :
    
    - **Code Java** (`new Button(...)`)
        
    - **XML** (`res/layout/activity_main.xml`)
        

### ✍️ Exemple XML

```xml
<LinearLayout ...>
    <EditText android:id="@+id/editTextMessage" />
    <Button android:id="@+id/buttonSend" />
</LinearLayout>
```

> `@+id/...` → crée un ID  
> Accessible via `R.id.buttonSend`

### 🔍 Récupération en Java

```java
Button btn = findViewById(R.id.buttonSend);
```

---

## 🎯 Gestion des événements

### 📌 Pattern commun

```java
btn.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        // Action quand on clique sur le bouton
    }
});
```

### ✅ Interface = Listener

|Abonnement|Notification (méthode)|
|---|---|
|`setOnClickListener`|`onClick(View v)`|
|`setOnLongClickListener`|`onLongClick(View v)`|
|`setOnFocusChangeListener`|`onFocusChange(View v, boolean hasFocus)`|
|`setOnKeyListener`|`onKey(View v, int keyCode, KeyEvent event)`|
|`setOnTouchListener`|`onTouch(View v, MotionEvent event)`|

---

## 🧼 Structure recommandée (clean code)

### Variables

```java
// Données
private int compteur = 0;

// Vues
private TextView compteurView;
private Button boutonAjoutView;
```

### Initialisation

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    compteurView = findViewById(R.id.compteurView);
    boutonAjoutView = findViewById(R.id.boutonAjoutView);

    boutonAjoutView.setOnClickListener(v -> {
        compteur++;
        miseAJourGraphique();
    });

    miseAJourGraphique();
}

private void miseAJourGraphique() {
    compteurView.setText(String.valueOf(compteur));
}
```

---

## 📚 Docs utiles

- [Documentation officielle Android](https://developer.android.com/guide)
    
- [Layouts & UI](https://developer.android.com/guide/topics/ui/)
    
- [Javadoc View](https://developer.android.com/reference/android/view/View)
    

---

Si tu veux, je peux aussi te faire un mémo "starter pack" pour un petit projet Android propre !