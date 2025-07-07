# 🎵 4NAP Festival - Architecture Firebase

## 🎯 Vue d'ensemble

Architecture complète et professionnelle pour gérer dynamiquement les artistes du festival 4NAP avec Firebase (Firestore + Storage + Auth).

## 🏗️ Architecture Technique

### Backend - Firebase
- **Firestore** : Base de données pour stocker les informations des artistes
- **Storage** : Stockage des images des artistes  
- **Authentication** : Système de connexion sécurisé pour l'admin

### Structure de données Firestore

**Collection : `artistes`**
```javascript
{
  nom: "string",           // Nom de l'artiste
  styleMusical: "string",  // Genre musical
  jour: "string",          // "11", "12", ou "13" (juillet)
  heure: "string",         // Format "HH:MM"
  description: "string",   // Description de l'artiste
  imageUrl: "string",      // URL de l'image (Firebase Storage)
  lienSocial: "string"     // Lien Instagram/Social (optionnel)
}
```

## 🖥️ Pages et Fonctionnalités

### 1. Dashboard Admin (`/admin.html`)
**Accès** : Protégé par Firebase Authentication

**Fonctionnalités** :
- ✅ Interface ultra-clean style Apple, responsive
- ✅ Authentification email/mot de passe
- ✅ Onglets par jour (11, 12, 13 juillet + "Tous")
- ✅ Affichage des artistes par jour
- ✅ Ajout d'artistes avec formulaire complet
- ✅ Modification/suppression des artistes existants
- ✅ Upload d'images (stockées dans Firebase Storage)
- ✅ Prévisualisation d'images en temps réel

**Design** :
- Interface minimaliste façon Apple
- Animations fluides
- Cards avec hover effects
- Modal responsive pour l'édition
- Loading states professionnels

### 2. Page Programmation Complète (`/programmation-complete/index.html`)
**Fonctionnalités** :
- ✅ Chargement dynamique de tous les artistes depuis Firestore
- ✅ Filtrage en temps réel par jour (Vendredi/Samedi/Dimanche)
- ✅ Cards responsive avec design cohérent
- ✅ Animations GSAP fluides
- ✅ Tri automatique par jour puis heure

**Design** :
- Cards avec badges colorés par jour
- Icônes dynamiques selon le genre musical
- Layout grid responsive
- Couleurs cohérentes avec la charte graphique

### 3. Page Sono Mondiale (`/programmation/sono-mondiale.html`)
**Fonctionnalités** :
- ✅ Affichage exclusif des artistes du 11 juillet
- ✅ Section dédiée intégrée harmonieusement
- ✅ Design spécifique au thème "Sono Mondiale"
- ✅ Cards détaillées avec description et liens sociaux

**Design** :
- Background gris clair pour distinction
- Bordures oranges (couleur Sono Mondiale)
- Cards plus grandes avec plus d'informations
- Animations d'apparition au scroll

## 🚀 Installation et Configuration

### 1. Configuration Firebase
Le projet est déjà configuré avec :
```javascript
const firebaseConfig = {
  apiKey: "AIzaSyCK20ovvLNY9lBSr7FotjXPU1mwHsg8pnk",
  authDomain: "nap-festival.firebaseapp.com",
  projectId: "nap-festival",
  storageBucket: "nap-festival.firebasestorage.app",
  // ...
};
```

### 2. Règles de Sécurité Firestore (à configurer)
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Lecture publique pour les artistes (pour les pages publiques)
    match /artistes/{document} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

### 3. Règles de Sécurité Storage (à configurer)
```javascript
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /artists/{allPaths=**} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

## 🔐 Gestion des Utilisateurs Admin

### Création d'un compte admin
1. Aller sur [Firebase Console](https://console.firebase.google.com/)
2. Projet : `nap-festival`
3. Authentication > Users > Add user
4. Créer un utilisateur avec email/mot de passe

### Connexion
- URL : `/admin.html`
- Utiliser les identifiants créés dans Firebase Auth

## 📱 Responsive Design

Toutes les pages sont entièrement responsive :

**Mobile (< 768px)** :
- Navigation hamburger
- Cards en 2 colonnes (programmation complète)
- Card unique (sono mondiale)
- Footer accordion
- Tabs avec scroll horizontal

**Tablet (768px - 1024px)** :
- Layout adapté
- Cards en grille flexible

**Desktop (> 1024px)** :
- Layout complet
- Toutes les fonctionnalités visibles

## 🎨 Système de Couleurs

**Par jour** :
- Vendredi (11 juillet) : `#ff6b35` (Orange)
- Samedi (12 juillet) : `#4CAF50` (Vert)  
- Dimanche (13 juillet) : `#2196F3` (Bleu)

**Sono Mondiale** : `#ff9a56` (Orange clair)

## 🔧 Fonctionnalités Techniques

### Animations GSAP
- Animations d'apparition au scroll
- Transitions fluides entre les états
- Stagger effects pour les grilles
- Loading animations

### Gestion d'État
- Filtrage en temps réel sans rechargement
- Cache local des données artistes
- Gestion d'erreurs robuste
- Loading states visuels

### Performance
- Chargement lazy des images
- Queries optimisées Firestore
- Animations GPU-accelerated
- Code modulaire et propre

## 📝 Utilisation

### Pour ajouter un artiste :
1. Se connecter sur `/admin.html`
2. Cliquer sur "+ Ajouter un artiste"
3. Remplir le formulaire
4. Uploader une image
5. Valider

### Pour modifier un artiste :
1. Cliquer sur "Modifier" sur la card artiste
2. Modifier les informations
3. Valider les changements

### Les changements apparaissent immédiatement :
- Dashboard admin
- Page programmation complète  
- Page sono mondiale (pour les artistes du 11 juillet)

## 🛡️ Sécurité

- Dashboard protégé par Firebase Auth
- Règles Firestore/Storage configurables
- Validation côté client et serveur
- Gestion d'erreurs complète

## 🚨 Notes Importantes

1. **Images** : Stockées dans Firebase Storage sous `/artists/`
2. **Jours** : Format string "11", "12", "13" (pas de Date object)
3. **Responsive** : Toutes les pages sont mobile-first
4. **Animations** : GSAP requis pour le bon fonctionnement
5. **Firebase** : Configuration déjà en place, prête à l'emploi

## 🎯 Roadmap Futur

- [ ] Filtrage par genre musical
- [ ] Recherche textuelle
- [ ] Export de la programmation
- [ ] Notifications push
- [ ] Mode sombre
- [ ] Multi-langue

---

**Made with ✌️ by Noa Giannone** 