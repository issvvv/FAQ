## Keycloak Commands FAQ

### General Commands
- **`kcadm.sh get realms --server http://localhost:8080/`** — List all realms.
- **`kcadm.sh create realms -s realm=new-realm -s enabled=true -o`** — Create a new realm (e.g., `new-realm`).

### Credentials Management
- **`kcadm.sh config credentials --server http://localhost:8080/ --realm new-realm --user admin --client admin`** — Set credentials for the `new-realm` realm.
- **`kcadm.sh config credentials --config ./keycloak/.keycloak/kcadm.config --server http://localhost:8080 --realm master --user admin`** — Generate a config file for Keycloak service.

### Example Usage
To create a new realm and configure credentials:
1. Set credentials for the `master` realm:
```cmd
kcadm.sh config credentials --server http://localhost:8080/ --realm master --user admin
```

2. Create a new realm:
```cmd
kcadm.sh create realms -s realm=demorealm -s enabled=true -o
```
