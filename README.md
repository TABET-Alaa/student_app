# Student App - Gestion de Produits

Ce projet est une application Spring Boot simple pour gérer des **produits**, en utilisant **Spring Data JPA** et une base de données **MySQL**.

## Fonctionnalités

- Ajouter des produits
- Consulter tous les produits
- Consulter un produit spécifique
- Rechercher des produits par mot-clé
- Mettre à jour un produit
- Supprimer un produit

## Détails Techniques

### Entité `Product`

L'application utilise une entité JPA `Product` avec les attributs suivants :

- `id` (`Long`) — Identifiant unique
- `name` (`String`) — Nom du produit
- `price` (`double`) — Prix du produit
- `quantity` (`int`) — Quantité en stock

### Configuration

L'unité de persistance est configurée dans le fichier `application.properties`.  
Exemple de configuration pour H2 :

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.h2.console.enabled=true
````
## Repository

Le `ProductRepository` est une interface qui étend `JpaRepository<Product, Long>`.  
Elle permet de réaliser facilement des opérations CRUD sur les produits sans avoir besoin d'implémenter quoi que ce soit.

### Exemple de Repository

```java
import org.springframework.data.jpa.repository.JpaRepository;
import java.util.List;

public interface ProductRepository extends JpaRepository<Product, Long> {
    // Recherche les produits dont le nom contient un mot-clé
    List<Product> findByNameContains(String keyword);
}
```