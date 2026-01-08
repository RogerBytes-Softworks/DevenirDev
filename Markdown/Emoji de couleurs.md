| Tables   |      Are      |  Cool |
| -------- | :-----------: | ----: |
| col 1 is | left-aligned  | $1600 |
| col 2 is |   centered    |   $12 |
| col 3 is | right-aligned |    $1 |


-------------------|--------------------------------------|
| `user_id`              | UUID          | Identifiant unique de l'utilisateur                                         | PK, NOT NULL                         |
| `email`                | VARCHAR(255)  | Adresse email de l'utilisateur                                              | UNIQUE, NOT NULL                     |
| `password_hash`        | VARCHAR(255)  | Hash du mot de passe (BCrypt/Argon2)                                        | NOT NULL                             |
| `first_name`           | VARCHAR(100)  | Prénom de l'utilisateur                                                     | NOT NULL                             |
| `last_name`            | VARCHAR(100)  | Nom de l'utilisateur                                                        | NOT NULL                             |
| `phone`                | VARCHAR(20)   | Numéro de téléphone                                                        | Optional                              |
| `role_id`              | INT           | Rôle de l'utilisateur (référence à `Roles`)                                | FK, NOT NULL                         |
| `company_id`           | UUID          | ID de l'entreprise cliente (pour les auditeurs/clients)                     | FK (NULL si interne)                 |
| `last_login`           | DATETIME      | Date et heure du dernier login                                              | Optional                              |
| `is_active`            | BOOLEAN       | Statut actif/inactif de l'utilisateur                                       | DEFAULT TRUE                         |
| `created_at`           | DATETIME      | Date de création du compte                                                  | NOT NULL, DEFAULT NOW()              |
| `updated_at`           | DATETIME      | Date de dernière mise à jour                                                | NOT NULL, DEFAULT NOW()              |