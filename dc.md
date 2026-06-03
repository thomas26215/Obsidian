```
flowchart LR
    PY["🐍 Objet Python<br/><b>ProtocolParameters</b><br/><i>arbre d'objets typés en mémoire</i>"]
    JSON["📄 JSON<br/><b>protocol.json</b><br/><i>fichier / réponse API</i>"]
    PY == "get_attributes_as_dict()<br/>— sérialisation —" ==> JSON
    JSON == "set_attributes_from_dict()<br/>— désérialisation —" ==> PY

```