<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prédiction de Match FIFA</title>
</head>
<body>
    <h2>Entrez les scores passés</h2>
    <input type="text" id="scoreInput" placeholder="Ex: 2-1">
    <button onclick="ajouterScore()">Ajouter Score</button>
    <button onclick="predireVainqueur()">Prédire</button>
    <p id="resultat"></p>

    <script>
        let scores = [];

        function ajouterScore() {
            let input = document.getElementById("scoreInput").value;
            if (/^\d+-\d+$/.test(input)) {
                scores.push(input);
                document.getElementById("scoreInput").value = "";
            } else {
                alert("Format invalide. Utilisez '2-1' par exemple.");
            }
        }

        function predireVainqueur() {
            let winA = 0, winB = 0, draw = 0;

            scores.forEach(score => {
                let [a, b] = score.split('-').map(Number);
                if (a > b) winA++;
                else if (b > a) winB++;
                else draw++;
            });

            let resultat = (winA > winB) ? "L'équipe A a plus de chances de gagner !" :
                           (winB > winA) ? "L'équipe B est favorite !" :
                           "Le match risque d'être nul !";

            document.getElementById("resultat").innerText = resultat;
            scores = [];
        }
    </script>
</body>
</html>
