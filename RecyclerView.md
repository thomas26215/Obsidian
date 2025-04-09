## 📋 `RecyclerView` en Android – Note complète

### 🔹 Pourquoi `RecyclerView` ?

`RecyclerView` est une version améliorée de `ListView` :

- Meilleure performance (recyclage des vues)
    
- Plus flexible (layouts horizontaux, grilles, etc.)
    
- Supporte les animations et interactions (glisser/supprimer, etc.)
    

---

## 🔧 Étapes pour utiliser un `RecyclerView`

### 1. Ajouter la dépendance dans `build.gradle`

```gradle
dependencies {
    implementation 'androidx.recyclerview:recyclerview:1.3.2'
}
```

---

### 2. Créer le layout de l’activité avec `RecyclerView`

**res/layout/activity_main.xml**

```xml
<androidx.recyclerview.widget.RecyclerView
    android:id="@+id/recyclerView"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="16dp"
/>
```

---

### 3. Créer le layout XML pour une ligne (item)

**res/layout/item_ligne.xml**

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="horizontal"
    android:padding="12dp">

    <TextView
        android:id="@+id/textItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Exemple"
        android:textSize="18sp" />
</LinearLayout>
```

---

### 4. Créer une classe `Adapter`

**Exemple : MyAdapter.java**

```java
public class MyAdapter extends RecyclerView.Adapter<MyAdapter.MyViewHolder> {

    private List<String> donnees;
    private Context context;

    public MyAdapter(Context context, List<String> donnees) {
        this.context = context;
        this.donnees = donnees;
    }

    public static class MyViewHolder extends RecyclerView.ViewHolder {
        TextView textItem;

        public MyViewHolder(View itemView) {
            super(itemView);
            textItem = itemView.findViewById(R.id.textItem);
        }
    }

    @Override
    public MyViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(context).inflate(R.layout.item_ligne, parent, false);
        return new MyViewHolder(view);
    }

    @Override
    public void onBindViewHolder(MyViewHolder holder, int position) {
        String element = donnees.get(position);
        holder.textItem.setText(element);
    }

    @Override
    public int getItemCount() {
        return donnees.size();
    }
}
```

---

### 5. Utiliser le `RecyclerView` dans ton activité

**MainActivity.java**

```java
public class MainActivity extends AppCompatActivity {

    RecyclerView recyclerView;
    MyAdapter adapter;
    List<String> listeDonnees;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        recyclerView = findViewById(R.id.recyclerView);
        listeDonnees = new ArrayList<>();

        // Exemple : remplir la liste
        for (int i = 1; i <= 20; i++) {
            listeDonnees.add("Élément " + i);
        }

        // Initialisation du RecyclerView
        adapter = new MyAdapter(this, listeDonnees);
        recyclerView.setLayoutManager(new LinearLayoutManager(this));
        recyclerView.setAdapter(adapter);
    }
}
```

---

## ✅ Résumé des fichiers nécessaires

|Type de fichier|Nom|
|---|---|
|Layout activité|`activity_main.xml`|
|Layout item|`item_ligne.xml`|
|Adapter Java|`MyAdapter.java`|
|Activité Java|`MainActivity.java`|

---

Si tu veux une version **Kotlin**, avec **RecyclerView + boutons cliquables**, ou en mode **grille (GridLayout)**, je peux te faire une variante 😄. Tu veux que je t’en prépare une ?