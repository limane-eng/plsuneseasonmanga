<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pétition Brawl Stars - Saison Manga</title>
    <link rel="stylesheet" href="styles.css"> <!-- Lien vers le fichier CSS -->
</head>
<body>
    <!-- Formulaire d'email -->
    <div class="container" id="email-container">
        <h1>Avant de signer la pétition</h1>
        <p>Veuillez entrer votre adresse email pour confirmer votre signature.</p>
        <input type="email" id="email-input" class="email-input" placeholder="Entrez votre adresse email" required />
        <button class="btn-sign" onclick="verifyEmail()">Vérifier l'email et signer</button>
    </div>

    <!-- Pétition Container -->
    <div class="container hidden" id="petition-container">
        <h1>Pétition pour ajouter une Saison Manga dans Brawl Stars !</h1>
        <p>Signez cette pétition pour que Brawl Stars rajoute une saison inspirée par l'univers manga !</p>

        <div class="progress-container">
            <div class="progress-bar" id="progress-bar"></div>
        </div>

        <p id="progress-text">0 sur 3 millions ont signé</p>

        <button class="btn-sign" onclick="signPetition()">Signer la pétition</button>
    </div>

    <!-- Félicitations Container -->
    <div class="container hidden" id="thank-you-container">
        <h1>Merci pour votre signature !</h1>
        <p>Votre soutien compte ! Nous avons besoin de 3 millions de signatures pour que cette saison Manga devienne réalité !</p>

        <div class="progress-container">
            <div class="progress-bar" id="thank-you-progress-bar"></div>
        </div>

        <p id="thank-you-progress-text">1 sur 3 millions ont signé</p>

        <button class="btn-home" onclick="goHome()">Retour à la pétition</button>
    </div>

    <script>
        // Variables de suivi de la pétition
        const maxSignatures = 3000000;
        let signedCount = localStorage.getItem('signedCount') ? parseInt(localStorage.getItem('signedCount')) : 0;
        let progressBar = document.getElementById('progress-bar');
        let progressText = document.getElementById('progress-text');
        let thankYouProgressBar = document.getElementById('thank-you-progress-bar');
        let thankYouProgressText = document.getElementById('thank-you-progress-text');

        // Fonction pour vérifier l'email et envoyer un mail de confirmation
        function verifyEmail() {
            let email = document.getElementById('email-input').value;
            if (email && validateEmail(email)) {
                // Simuler l'envoi d'un email
                alert("Un email de vérification a été envoyé à " + email);

                // Envoi réel de l'email de vérification
                // Vous devez utiliser un serveur pour envoyer l'email ici

                // Une fois l'email vérifié, permettre à l'utilisateur de signer
                document.getElementById('email-container').classList.add('hidden');
                document.getElementById('petition-container').classList.remove('hidden');
                updateProgressBar();
            } else {
                alert("Veuillez entrer une adresse email valide.");
            }
        }

        // Fonction de validation d'email
        function validateEmail(email) {
            const re = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$/;
            return re.test(email);
        }

        // Initialisation de la barre de progression
        function updateProgressBar() {
            const progress = (signedCount / maxSignatures) * 100;
            progressBar.style.width = progress + '%';
            progressText.innerText = `${signedCount} sur 3 millions ont signé`;
            
            // Mise à jour sur la page de félicitations
            thankYouProgressBar.style.width = progress + '%';
            thankYouProgressText.innerText = `${signedCount} sur 3 millions ont signé`;
        }

        // Fonction pour signer la pétition
        function signPetition() {
            signedCount++;
            localStorage.setItem('signedCount', signedCount); // Sauvegarde dans localStorage
            updateProgressBar();

            // Transition vers la page de félicitations
            document.getElementById('petition-container').classList.add('hidden');
            document.getElementById('thank-you-container').classList.remove('hidden');
        }

        // Fonction pour retourner à la pétition
        function goHome() {
            // Remise à zéro de l'affichage (comme si l'utilisateur n'avait pas encore signé)
            document.getElementById('thank-you-container').classList.add('hidden');
            document.getElementById('petition-container').classList.remove('hidden');
            updateProgressBar();
        }

        // Initialiser la page avec les valeurs existantes de signature
        updateProgressBar();
    </script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    flex-direction: column;
}

.container {
    text-align: center;
    background-color: #fff;
    padding: 40px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    width: 80%;
    max-width: 600px;
}

h1 {
    color: #f3a800;
}

.progress-container {
    width: 100%;
    background-color: #e0e0e0;
    border-radius: 25px;
    margin: 20px 0;
}

.progress-bar {
    height: 25px;
    background-color: #4caf50;
    width: 0;
    border-radius: 25px;
}

.btn-sign, .btn-home {
    background-color: #f3a800;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 18px;
}

.btn-sign:hover, .btn-home:hover {
    background-color: #e07b00;
}

.hidden {
    display: none;
}

.email-input {
    margin-bottom: 20px;
    padding: 10px;
    font-size: 16px;
    border-radius: 5px;
    width: 80%;
    max-width: 400px;
}
