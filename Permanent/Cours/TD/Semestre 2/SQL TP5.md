10)

```SQL
CREATE OR REPLACE FUNCTION name_function()
RETURNS TRIGGER AS $$
	
BEGIN
	IF EXISTS (SELECT * FROM chefDeBord c WHERE new.numadh = c.numadh AND new.numcourse = c.numcourse) THEN
		RAISE EXCEPTION 'Vous ne pouvez pas mettre dans equipier car déja présent dans chefdebord dans la même course !';
	END IF;

	IF EXISTS (SELECT count(SELECT * FROM EQUIPIER) FROM )


	IF EXISTS (SELECT count(*) as nombre_personnes from equipier e where (select nbplaces from bateau b) >= (nombre_personnes+1) and e.numbat = b.numbat AND e.numcourse = e.numcourse) THEN
		RAISE EXCEPTION 'Taille du bateau trop petite';
	END IF;


	RETURN {OLD/NEW};
END;
$$ LANGUAGE plpgsql;


/* Crée le trigger qui déclenchera la fonction une fois qu'il sera appelé (Trigger) */

CREATE OR REPLACE TRIGGER
name_trigger
AFTER UPDATE OR INSERT
ON equipier
FOR EACH ROW
EXECUTE FUNCTION name_function();
```

13)

```SQL
CREATE OR REPLACE FUNCTION name_function()
RETURNS TRIGGER AS $$
	
BEGIN
	IF NOT EXISTS (SELECT * FROM course c WHERE new.dateregate > c.datedebut AND new.dateregate < c.datefin AND new.numcourse = c.numcourse) THEN
		RAISE EXCEPTION 'Pas sur la même date qu''une course'
	END IF;


	RETURN NEW;
END;
$$ LANGUAGE plpgsql;


/* Crée le trigger qui déclenchera la fonction une fois qu'il sera appelé (Trigger) */

CREATE OR REPLACE TRIGGER
name_trigger
AFTER UPDATE OR INSERT
ON equipier
FOR EACH ROW
EXECUTE FUNCTION name_function();

```