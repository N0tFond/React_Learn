### Méthode 2: Vite (plus rapide et plus léger)

```shellscript
npm create vite@latest mon-app-react -- --template react
cd mon-app-react
npm install
npm run dev
```

### Structure de base d'un projet React

```plaintext
mon-app-react/
  ├── node_modules/
  ├── public/
  │   ├── index.html
  │   └── favicon.ico
  ├── src/
  │   ├── App.js
  │   ├── index.js
  │   ├── components/
  │   └── assets/
  ├── package.json
  └── README.md
```

---

## 3. Composants et JSX

### Qu'est-ce que JSX?

JSX est une extension syntaxique de JavaScript qui ressemble à du HTML mais avec la puissance de JavaScript. Il est transformé en JavaScript standard par Babel.

```jsx
// Ceci est du JSX
const element = <h1>Bonjour, monde!</h1>;

// Il est transformé en ceci par Babel
// const element = React.createElement('h1', null, 'Bonjour, monde!');
```

### Types de composants

#### Composants fonctionnels

```jsx
import React from "react";

// Composant fonctionnel (recommandé)
function Salutation(props) {
  return <h1>Bonjour, {props.nom}!</h1>;
}

export default Salutation;
```

#### Composants de classe (moins utilisés dans le React moderne)

```jsx
import React, { Component } from "react";

// Composant de classe
class Salutation extends Component {
  render() {
    return <h1>Bonjour, {this.props.nom}!</h1>;
  }
}

export default Salutation;
```

### Composition de composants

```jsx
import React from "react";
import Salutation from "./Salutation";
import Profil from "./Profil";

function App() {
  return (
    <div>
      <Salutation nom="Marie" />
      <Profil utilisateur="marie123" />
    </div>
  );
}

export default App;
```

---

## 4. Props et État (State)

### Props

Les props sont des données passées d'un composant parent à un composant enfant. Elles sont en lecture seule.

```jsx
import React from "react";

// Composant parent
function App() {
  return <Carte titre="Mon titre" contenu="Mon contenu" />;
}

// Composant enfant
function Carte(props) {
  return (
    <div className="carte">
      <h2>{props.titre}</h2>
      <p>{props.contenu}</p>
    </div>
  );
}

export default App;
```

### État (State)

L'état est géré à l'intérieur d'un composant et peut changer au fil du temps.

```jsx
import React, { useState } from "react";

function Compteur() {
  // Déclaration d'un état avec useState
  const [compte, setCompte] = useState(0);

  return (
    <div>
      <p>Vous avez cliqué {compte} fois</p>
      <button onClick={() => setCompte(compte + 1)}>Cliquez ici</button>
    </div>
  );
}

export default Compteur;
```

### Différence entre Props et State

| Props                                       | State                                          |
| ------------------------------------------- | ---------------------------------------------- |
| Passées au composant                        | Défini dans le composant                       |
| Immuables                                   | Peut être modifié                              |
| Accessibles en lecture seule                | Peut être mis à jour avec setState ou setX     |
| Peuvent être passées aux composants enfants | Généralement non passé aux enfants directement |

---

## 5. Gestion des événements

### Syntaxe des événements en React

```jsx
import React, { useState } from "react";

function Bouton() {
  const [estActif, setEstActif] = useState(false);

  // Gestionnaire d'événement
  function handleClick() {
    setEstActif(!estActif);
  }

  return (
    <button onClick={handleClick} className={estActif ? "actif" : "inactif"}>
      {estActif ? "Actif" : "Inactif"}
    </button>
  );
}

export default Bouton;
```

### Événements courants

- `onClick`: Déclenché lors d'un clic
- `onChange`: Déclenché lorsqu'une valeur change (formulaires)
- `onSubmit`: Déclenché lors de la soumission d'un formulaire
- `onMouseOver`: Déclenché lorsque la souris passe au-dessus
- `onKeyDown`: Déclenché lorsqu'une touche est enfoncée

### Passage de paramètres aux gestionnaires d'événements

```jsx
import React from "react";

function ListeBoutons() {
  // Avec paramètre
  function handleClick(id) {
    console.log("Bouton cliqué:", id);
  }

  return (
    <div>
      {/* Utilisation d'une fonction fléchée pour passer des paramètres */}
      <button onClick={() => handleClick(1)}>Bouton 1</button>
      <button onClick={() => handleClick(2)}>Bouton 2</button>
      <button onClick={() => handleClick(3)}>Bouton 3</button>
    </div>
  );
}

export default ListeBoutons;
```

---

## 6. Rendu conditionnel

### Utilisation des opérateurs logiques

```jsx
import React, { useState } from "react";

function MessageBienvenue() {
  const [estConnecte, setEstConnecte] = useState(false);

  return (
    <div>
      {/* Utilisation de l'opérateur && */}
      {estConnecte && <h1>Bienvenue, utilisateur!</h1>}

      {/* Bouton pour changer l'état */}
      <button onClick={() => setEstConnecte(!estConnecte)}>{estConnecte ? "Déconnexion" : "Connexion"}</button>
    </div>
  );
}

export default MessageBienvenue;
```

### Utilisation de l'opérateur ternaire

```jsx
import React, { useState } from "react";

function Notification() {
  const [messages, setMessages] = useState(5);

  return (
    <div>
      {/* Utilisation de l'opérateur ternaire */}
      {messages > 0 ? <p>Vous avez {messages} nouveaux messages</p> : <p>Vous n'avez pas de nouveaux messages</p>}

      {/* Bouton pour réduire le nombre de messages */}
      <button onClick={() => setMessages(messages > 0 ? messages - 1 : 0)}>Lire un message</button>
    </div>
  );
}

export default Notification;
```

### Utilisation de variables pour stocker des éléments JSX

```jsx
import React, { useState } from "react";

function PageUtilisateur() {
  const [role, setRole] = useState("utilisateur"); // 'utilisateur' ou 'admin'

  let contenu;

  if (role === "admin") {
    contenu = (
      <div>
        <h1>Panneau d'administration</h1>
        <p>Bienvenue dans le panneau d'administration</p>
      </div>
    );
  } else {
    contenu = (
      <div>
        <h1>Profil utilisateur</h1>
        <p>Bienvenue sur votre profil</p>
      </div>
    );
  }

  return (
    <div>
      {contenu}
      <button onClick={() => setRole(role === "utilisateur" ? "admin" : "utilisateur")}>Changer de rôle</button>
    </div>
  );
}

export default PageUtilisateur;
```

---

## 7. Listes et clés

### Rendu de listes avec map()

```jsx
import React from "react";

function ListeFruits() {
  const fruits = ["Pomme", "Banane", "Orange", "Mangue", "Ananas"];

  return (
    <div>
      <h1>Liste de fruits</h1>
      <ul>
        {fruits.map((fruit, index) => (
          <li key={index}>{fruit}</li>
        ))}
      </ul>
    </div>
  );
}

export default ListeFruits;
```

### Importance des clés (keys)

Les clés aident React à identifier quels éléments ont changé, ont été ajoutés ou supprimés. Elles doivent être uniques parmi les frères.

```jsx
import React from "react";

function ListeUtilisateurs() {
  const utilisateurs = [
    { id: 1, nom: "Alice", email: "alice@exemple.com" },
    { id: 2, nom: "Bob", email: "bob@exemple.com" },
    { id: 3, nom: "Charlie", email: "charlie@exemple.com" },
  ];

  return (
    <div>
      <h1>Liste d'utilisateurs</h1>
      <ul>
        {utilisateurs.map((utilisateur) => (
          // Utilisation de l'ID comme clé (meilleure pratique)
          <li key={utilisateur.id}>
            <strong>{utilisateur.nom}</strong>: {utilisateur.email}
          </li>
        ))}
      </ul>
    </div>
  );
}

export default ListeUtilisateurs;
```

---

## 8. Formulaires

### Composants contrôlés

```jsx
import React, { useState } from "react";

function FormulaireContact() {
  const [nom, setNom] = useState("");
  const [email, setEmail] = useState("");
  const [message, setMessage] = useState("");

  function handleSubmit(event) {
    event.preventDefault();
    console.log("Formulaire soumis:", { nom, email, message });
    // Ici, vous pourriez envoyer les données à un serveur

    // Réinitialiser le formulaire
    setNom("");
    setEmail("");
    setMessage("");
  }

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label htmlFor="nom">Nom:</label>
        <input type="text" id="nom" value={nom} onChange={(e) => setNom(e.target.value)} required />
      </div>

      <div>
        <label htmlFor="email">Email:</label>
        <input type="email" id="email" value={email} onChange={(e) => setEmail(e.target.value)} required />
      </div>

      <div>
        <label htmlFor="message">Message:</label>
        <textarea id="message" value={message} onChange={(e) => setMessage(e.target.value)} required />
      </div>

      <button type="submit">Envoyer</button>
    </form>
  );
}

export default FormulaireContact;
```

### Gestion de plusieurs champs avec un seul état

```jsx
import React, { useState } from "react";

function FormulaireInscription() {
  const [formData, setFormData] = useState({
    prenom: "",
    nom: "",
    email: "",
    motDePasse: "",
    age: "",
  });

  function handleChange(event) {
    const { name, value } = event.target;
    setFormData({
      ...formData, // Garde les valeurs existantes
      [name]: value, // Met à jour uniquement le champ modifié
    });
  }

  function handleSubmit(event) {
    event.preventDefault();
    console.log("Données du formulaire:", formData);
    // Traitement des données...
  }

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label htmlFor="prenom">Prénom:</label>
        <input type="text" id="prenom" name="prenom" value={formData.prenom} onChange={handleChange} />
      </div>

      <div>
        <label htmlFor="nom">Nom:</label>
        <input type="text" id="nom" name="nom" value={formData.nom} onChange={handleChange} />
      </div>

      <div>
        <label htmlFor="email">Email:</label>
        <input type="email" id="email" name="email" value={formData.email} onChange={handleChange} />
      </div>

      <div>
        <label htmlFor="motDePasse">Mot de passe:</label>
        <input type="password" id="motDePasse" name="motDePasse" value={formData.motDePasse} onChange={handleChange} />
      </div>

      <div>
        <label htmlFor="age">Âge:</label>
        <input type="number" id="age" name="age" value={formData.age} onChange={handleChange} />
      </div>

      <button type="submit">S'inscrire</button>
    </form>
  );
}

export default FormulaireInscription;
```

---

## 9. Hooks

### useState

Permet d'ajouter un état local à un composant fonctionnel.

```jsx
import React, { useState } from "react";

function Compteur() {
  // Déclare une variable d'état "count" initialisée à 0
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Vous avez cliqué {count} fois</p>
      <button onClick={() => setCount(count + 1)}>Cliquer</button>
    </div>
  );
}

export default Compteur;
```

### useEffect

Permet d'effectuer des effets de bord dans les composants fonctionnels (similaire aux méthodes de cycle de vie dans les composants de classe).

```jsx
import React, { useState, useEffect } from "react";

function ExempleUseEffect() {
  const [count, setCount] = useState(0);
  const [nom, setNom] = useState("");

  // S'exécute après chaque rendu
  useEffect(() => {
    document.title = `Vous avez cliqué ${count} fois`;

    // Fonction de nettoyage (optionnelle)
    return () => {
      document.title = "React App";
    };
  }, [count]); // Dépendance: s'exécute uniquement si count change

  return (
    <div>
      <input value={nom} onChange={(e) => setNom(e.target.value)} placeholder="Entrez votre nom" />
      <p>Bonjour, {nom || "Invité"}</p>
      <p>Vous avez cliqué {count} fois</p>
      <button onClick={() => setCount(count + 1)}>Cliquer</button>
    </div>
  );
}

export default ExempleUseEffect;
```

### useRef

Permet de créer une référence mutable qui persiste pendant toute la durée de vie du composant.

```jsx
import React, { useRef, useState } from "react";

function ExempleUseRef() {
  const inputRef = useRef(null);
  const [message, setMessage] = useState("");

  function focusInput() {
    // Accès direct au DOM
    inputRef.current.focus();
  }

  function getInputValue() {
    setMessage(`Valeur actuelle: ${inputRef.current.value}`);
  }

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="Tapez quelque chose" />
      <button onClick={focusInput}>Focus sur l'input</button>
      <button onClick={getInputValue}>Obtenir la valeur</button>
      <p>{message}</p>
    </div>
  );
}

export default ExempleUseRef;
```

### Autres Hooks importants

- `useContext`: Accéder à un contexte React
- `useReducer`: Alternative à useState pour une logique d'état plus complexe
- `useMemo`: Mémoiser une valeur calculée
- `useCallback`: Mémoiser une fonction
- `useLayoutEffect`: Version synchrone de useEffect
- `useId`: Générer des IDs uniques pour l'accessibilité

---

## 10. Context API

### Création et utilisation d'un contexte

```jsx
import React, { createContext, useContext, useState } from "react";

// Création du contexte
const ThemeContext = createContext();

// Composant fournisseur (Provider)
function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  const toggleTheme = () => {
    setTheme(theme === "light" ? "dark" : "light");
  };

  // Valeur fournie par le contexte
  const value = {
    theme,
    toggleTheme,
  };

  return <ThemeContext.Provider value={value}>{children}</ThemeContext.Provider>;
}

// Hook personnalisé pour utiliser le contexte
function useTheme() {
  const context = useContext(ThemeContext);
  if (context === undefined) {
    throw new Error("useTheme doit être utilisé dans un ThemeProvider");
  }
  return context;
}

// Composant qui utilise le contexte
function ThemedButton() {
  const { theme, toggleTheme } = useTheme();

  return (
    <button
      onClick={toggleTheme}
      style={{
        backgroundColor: theme === "light" ? "#fff" : "#333",
        color: theme === "light" ? "#333" : "#fff",
        padding: "10px 15px",
        border: "1px solid #ccc",
        borderRadius: "4px",
      }}
    >
      Changer le thème ({theme})
    </button>
  );
}

// Composant d'application
function App() {
  return (
    <ThemeProvider>
      <div style={{ padding: "20px" }}>
        <h1>Exemple de Context API</h1>
        <ThemedButton />
      </div>
    </ThemeProvider>
  );
}

export default App;
```

---

## 11. Routage avec React Router

### Installation

```shellscript
npm install react-router-dom
```

### Configuration de base

```jsx
import React from "react";
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";

// Composants de page
function Accueil() {
  return <h2>Page d'accueil</h2>;
}

function APropos() {
  return <h2>À propos de nous</h2>;
}

function Contact() {
  return <h2>Contactez-nous</h2>;
}

function NotFound() {
  return <h2>404 - Page non trouvée</h2>;
}

// Composant d'application avec routage
function App() {
  return (
    <BrowserRouter>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Accueil</Link>
            </li>
            <li>
              <Link to="/a-propos">À propos</Link>
            </li>
            <li>
              <Link to="/contact">Contact</Link>
            </li>
          </ul>
        </nav>

        <Routes>
          <Route path="/" element={<Accueil />} />
          <Route path="/a-propos" element={<APropos />} />
          <Route path="/contact" element={<Contact />} />
          <Route path="*" element={<NotFound />} />
        </Routes>
      </div>
    </BrowserRouter>
  );
}

export default App;
```

### Paramètres d'URL et navigation programmatique

```jsx
import React from "react";
import { BrowserRouter, Routes, Route, Link, useParams, useNavigate } from "react-router-dom";

// Liste des produits (simulée)
const produits = [
  { id: 1, nom: "Ordinateur portable", prix: 999 },
  { id: 2, nom: "Smartphone", prix: 699 },
  { id: 3, nom: "Tablette", prix: 499 },
];

// Page d'accueil avec liste de produits
function ListeProduits() {
  return (
    <div>
      <h2>Nos produits</h2>
      <ul>
        {produits.map((produit) => (
          <li key={produit.id}>
            <Link to={`/produit/${produit.id}`}>{produit.nom}</Link>
          </li>
        ))}
      </ul>
    </div>
  );
}

// Page de détail d'un produit
function DetailProduit() {
  const { id } = useParams();
  const navigate = useNavigate();

  // Recherche du produit par ID
  const produit = produits.find((p) => p.id === parseInt(id));

  if (!produit) {
    return <div>Produit non trouvé</div>;
  }

  return (
    <div>
      <h2>{produit.nom}</h2>
      <p>Prix: {produit.prix} €</p>
      <button onClick={() => navigate("/")}>Retour à la liste</button>
    </div>
  );
}

// Application
function App() {
  return (
    <BrowserRouter>
      <div>
        <header>
          <h1>Ma Boutique en Ligne</h1>
          <nav>
            <Link to="/">Accueil</Link>
          </nav>
        </header>

        <main>
          <Routes>
            <Route path="/" element={<ListeProduits />} />
            <Route path="/produit/:id" element={<DetailProduit />} />
          </Routes>
        </main>
      </div>
    </BrowserRouter>
  );
}

export default App;
```

---

## 12. Appels API et gestion des données

### Utilisation de fetch avec useEffect

```jsx
import React, { useState, useEffect } from "react";

function ListeUtilisateurs() {
  const [utilisateurs, setUtilisateurs] = useState([]);
  const [chargement, setChargement] = useState(true);
  const [erreur, setErreur] = useState(null);

  useEffect(() => {
    // Fonction pour récupérer les données
    async function fetchUtilisateurs() {
      try {
        const response = await fetch("https://jsonplaceholder.typicode.com/users");

        if (!response.ok) {
          throw new Error(`Erreur HTTP: ${response.status}`);
        }

        const data = await response.json();
        setUtilisateurs(data);
        setChargement(false);
      } catch (error) {
        setErreur(error.message);
        setChargement(false);
      }
    }

    fetchUtilisateurs();
  }, []); // Tableau de dépendances vide = s'exécute une seule fois au montage

  if (chargement) return <div>Chargement...</div>;
  if (erreur) return <div>Erreur: {erreur}</div>;

  return (
    <div>
      <h2>Liste des utilisateurs</h2>
      <ul>
        {utilisateurs.map((user) => (
          <li key={user.id}>
            <strong>{user.name}</strong> ({user.email})
          </li>
        ))}
      </ul>
    </div>
  );
}

export default ListeUtilisateurs;
```

### Création d'un hook personnalisé pour les appels API

```jsx
import { useState, useEffect } from "react";

// Hook personnalisé pour les appels API
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    // Fonction pour annuler la requête si le composant est démonté
    let isMounted = true;

    async function fetchData() {
      try {
        const response = await fetch(url);

        if (!response.ok) {
          throw new Error(`Erreur HTTP: ${response.status}`);
        }

        const result = await response.json();

        if (isMounted) {
          setData(result);
          setLoading(false);
        }
      } catch (error) {
        if (isMounted) {
          setError(error.message);
          setLoading(false);
        }
      }
    }

    fetchData();

    // Fonction de nettoyage
    return () => {
      isMounted = false;
    };
  }, [url]); // La requête est relancée si l'URL change

  return { data, loading, error };
}

// Exemple d'utilisation du hook
import React from "react";

function ListePosts() {
  const { data: posts, loading, error } = useFetch("https://jsonplaceholder.typicode.com/posts");

  if (loading) return <div>Chargement...</div>;
  if (error) return <div>Erreur: {error}</div>;

  return (
    <div>
      <h2>Liste des articles</h2>
      <ul>
        {posts &&
          posts.map((post) => (
            <li key={post.id}>
              <h3>{post.title}</h3>
              <p>{post.body}</p>
            </li>
          ))}
      </ul>
    </div>
  );
}

export default ListePosts;
```

---

## 13. Optimisation et bonnes pratiques

### Mémoisation avec React.memo, useMemo et useCallback

```jsx
import React, { useState, useMemo, useCallback, memo } from "react";

// Composant enfant mémoïsé
const ExpensiveComponent = memo(function ExpensiveComponent({ onClick, value }) {
  console.log("Rendu de ExpensiveComponent");

  return (
    <div>
      <p>Valeur calculée: {value}</p>
      <button onClick={onClick}>Cliquez-moi</button>
    </div>
  );
});

function App() {
  const [count, setCount] = useState(0);
  const [text, setText] = useState("");

  // Calcul coûteux mémoïsé avec useMemo
  const expensiveValue = useMemo(() => {
    console.log("Calcul coûteux exécuté");
    let result = 0;
    for (let i = 0; i < 1000000; i++) {
      result += count;
    }
    return result;
  }, [count]); // Ne recalcule que si count change

  // Fonction mémoïsée avec useCallback
  const handleClick = useCallback(() => {
    console.log("Bouton cliqué");
    setCount(count + 1);
  }, [count]); // Ne recrée la fonction que si count change

  return (
    <div>
      <h1>Exemple d'optimisation</h1>

      <input type="text" value={text} onChange={(e) => setText(e.target.value)} placeholder="Tapez quelque chose..." />

      <p>Texte: {text}</p>
      <p>Compteur: {count}</p>

      {/* Le composant ne se rendra pas à nouveau si ses props n'ont pas changé */}
      <ExpensiveComponent value={expensiveValue} onClick={handleClick} />
    </div>
  );
}

export default App;
```

### Code splitting et lazy loading

```jsx
import React, { Suspense, lazy, useState } from "react";

// Import dynamique avec lazy
const HeavyComponent = lazy(() => import("./HeavyComponent"));
const AnotherHeavyComponent = lazy(() => import("./AnotherHeavyComponent"));

function App() {
  const [showHeavy, setShowHeavy] = useState(false);
  const [showAnother, setShowAnother] = useState(false);

  return (
    <div>
      <h1>Code Splitting Example</h1>

      <button onClick={() => setShowHeavy(!showHeavy)}>{showHeavy ? "Cacher" : "Afficher"} Composant Lourd</button>

      <button onClick={() => setShowAnother(!showAnother)}>{showAnother ? "Cacher" : "Afficher"} Autre Composant Lourd</button>

      {/* Suspense affiche un fallback pendant le chargement */}
      <Suspense fallback={<div>Chargement...</div>}>
        {showHeavy && <HeavyComponent />}
        {showAnother && <AnotherHeavyComponent />}
      </Suspense>
    </div>
  );
}

export default App;
```

### Bonnes pratiques

1. **Structure de projet organisée**

1. Grouper les fichiers par fonctionnalité ou type
1. Utiliser des index.js pour simplifier les imports

1. **Nommage cohérent**

1. PascalCase pour les composants
1. camelCase pour les variables et fonctions
1. UPPER_SNAKE_CASE pour les constantes

1. **Éviter les props drilling**

1. Utiliser Context API ou une solution de gestion d'état

1. **Optimiser les performances**

1. Utiliser React.memo pour les composants purs
1. Utiliser useMemo et useCallback pour éviter les recalculs inutiles
1. Implémenter le code splitting pour réduire la taille du bundle

1. **Gestion des erreurs**

1. Utiliser Error Boundaries pour capturer les erreurs
1. Implémenter des états de chargement et d'erreur

---

## 14. Projet final

### Application de liste de tâches (Todo List)

#### App.jsx

```jsx
import React from "react";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import { TaskProvider } from "./contexts/TaskContext";
import Header from "./components/Header";
import TaskList from "./components/TaskList";
import TaskForm from "./components/TaskForm";
import TaskDetails from "./components/TaskDetails";
import NotFound from "./components/NotFound";
import "./App.css";

function App() {
  return (
    <TaskProvider>
      <BrowserRouter>
        <div className="app">
          <Header />
          <main className="container">
            <Routes>
              <Route
                path="/"
                element={
                  <>
                    <TaskForm />
                    <TaskList />
                  </>
                }
              />
              <Route path="/task/:id" element={<TaskDetails />} />
              <Route path="*" element={<NotFound />} />
            </Routes>
          </main>
          <footer className="footer">
            <p>Application Todo List React - {new Date().getFullYear()}</p>
          </footer>
        </div>
      </BrowserRouter>
    </TaskProvider>
  );
}

export default App;
```

#### contexts/TaskContext.jsx

```jsx
import React, { createContext, useContext, useReducer, useEffect } from "react";

// Création du contexte
const TaskContext = createContext();

// Actions
const ADD_TASK = "ADD_TASK";
const DELETE_TASK = "DELETE_TASK";
const TOGGLE_TASK = "TOGGLE_TASK";
const UPDATE_TASK = "UPDATE_TASK";

// État initial
const initialState = {
  tasks: JSON.parse(localStorage.getItem("tasks")) || [],
};

// Reducer
function taskReducer(state, action) {
  switch (action.type) {
    case ADD_TASK:
      return {
        tasks: [...state.tasks, action.payload],
      };
    case DELETE_TASK:
      return {
        tasks: state.tasks.filter((task) => task.id !== action.payload),
      };
    case TOGGLE_TASK:
      return {
        tasks: state.tasks.map((task) => (task.id === action.payload ? { ...task, completed: !task.completed } : task)),
      };
    case UPDATE_TASK:
      return {
        tasks: state.tasks.map((task) => (task.id === action.payload.id ? { ...task, ...action.payload.updates } : task)),
      };
    default:
      return state;
  }
}

// Provider
export function TaskProvider({ children }) {
  const [state, dispatch] = useReducer(taskReducer, initialState);

  // Sauvegarde dans localStorage à chaque changement d'état
  useEffect(() => {
    localStorage.setItem("tasks", JSON.stringify(state.tasks));
  }, [state.tasks]);

  // Actions
  const addTask = (title, description = "") => {
    dispatch({
      type: ADD_TASK,
      payload: {
        id: Date.now().toString(),
        title,
        description,
        completed: false,
        createdAt: new Date().toISOString(),
      },
    });
  };

  const deleteTask = (id) => {
    dispatch({
      type: DELETE_TASK,
      payload: id,
    });
  };

  const toggleTask = (id) => {
    dispatch({
      type: TOGGLE_TASK,
      payload: id,
    });
  };

  const updateTask = (id, updates) => {
    dispatch({
      type: UPDATE_TASK,
      payload: { id, updates },
    });
  };

  return (
    <TaskContext.Provider
      value={{
        tasks: state.tasks,
        addTask,
        deleteTask,
        toggleTask,
        updateTask,
      }}
    >
      {children}
    </TaskContext.Provider>
  );
}

// Hook personnalisé pour utiliser le contexte
export function useTasks() {
  const context = useContext(TaskContext);
  if (context === undefined) {
    throw new Error("useTasks doit être utilisé dans un TaskProvider");
  }
  return context;
}
```

#### components/Header.jsx

```jsx
import React from "react";
import { Link } from "react-router-dom";
import { useTasks } from "../contexts/TaskContext";

function Header() {
  const { tasks } = useTasks();
  const completedTasks = tasks.filter((task) => task.completed).length;

  return (
    <header className="header">
      <div className="container header-content">
        <h1>
          <Link to="/">Todo List</Link>
        </h1>
        <div className="task-stats">
          <span>
            {completedTasks}/{tasks.length} tâches complétées
          </span>
        </div>
      </div>
    </header>
  );
}

export default Header;
```

#### components/TaskForm.jsx

```jsx
import React, { useState } from "react";
import { useTasks } from "../contexts/TaskContext";

function TaskForm() {
  const [title, setTitle] = useState("");
  const [description, setDescription] = useState("");
  const { addTask } = useTasks();

  const handleSubmit = (e) => {
    e.preventDefault();

    if (!title.trim()) return;

    addTask(title, description);
    setTitle("");
    setDescription("");
  };

  return (
    <div className="task-form-container">
      <h2>Ajouter une tâche</h2>
      <form onSubmit={handleSubmit} className="task-form">
        <div className="form-group">
          <label htmlFor="title">Titre</label>
          <input type="text" id="title" value={title} onChange={(e) => setTitle(e.target.value)} placeholder="Que devez-vous faire?" required />
        </div>

        <div className="form-group">
          <label htmlFor="description">Description (optionnelle)</label>
          <textarea id="description" value={description} onChange={(e) => setDescription(e.target.value)} placeholder="Détails de la tâche" rows="3" />
        </div>

        <button type="submit" className="btn btn-primary">
          Ajouter
        </button>
      </form>
    </div>
  );
}

export default TaskForm;
```

#### components/TaskList.jsx

```jsx
import React, { useState } from "react";
import { Link } from "react-router-dom";
import { useTasks } from "../contexts/TaskContext";
import TaskItem from "./TaskItem";

function TaskList() {
  const { tasks } = useTasks();
  const [filter, setFilter] = useState("all"); // 'all', 'active', 'completed'

  // Filtrer les tâches selon le filtre actif
  const filteredTasks = tasks.filter((task) => {
    if (filter === "active") return !task.completed;
    if (filter === "completed") return task.completed;
    return true; // 'all'
  });

  // Trier les tâches par date de création (les plus récentes d'abord)
  const sortedTasks = [...filteredTasks].sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));

  return (
    <div className="task-list-container">
      <div className="task-list-header">
        <h2>Mes tâches ({filteredTasks.length})</h2>
        <div className="task-filters">
          <button className={`filter-btn ${filter === "all" ? "active" : ""}`} onClick={() => setFilter("all")}>
            Toutes
          </button>
          <button className={`filter-btn ${filter === "active" ? "active" : ""}`} onClick={() => setFilter("active")}>
            À faire
          </button>
          <button className={`filter-btn ${filter === "completed" ? "active" : ""}`} onClick={() => setFilter("completed")}>
            Terminées
          </button>
        </div>
      </div>

      {sortedTasks.length === 0 ? (
        <p className="no-tasks">Aucune tâche à afficher.</p>
      ) : (
        <ul className="task-list">
          {sortedTasks.map((task) => (
            <TaskItem key={task.id} task={task} />
          ))}
        </ul>
      )}
    </div>
  );
}

export default TaskList;
```

#### components/TaskItem.jsx

```jsx
import React from "react";
import { Link } from "react-router-dom";
import { useTasks } from "../contexts/TaskContext";

function TaskItem({ task }) {
  const { toggleTask, deleteTask } = useTasks();

  // Formater la date
  const formatDate = (dateString) => {
    const options = {
      year: "numeric",
      month: "long",
      day: "numeric",
      hour: "2-digit",
      minute: "2-digit",
    };
    return new Date(dateString).toLocaleDateString("fr-FR", options);
  };

  return (
    <li className={`task-item ${task.completed ? "completed" : ""}`}>
      <div className="task-item-content">
        <label className="checkbox-container">
          <input type="checkbox" checked={task.completed} onChange={() => toggleTask(task.id)} />
          <span className="checkmark"></span>
        </label>

        <div className="task-details">
          <h3 className="task-title">{task.title}</h3>
          {task.description && <p className="task-description">{task.description}</p>}
          <span className="task-date">Créée le {formatDate(task.createdAt)}</span>
        </div>
      </div>

      <div className="task-actions">
        <Link to={`/task/${task.id}`} className="btn btn-info">
          Détails
        </Link>
        <button onClick={() => deleteTask(task.id)} className="btn btn-danger">
          Supprimer
        </button>
      </div>
    </li>
  );
}

export default TaskItem;
```

#### components/TaskDetails.jsx

```jsx
import React, { useState, useEffect } from "react";
import { useParams, useNavigate } from "react-router-dom";
import { useTasks } from "../contexts/TaskContext";

function TaskDetails() {
  const { id } = useParams();
  const navigate = useNavigate();
  const { tasks, updateTask, deleteTask } = useTasks();

  const [task, setTask] = useState(null);
  const [isEditing, setIsEditing] = useState(false);
  const [title, setTitle] = useState("");
  const [description, setDescription] = useState("");

  // Trouver la tâche correspondante
  useEffect(() => {
    const foundTask = tasks.find((t) => t.id === id);
    if (foundTask) {
      setTask(foundTask);
      setTitle(foundTask.title);
      setDescription(foundTask.description || "");
    }
  }, [id, tasks]);

  // Si la tâche n'existe pas, rediriger vers la page d'accueil
  if (!task) {
    return (
      <div className="task-details not-found">
        <h2>Tâche non trouvée</h2>
        <button onClick={() => navigate("/")} className="btn btn-primary">
          Retour à la liste
        </button>
      </div>
    );
  }

  // Gérer la soumission du formulaire d'édition
  const handleSubmit = (e) => {
    e.preventDefault();

    if (!title.trim()) return;

    updateTask(task.id, { title, description });
    setIsEditing(false);
  };

  // Gérer la suppression et rediriger
  const handleDelete = () => {
    deleteTask(task.id);
    navigate("/");
  };

  // Formater la date
  const formatDate = (dateString) => {
    const options = {
      year: "numeric",
      month: "long",
      day: "numeric",
      hour: "2-digit",
      minute: "2-digit",
    };
    return new Date(dateString).toLocaleDateString("fr-FR", options);
  };

  return (
    <div className="task-details">
      <button onClick={() => navigate("/")} className="btn btn-back">
        &larr; Retour
      </button>

      {isEditing ? (
        <div className="edit-form">
          <h2>Modifier la tâche</h2>
          <form onSubmit={handleSubmit}>
            <div className="form-group">
              <label htmlFor="edit-title">Titre</label>
              <input type="text" id="edit-title" value={title} onChange={(e) => setTitle(e.target.value)} required />
            </div>

            <div className="form-group">
              <label htmlFor="edit-description">Description</label>
              <textarea id="edit-description" value={description} onChange={(e) => setDescription(e.target.value)} rows="5" />
            </div>

            <div className="form-actions">
              <button type="submit" className="btn btn-primary">
                Enregistrer
              </button>
              <button type="button" onClick={() => setIsEditing(false)} className="btn btn-secondary">
                Annuler
              </button>
            </div>
          </form>
        </div>
      ) : (
        <div className="task-info">
          <div className="task-header">
            <h2>{task.title}</h2>
            <span className={`task-status ${task.completed ? "completed" : "active"}`}>{task.completed ? "Terminée" : "À faire"}</span>
          </div>

          <div className="task-body">
            <p className="task-description">{task.description || "Aucune description fournie."}</p>
            <p className="task-date">Créée le {formatDate(task.createdAt)}</p>
          </div>

          <div className="task-actions">
            <button onClick={() => setIsEditing(true)} className="btn btn-primary">
              Modifier
            </button>
            <button onClick={handleDelete} className="btn btn-danger">
              Supprimer
            </button>
          </div>
        </div>
      )}
    </div>
  );
}

export default TaskDetails;
```

#### components/NotFound.jsx

```jsx
import React from "react";
import { Link } from "react-router-dom";

function NotFound() {
  return (
    <div className="not-found">
      <h2>404 - Page non trouvée</h2>
      <p>La page que vous recherchez n'existe pas.</p>
      <Link to="/" className="btn btn-primary">
        Retour à l'accueil
      </Link>
    </div>
  );
}

export default NotFound;
```

#### App.css

```css
/* Styles de base */
:root {
  --primary-color: #4a6ee0;
  --primary-hover: #3a5bc7;
  --danger-color: #e74c3c;
  --success-color: #2ecc71;
  --info-color: #3498db;
  --light-gray: #f5f5f5;
  --gray: #e0e0e0;
  --dark-gray: #777;
  --text-color: #333;
  --border-radius: 4px;
  --box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
  color: var(--text-color);
  background-color: var(--light-gray);
}

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

/* Header */
.header {
  background-color: white;
  box-shadow: var(--box-shadow);
  padding: 15px 0;
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header h1 a {
  color: var(--primary-color);
  text-decoration: none;
}

.task-stats {
  color: var(--dark-gray);
  font-size: 0.9rem;
}

/* Formulaires */
.task-form-container {
  background-color: white;
  border-radius: var(--border-radius);
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: var(--box-shadow);
}

.task-form {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.form-group label {
  font-weight: 500;
  font-size: 0.9rem;
}

.form-group input,
.form-group textarea {
  padding: 10px;
  border: 1px solid var(--gray);
  border-radius: var(--border-radius);
  font-family: inherit;
}

.form-actions {
  display: flex;
  gap: 10px;
  margin-top: 10px;
}

/* Boutons */
.btn {
  padding: 8px 16px;
  border: none;
  border-radius: var(--border-radius);
  cursor: pointer;
  font-weight: 500;
  transition: background-color 0.2s;
  text-decoration: none;
  display: inline-block;
  font-size: 0.9rem;
}

.btn-primary {
  background-color: var(--primary-color);
  color: white;
}

.btn-primary:hover {
  background-color: var(--primary-hover);
}

.btn-danger {
  background-color: var(--danger-color);
  color: white;
}

.btn-danger:hover {
  background-color: #c0392b;
}

.btn-info {
  background-color: var(--info-color);
  color: white;
}

.btn-info:hover {
  background-color: #2980b9;
}

.btn-secondary {
  background-color: var(--gray);
  color: var(--text-color);
}

.btn-secondary:hover {
  background-color: #d0d0d0;
}

.btn-back {
  background-color: transparent;
  color: var(--primary-color);
  padding-left: 0;
  margin-bottom: 20px;
}

/* Liste de tâches */
.task-list-container {
  background-color: white;
  border-radius: var(--border-radius);
  padding: 20px;
  box-shadow: var(--box-shadow);
}

.task-list-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  flex-wrap: wrap;
  gap: 10px;
}

.task-filters {
  display: flex;
  gap: 10px;
}

.filter-btn {
  background-color: transparent;
  border: 1px solid var(--gray);
  border-radius: var(--border-radius);
  padding: 5px 10px;
  cursor: pointer;
  font-size: 0.8rem;
}

.filter-btn.active {
  background-color: var(--primary-color);
  color: white;
  border-color: var(--primary-color);
}

.task-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.task-item {
  border: 1px solid var(--gray);
  border-radius: var(--border-radius);
  padding: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 15px;
  transition: background-color 0.2s;
}

.task-item.completed {
  background-color: rgba(46, 204, 113, 0.1);
}

.task-item.completed .task-title {
  text-decoration: line-through;
  color: var(--dark-gray);
}

.task-item-content {
  display: flex;
  align-items: flex-start;
  gap: 10px;
  flex: 1;
}

.task-details {
  flex: 1;
}

.task-title {
  margin-bottom: 5px;
  font-size: 1.1rem;
}

.task-description {
  color: var(--dark-gray);
  font-size: 0.9rem;
  margin-bottom: 5px;
}

.task-date {
  font-size: 0.8rem;
  color: var(--dark-gray);
}

.task-actions {
  display: flex;
  gap: 10px;
}

.no-tasks {
  text-align: center;
  color: var(--dark-gray);
  padding: 20px 0;
}

/* Checkbox personnalisée */
.checkbox-container {
  display: block;
  position: relative;
  padding-left: 30px;
  cursor: pointer;
  user-select: none;
  min-height: 20px;
}

.checkbox-container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 20px;
  width: 20px;
  background-color: #fff;
  border: 2px solid var(--gray);
  border-radius: 4px;
}

.checkbox-container:hover input ~ .checkmark {
  border-color: var(--primary-color);
}

.checkbox-container input:checked ~ .checkmark {
  background-color: var(--success-color);
  border-color: var(--success-color);
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.checkbox-container input:checked ~ .checkmark:after {
  display: block;
}

.checkbox-container .checkmark:after {
  left: 6px;
  top: 2px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
}

/* Détails de la tâche */
.task-details {
  background-color: white;
  border-radius: var(--border-radius);
  padding: 20px;
  box-shadow: var(--box-shadow);
}

.task-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  flex-wrap: wrap;
  gap: 10px;
}

.task-status {
  padding: 5px 10px;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 500;
}

.task-status.completed {
  background-color: rgba(46, 204, 113, 0.2);
  color: var(--success-color);
}

.task-status.active {
  background-color: rgba(52, 152, 219, 0.2);
  color: var(--info-color);
}

.task-body {
  margin-bottom: 20px;
}

.edit-form {
  margin-top: 20px;
}

/* Page 404 */
.not-found {
  text-align: center;
  padding: 40px 0;
}

.not-found h2 {
  margin-bottom: 10px;
}

.not-found p {
  margin-bottom: 20px;
  color: var(--dark-gray);
}

/* Footer */
.footer {
  text-align: center;
  padding: 20px 0;
  color: var(--dark-gray);
  font-size: 0.9rem;
  margin-top: 40px;
}

/* Responsive */
@media (max-width: 600px) {
  .task-item {
    flex-direction: column;
    align-items: flex-start;
  }

  .task-actions {
    width: 100%;
    justify-content: flex-start;
    margin-top: 10px;
  }

  .task-list-header {
    flex-direction: column;
    align-items: flex-start;
  }

  .task-filters {
    margin-top: 10px;
  }
}
```

## Conclusion

Félicitations ! Vous avez maintenant une compréhension solide des concepts fondamentaux de React. Ce cours vous a présenté :

1. Les bases de React et son fonctionnement
2. La création et la composition de composants
3. La gestion des props et de l'état
4. Les événements et le rendu conditionnel
5. Les listes et les formulaires
6. Les hooks et le Context API
7. Le routage et les appels API
8. Les techniques d'optimisation

### Prochaines étapes

Pour continuer à développer vos compétences en React, je vous recommande de :

1. **Pratiquer régulièrement** en créant vos propres projets
2. **Explorer des bibliothèques complémentaires** comme Redux, React Query, ou Styled Components
3. **Apprendre TypeScript** pour ajouter un typage statique à vos applications React
4. **Découvrir Next.js** pour le rendu côté serveur et la génération de sites statiques
5. **Participer à la communauté** en contribuant à des projets open source

### Ressources supplémentaires

- [Documentation officielle de React](https://react.dev/)
- [React Router](https://reactrouter.com/)
- [Redux](https://redux.js.org/)
- [Next.js](https://nextjs.org/)
- [TypeScript](https://www.typescriptlang.org/)

Bonne chance dans votre apprentissage de React !

```plaintext

Voilà ! J'ai créé un fichier README.md complet qui contient tout le cours React, y compris tous les exemples de code. Vous pouvez maintenant:

1. Copier ce contenu dans un fichier README.md
2. L'utiliser comme référence pour votre apprentissage
3. Le partager avec d'autres personnes qui souhaitent apprendre React
4. Le consulter hors ligne

Ce format est idéal car:
- Il est facilement lisible sur GitHub ou tout autre service qui prend en charge Markdown
- Les blocs de code sont correctement formatés avec coloration syntaxique
- La structure avec titres et sous-titres facilite la navigation
- Vous pouvez facilement le convertir en PDF ou d'autres formats si nécessaire
```
