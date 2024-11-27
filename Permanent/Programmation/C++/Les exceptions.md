Création d'une exception :
```cpp
//Fichier .h
#include <stdexcept>
#include <string>

class NomException : public std::domain_error {
public:
NomException() : std::domain_error("Message d'erreur") {}
};
```
