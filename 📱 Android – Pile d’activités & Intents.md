# 📲 Android – Pile d’activités & Intents (R4 Real 11)

## 📚 1. Pile d’activités (Back Stack)

- Une app Android = plusieurs **`Activity`**, gérées dans une **pile (back stack)**.
    
- Chaque **tâche (task)** = 1 processus Android indépendant avec sa propre pile.
    
- Quand une activité est lancée → ajoutée **au sommet de la pile**.
    

### 🎯 Activité principale (dans le `AndroidManifest.xml`)

```xml
<activity android:name=".MainActivity" android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

---

## 🧭 2. Intents (Navigation entre activités)

### ➕ Créer une activité (depuis une autre activité)

```java
Intent intent = new Intent(this, TargetActivity.class);
startActivity(intent);
```

> `this` = nomDeLActivity.this si dans un listener

---

## 📩 3. Passage de données entre activités

### ➡️ Envoi

```java
Intent intent = new Intent(this, HelloActivity.class);
intent.putExtra(HelloActivity.PRENOM_KEY, "Alice");
startActivity(intent);
```

### ⬅️ Réception (`HelloActivity.java`)

```java
public static final String PRENOM_KEY = "prenom_key";

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_hello);

    String prenom = getIntent().getStringExtra(PRENOM_KEY);
}
```

---

## 🧳 4. Types de données (`Intent.putExtra(...)`)

|Type|Envoi|Récupération|
|---|---|---|
|`int`|`putExtra("key", 42)`|`getIntExtra("key", 0)`|
|`String[]`|`putExtra("key", new String[]{"A", "B"})`|`getStringArrayExtra("key")`|
|`float`|`putExtra("key", 3.14f)`|`getFloatExtra("key", 0.0f)`|
|`Parcelable`|`putExtra("key", monObjet)`|`getParcelableExtra("key")`|

---

## 📦 5. Objet complexe : `Parcelable`

```java
public class Resultat implements Parcelable {
    private int nombreVictoire, nombreEgalite, nombreDefaite;

    public Resultat() {}

    protected Resultat(Parcel in) {
        nombreVictoire = in.readInt();
        nombreEgalite = in.readInt();
        nombreDefaite = in.readInt();
    }

    @Override
    public void writeToParcel(Parcel parcel, int flags) {
        parcel.writeInt(nombreVictoire);
        parcel.writeInt(nombreEgalite);
        parcel.writeInt(nombreDefaite);
    }

    public static final Parcelable.Creator<Resultat> CREATOR = ...
}
```

---

## 🔄 6. Obtenir un **résultat** d’une activité (ActivityResultLauncher)

### 🔧 1. Déclarer dans l’activité A

```java
ActivityResultLauncher<Intent> activityResultLauncher =
    registerForActivityResult(new ActivityResultContracts.StartActivityForResult(),
        result -> {
            if (result.getResultCode() == RESULT_OK) {
                Intent data = result.getData();
                String message = data.getStringExtra("clé");
            }
        });
```

### 🚀 2. Lancer l’activité B

```java
Intent intent = new Intent(this, ActivityB.class);
activityResultLauncher.launch(intent);
```

### 🛑 3. Côté activité B (renvoi d’un résultat)

```java
Intent retour = new Intent();
retour.putExtra("clé", "valeur");
setResult(RESULT_OK, retour);
finish(); // ferme l'activité
```

---

## 🚩 7. Flags importants (`Intent.addFlags(...)`)

|Flag|Description|
|---|---|
|`FLAG_ACTIVITY_CLEAR_TOP`|Nettoie les activités au-dessus de celle ciblée si elle existe déjà. Appelle `onNewIntent()`|
|`FLAG_ACTIVITY_REORDER_TO_FRONT`|Ramène l’activité ciblée au sommet si déjà instanciée|
|`FLAG_ACTIVITY_SINGLE_TOP`|Si l’activité ciblée est déjà au sommet → pas de nouvelle instance|

```java
Intent intent = new Intent(this, MainActivity.class);
intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
startActivity(intent);
```

---

## 🔗 Ressources utiles

- [Tasks & Back Stack](https://developer.android.com/guide/components/tasks-and-back-stack)
    
- [Intents & Filters](https://developer.android.com/guide/components/intents-filters)
    
- [Intent reference](https://developer.android.com/reference/android/content/Intent)
    
# Envoyer une liste d'items

Pour **envoyer une liste d’objets avec un `Intent`** en Android, tu peux procéder de différentes manières selon le type d’objet de ta liste.

---

## ✅ 1. **Liste de types primitifs ou simples (`String`, `Integer`, etc.)**

### 🔁 Exemple avec `ArrayList<String>` :

**Activité A – envoi**

```java
Intent intent = new Intent(this, ActiviteB.class);
ArrayList<String> maListe = new ArrayList<>();
maListe.add("pomme");
maListe.add("banane");

intent.putStringArrayListExtra("fruits", maListe);
startActivity(intent);
```

**Activité B – réception**

```java
ArrayList<String> fruits = getIntent().getStringArrayListExtra("fruits");
```

---

## ✅ 2. **Liste d’objets personnalisés**

L’objet doit :

- Implémenter `Serializable` **ou** `Parcelable`
    

### a. 🔸 Avec `Serializable` (plus simple)

**Ton objet :**

```java
public class Produit implements Serializable {
    String nom;
    int prix;

    public Produit(String nom, int prix) {
        this.nom = nom;
        this.prix = prix;
    }
}
```

**Activité A – envoi :**

```java
ArrayList<Produit> listeProduits = new ArrayList<>();
listeProduits.add(new Produit("Stylo", 2));
listeProduits.add(new Produit("Classeur", 4));

Intent intent = new Intent(this, ActiviteB.class);
intent.putExtra("produits", listeProduits);
startActivity(intent);
```

**Activité B – réception :**

```java
ArrayList<Produit> produits = (ArrayList<Produit>) getIntent().getSerializableExtra("produits");
```

---

### b. 🧱 Avec `Parcelable` (plus performant, recommandé pour gros volumes)

**Ton objet :**

```java
public class Produit implements Parcelable {
    String nom;
    int prix;

    public Produit(String nom, int prix) {
        this.nom = nom;
        this.prix = prix;
    }

    protected Produit(Parcel in) {
        nom = in.readString();
        prix = in.readInt();
    }

    public static final Creator<Produit> CREATOR = new Creator<Produit>() {
        @Override
        public Produit createFromParcel(Parcel in) {
            return new Produit(in);
        }

        @Override
        public Produit[] newArray(int size) {
            return new Produit[size];
        }
    };

    @Override
    public void writeToParcel(Parcel dest, int flags) {
        dest.writeString(nom);
        dest.writeInt(prix);
    }

    @Override
    public int describeContents() {
        return 0;
    }
}
```

**Envoi (même que Serializable) :**

```java
Intent intent = new Intent(this, ActiviteB.class);
intent.putParcelableArrayListExtra("produits", listeProduits);
startActivity(intent);
```

**Réception :**

```java
ArrayList<Produit> produits = getIntent().getParcelableArrayListExtra("produits");
```

---

Souhaites-tu un exemple complet avec interface et affichage via un `RecyclerView` aussi ?