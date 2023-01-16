# Projet Final

Pour ce devoir, vous devrez soumettre le lien du dépôt GitHub pour votre projet final. Lorsque vous serez prêt, veuillez télécharger le modèle situé en dessous de cette fenêtre, remplissez-le et soumettez-le en tant que votre devoir.

## Pour obtenir une certification de développeur pour ce cours, votre projet doit :

1. Suivre cette forme de nomination :
[**https://github.com/VOTRE_IDENTIFIANT_GITHUB_ICI/blockchain-developer-bootcamp-final-project**](https://github.com/VOTRE_IDENTIFIANT_GITHUB_ICI/blockchain-developer-bootcamp-final-project)

2. Contenir un fichier README.md qui décrit le projet, décrit la structure du répertoire, et comment accéder à la partie frontend du projet (voir #8). S’il vous plait veuillez aussi inclure votre compte public d’ETHEREUM si vous vous voulez recevoir votre certificat sous format NFT (Optionnel).
3. Contenir un ou des contrats intelligents (Smart Contract(s)) qui:
 - **Sont commentés** suivant la [description décrite ici](https://docs.soliditylang.org/en/latest/natspec-format.html)
 - Utilisent au moins deux model de conception (Design Pattern) depuis la section des contrats intelligents [(VOIR LA LISTE DES MODEL DE CONCEPTION ICI)](https://docs.google.com/document/d/1tthsXLlv5BDXEGUfoP6_MAsL_8_T0sRBNQs_1OnPxak/edit)
 - **Se protégent contre deux vecteurs d’attaque** depuis la section des contrats intelligents avec leurs [numéro SWC](https://swcregistry.io/) [(VOIR LA LISTE DES VECTEURS D’ATTAQUE ICI](https://docs.google.com/document/d/1tthsXLlv5BDXEGUfoP6_MAsL_8_T0sRBNQs_1OnPxak/edit))
- héritent d'au moins **une bibliothèque(library) ou interface**
- Peuvent être facilement compilé, migré et testé (voir #5) (nous devons juste le compiler et le tester localement).
4. **Contenir un fichier Markdown nommé** **design\_pattern\_decisions.md** **et** **avoiding\_common\_attacks.md** qui décrit votre model de conception et les mesures de sécurité. [Vous pouvez voir une liste de modèles de conception et des problèmes de sécurité traité dans ce cours ici](https://docs.google.com/document/d/1tthsXLlv5BDXEGUfoP6_MAsL_8_T0sRBNQs_1OnPxak/edit).
5. **Ayez au moins cinq tests unitaires pour votre (vos) contrat(s) intelligent(s)** qui passent. Dans le code, incluez une phrase ou deux expliquant ce que sont les tests couvrant leur comportement attendu. Vous n'êtes pas obligé de construire des tests unitaires pour votre frontend, seulement pour vos contrats intelligents
6. **Contenir un fichier** deployed\_address.txt qui contient l'adresse testnet et le réseau où votre ou vos contrats ont été déployés.
7. **Avoir une interface frontend** construite avec un framework comme React ou du simple HTML/CSS/JS qui :
- **Détecte l**a présence de MetaMask.
- **Se connecte** au compte courant.
- **Affiche les informations** de votre contrat intelligent
- Permet à un utilisateur de **soumettre une transaction** pour mettre à jour l'état du contrat intelligent
- **Met à jour le frontend** si la transaction est réussie ou non
8. **Être héberger** sur **GitHub Pages, Netlify, Fleek, Surge, Heroku** ou tout autre service frontal gratuit qui offre aux utilisateurs une interface publique à votre application décentralisée. Cette adresse doit figurer dans votre document README.md.
9. Dans votre fichier README.md, assurez-vous d'avoir des instructions claires sur :
- **L'installation des dépendances** pour votre projet.
- **L'accès ou** - si votre projet nécessite un serveur (non requis) - **l'exécution de votre projet**.
- **L’exécution des tests unitaires de votre contrat intelligent** et savoir sur quel port un testnet local doit être exécuté.
- Note : Cette section nécessitait auparavant trois scripts bash mais a été révisée.
10. **Un enregistrement de votre parcours dans votre projet,** y compris la soumission des transactions et la visualisation de l'état mis à jour. Vous pouvez utiliser un enregistreur d'écran de votre choix ou un logiciel comme Loom, et vous pouvez partager le lien vers l'enregistrement dans votre README.md.

## Rappelez-vous :
**NE TÉLÉCHARGEZ PAS D'INFORMATIONS SENSIBLES SUR GITHUB OU UN SITE PUBLIC !** Les détails de votre compte Infura, les mnémoniques MetaMask, les clés privées, etc., doivent tous être dans un fichier .env que vous ajoutez à votre .gitignore dans votre projet local. Dans votre README.md, vous devez indiquer à l'utilisateur comment remplir le fichier .env localement avec ses propres informations. [Lisez plus à ce sujet ici](https://blog.infura.io/how-to-use-dotenv-to-enhance-basic-security-within-your-dapp/)

 ## **Une note sur le style :** 
 Dans ce cours, nous mettons l'accent sur **la fonctionnalité** et **la sécurité** plutôt que sur le style. Il ne s'agit pas d'un cours de conception d'interface, mais d'un cours sur Ethereum et le développement d'applications décentralisées. Nous voulons simplement que vous démontriez ce que vous avez appris tout au long du cours, même si c'est très simple.

### **Vous pourrez livrer des mises à jour à votre dépôt jusqu'à 23h59, [heure de l'AoE](https://www.timeanddate.com/time/zones/aoe) , le 30 novembre.**
