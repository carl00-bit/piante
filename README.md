<!DOCTYPE html>
<html lang="it">
<head>
  <meta charset="UTF-8">
  <title>Quiz 3x2 con Risposte Testuali</title>
  <style>
    body {
  font-family: 'Segoe UI', Arial, sans-serif;
  font-size: 1.1em;
  color:rgb(255, 255, 255);
  background-color:rgb(10, 53, 0);
  max-width: 600px;
  margin: 40px auto;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0,0,0,0.4);
  }
  button {
  margin: 10px 5px;
    padding: 10px 20px;
    background-color:rgb(29, 78, 18);
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 1em;
    }
  button:hover {
    background-color:rgb(55, 217, 58);
    }
 #result {
    margin-top: 30px;
    font-weight: bold;
    font-size: 1.2em;
    color:rgb(255, 255, 255);
    }
  </style>
</head>
<body>

  <h1>Che pianta sei?</h1>
  <div id="question-container"></div>
  <div id="result"></div>

  <script>
    const domande = [
      { type: "finta", text: "Ti consideri una persona socievole o solitaria?", options: ["Socievole", "Solitaria"] },
      { type: "vera", id: "Q1", text: "In una festa è più probabile che parli con tante persone o che tu stia con un gruppo ristretto?", options: ["Parli", "Ristretto"] },
      { type: "finta", text: "D'estate preferisci prendere il sole o stare sotto l'ombrellone?", options: ["Sole", "Ombrellone"] },
      { type: "vera", id: "Q2", text: "I tuoi amici organizzano una passeggiata sulla neve: preferiresti andare o rimanere davanti al camino?", options: ["Vai", "Rimani"] },
      { type: "finta", text: "Vesti casual o vivace?", options: ["Casual", "Vivace"] },
      { type: "vera", id: "Q3", text: "Quando spesso ricevi complimenti  sul tuo look?", options: ["Spesso", "Mai"] }
    ];

    const risultati = {
      "Parli-Vai-Spesso": "Sei un'ortensia",
      "Parli-Vai-Mai": "Sei una felce",
      "Parli-Rimani-Spesso": "Sei un geranio",
      "Parli-Rimani-Mai": "Sei un'edera del diavolo",
      "Ristretto-Vai-Spesso": "Sei una primula",
      "Ristretto-Vai-Mai": "Sei un cactus",
      "Ristretto-Rimani-Spesso": "Sei una begonia",
      "Ristretto-Rimani-Mai": "Sei una lingua di suocera"
    };

    let currentIndex = 0;
    const risposteVere = [];

    function mostraDomanda() {
      const container = document.getElementById("question-container");
      container.innerHTML = "";

      if (currentIndex >= domande.length) {
        mostraRisultato();
        return;
      }

      const domanda = domande[currentIndex];
      const p = document.createElement("p");
      p.textContent = domanda.text;
      container.appendChild(p);

      domanda.options.forEach((opzione) => {
        const btn = document.createElement("button");
        btn.textContent = opzione;
        btn.onclick = () => {
          if (domanda.type === "vera") {
            risposteVere.push(opzione);
          }
          currentIndex++;
          mostraDomanda();
        };
        container.appendChild(btn);
      });
    }

    function mostraRisultato() {
      const codice = risposteVere.join("-");
      const testo = risultati[codice] || "Combinazione non prevista.";
      document.getElementById("result").textContent = `Risultato: ${testo}`;
    }

    mostraDomanda();
  </script>

</body>
</html>
