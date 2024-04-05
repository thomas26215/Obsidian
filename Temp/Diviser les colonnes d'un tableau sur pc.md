```CSS
.grid{
	display: grid;
	gap: 10px;
	grid-template-colummns: 1fr;
}
.grid article{
	background-color: silver;
}
@media screen and (min-width: 1025px){
	.grid{
		grid-template-columns: 1fr 1fr;
	}
}
```

---
**Links :**
[[Adapter le site en fonction des appareils en HTML]]
[[CSS - Des tableaux visuels avec les Grids !]]