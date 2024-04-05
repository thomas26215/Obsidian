1
```SQL
CREATE USER invite WITH password 'invite';
CREATE USER Arthur WITH password 'Arthur';
CREATE USER Lancelot WITH password 'Lancelot';
```
2
```SQL
CREATE ROLE chefs;
GRANT chefs to arthur, lancelot;
```
3
```SQL
REVOKE CONNECT ON DATABASE quete FROM PUBLIC;
GRANT CONNECT ON DATABASE quete [TO invite, lancelot, arthur | TO invite, chefs];
```
4
```SQL
GRANT SELECT ON graal TO PUBLIC;
```
5
```SQL
GRANT ALL ON chevalier, grall To Chefs;;
REVOKE UPDATE, DELETE ON chevalier, graal To chefs FROM Chefs;
GRANt UPDATE (pays_naissance) ON chevaliers To chefs;
GRANT UPDATE (authentique, découvreur) ON graal To chefs;
GRANT SELECT, UPDATE (authentique, découvreur) ON graal To chefs;
GRANT SELECT, UPDATE (pays_naissance) ON chevaliers TO chefs;
```