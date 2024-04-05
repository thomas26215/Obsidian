**Code en une fonction :**
```Java
public static void triBulles(ArrayList<Integer> v){
	int j;
	int i = 0
	while(j < v.size()-1){
		j = v.size()-1;
		while(j > i){
			if(v.get(j) < v.get(j-1)){
				int temporaire = v.get(j);
				v.set(j, v.get(j-1));
				v.set(j-1, temporaire);
			}
			j = j-1;
		}
		i += 1
	}
}
```

---
**Links :**
[[Tri à bulle]]
