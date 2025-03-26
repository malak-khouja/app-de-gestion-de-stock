# 📦 Gestion des Commandes  

Ce projet est une application de gestion des commandes utilisant **Java**, **JavaFX**, et **PostgreSQL**.  
Il permet de gérer les clients, leurs commandes et les articles commandés.

---

## 📌 Objectifs  

- Implémenter un système de gestion des clients, commandes et articles.  
- Utiliser la **Programmation Orientée Objet (POO)** avec Java.  
- Implémenter une **interface graphique** avec **JavaFX**.  
- Gérer les données avec **PostgreSQL** et **JDBC**.  

---

## 📁 Structure du Projet  

```
📂 GestionCommandes
 ┣ 📂 src
 ┃ ┣ 📂 models
 ┃ ┃ ┣ 📜 Client.java
 ┃ ┃ ┣ 📜 Commande.java
 ┃ ┃ ┣ 📜 Article.java
 ┃ ┃ ┗ 📜 Operation.java
 ┃ ┣ 📂 database
 ┃ ┃ ┣ 📜 DatabaseConnection.java
 ┃ ┃ ┣ 📜 ArticleDb.java
 ┃ ┃ ┗ 📜 CommandeDb.java
 ┃ ┣ 📂 ui
 ┃ ┃ ┗ 📜 MainApp.java
 ┃ ┗ 📜 Main.java
 ┣ 📂 resources
 ┣ 📜 README.md
 ┣ 📜 GestionCommandes.sql
 ┗ 📜 GestionCommandes.iml
```

---

## ⚙️ Fonctionnalités  

✔ **Gestion des Clients** : Ajouter, modifier et afficher les clients.  
✔ **Gestion des Commandes** : Enregistrer une commande, calculer le total TTC, afficher les commandes par client.  
✔ **Gestion des Articles** : Ajouter des articles, afficher les articles commandés par client et date.  
✔ **Connexion à PostgreSQL** : CRUD sur les articles et commandes.  
✔ **Interface graphique avec JavaFX** : Interface de saisie des articles.  

---

## 🛠️ Installation  

### 1️⃣ Prérequis  

- **Java 11+**  
- **PostgreSQL** installé  
- **JavaFX** installé  

### 2️⃣ Cloner le projet  

```sh
git clone https://github.com/ton-repo/GestionCommandes.git
cd GestionCommandes
```

### 3️⃣ Configurer la base de données  

- Importer `GestionCommandes.sql` dans PostgreSQL.  
- Modifier `DatabaseConnection.java` avec vos paramètres :  

```java
private static final String URL = "jdbc:postgresql://localhost:5432/gestion";
private static final String USER = "votre_user";
private static final String PASSWORD = "votre_mot_de_passe";
```

### 4️⃣ Exécuter le projet  

- Compiler le projet :  

```sh
javac -d bin src/**/*.java
```

- Exécuter l'application :  

```sh
java -cp bin Main
```

---

## 📊 Diagramme UML  

📌 **Diagramme de Classe**  

```plaintext
+-----------------+
|     Client      |
+-----------------+
| - codeClient    |
| - rs            |
| - adresse       |
| - telephone     |
+-----------------+
| + getClients()  |
| + addClient()   |
+-----------------+

+-----------------+
|    Commande     |
+-----------------+
| - numCmd        |
| - dateCmd       |
| - totalHT       |
| - totalTTC      |
+-----------------+
| + afficheCommande(codeClient) |
+-----------------+

+-----------------+
|    Article      |
+-----------------+
| - codeArticle   |
| - libelle       |
| - qte          |
| - prixHT        |
+-----------------+
| + afficheArticle(codeClient, date) |
+-----------------+

+-----------------+
|    Opération    |
+-----------------+
| + commander(dateCmd, codeArticle, qte) |
| + prixCommande(prixTTC, prixLettre)    |
+-----------------+
```

---

## 📂 Base de Données  

📌 **Tables :**  

```sql
CREATE TABLE Client (
    codeClient VARCHAR(50) PRIMARY KEY,
    rs VARCHAR(100),
    adresse VARCHAR(255),
    telephone VARCHAR(20)
);

CREATE TABLE Commande (
    numCmd VARCHAR(50) PRIMARY KEY,
    dateCmd DATE,
    totalHT DECIMAL(10,2),
    totalTTC DECIMAL(10,2),
    codeClient VARCHAR(50),
    FOREIGN KEY (codeClient) REFERENCES Client(codeClient)
);

CREATE TABLE Article (
    codeArticle VARCHAR(50) PRIMARY KEY,
    libelle VARCHAR(100),
    qte INT,
    prixHT DECIMAL(10,2)
);

CREATE TABLE Commande_Article (
    numCmd VARCHAR(50),
    codeArticle VARCHAR(50),
    qte INT,
    PRIMARY KEY (numCmd, codeArticle),
    FOREIGN KEY (numCmd) REFERENCES Commande(numCmd),
    FOREIGN KEY (codeArticle) REFERENCES Article(codeArticle)
);
```

---

## 🏗️ Développement  

### 🔹 Classes Principales  

- **Client.java** : Représente un client et ses informations.  
- **Commande.java** : Stocke les commandes et calcule les totaux.  
- **Article.java** : Contient les articles et leur gestion.  
- **Operation.java** : Interface contenant les méthodes `commander()` et `prixCommande()`.  

### 🔹 Base de Données  

- **DatabaseConnection.java** : Gère la connexion PostgreSQL.  
- **ArticleDb.java** : Contient les opérations CRUD sur les articles.  
- **CommandeDb.java** : Gestion des commandes.  

### 🔹 Interface Graphique  

- **MainApp.java** : Interface graphique pour la saisie des articles en **JavaFX**.  

---

## 🚀 Auteur  

👤 **Nom** : *Malak Khouja*  
🎓 *Étudiante en Mathématiques et Informatique*  
💻 Passionnée par **le développement logiciel et la data science**  

---

## 📜 Licence  

Ce projet est sous licence **MIT**. Vous pouvez l'utiliser librement, mais toute contribution est la bienvenue ! 🚀
