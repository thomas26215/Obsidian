On utilise un ETL quand le volume de données est trop importante. Ainsi, on va d'abord les charger, puis les transformer. Cela permet de faire la programmation parallèle.
 En fait, une fois que les données ont été chargées, on peut les transformer par groupe, donc on peut utiliser plusieurs processus en même temps contrairement à [[ETL : Extract, Transform and Load|ETL]] qui lui va les transformer une par une

