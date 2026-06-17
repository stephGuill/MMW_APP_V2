MCD - MLD - MPD

des schémas propres (type MCD/MLD/MPD) en format texte clair ou Mermaid 
1. MCD (Modèle Conceptuel de Données)
Entités + relations (niveau métier)

Entités principales :

User
Role
Question
Game
UserProgress
Reward
RewardEvent
EmailToken
FriendInvite
Relations :

User ↔ Role (N:N via user_roles)
User → Game (1:N)
User → UserProgress (1:1)
User ↔ Reward (N:N avec balance)
User → RewardEvent (1:N)
User → EmailToken (1:N)
User → FriendInvite (1:N)
Version Mermaid (tu peux coller ça dans https://mermaid.live) :erDiagram

USER ||--o{ GAME : plays
USER ||--|| USER_PROGRESS : has
USER ||--o{ USER_REWARD_EVENTS : earns
USER ||--o{ EMAIL_VERIFICATION_TOKENS : verifies
USER ||--o{ FRIEND_INVITES : sends

USER }o--o{ ROLE : has

USER ||--o{ USER_REWARD_BALANCES : owns
REWARD_CATALOG ||--o{ USER_REWARD_BALANCES : defines

REWARD_CATALOG ||--o{ USER_REWARD_EVENTS : logs

USER {
  int id
  string username
  string email
}

ROLE {
  int id
  string code
}

GAME {
  int id
  int score
}

QUESTION {
  int id
  int level
}

REWARD_CATALOG {
  int id
  string code
}


 

1. MCD (Modèle Conceptuel de Données)
Entités + relations (niveau métier)

Entités principales :

User
Role
Question
Game
UserProgress
Reward
RewardEvent
EmailToken
FriendInvite
Relations :

User ↔ Role (N:N via user_roles)
User → Game (1:N)
User → UserProgress (1:1)
User ↔ Reward (N:N avec balance)
User → RewardEvent (1:N)
User → EmailToken (1:N)
User → FriendInvite (1:N)
Version Mermaid (tu peux coller ça dans https://mermaid.live) :

mermaid
Expand
Show Code


100%



1. MLD (Modèle Logique de Données)
Ici on est proche du SQL, mais simplifié :

users(id, username, email, password_hash, role, best_score, ...)

roles(id, code, label)

user_roles(user_id, role_id)

questions(id, level, question, options, correct_option)

games(id, user_id, score, level_reached, duration)

user_progress(user_id, current_level, max_level, total_score, ...)

reward_catalog(id, code, label)

user_reward_balances(user_id, reward_id, quantity)

user_reward_events(id, user_id, reward_id, delta, reason)

email_verification_tokens(id, user_id, token_hash, expires_at)

friend_invites(id, sender_user_id, recipient_email, token_hash)

3. MPD (Modèle Physique de Données)
C’est quasiment mon SQL actuel  (il est déjà très propre)

Points intéressants :

InnoDB 
FK bien définies 
index optimisés 
contraintes CHECK 
Améliorations possibles :

ajouter index sur users(role)
ajouter index sur games(created_at)
normaliser users.role (déjà redondant avec user_roles)



