# POKEDEX
ShinyDex e Megas – Kanto
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Poketiba – Shinydex Kanto</title>
<style>
body {
    font-family: Arial, sans-serif;
    background: #f2f2f2;
    margin: 0;
    padding: 20px;
}

h1 {
    text-align: center;
}

#pokemon-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 15px;
}

.pokemon-card {
    background: white;
    border-radius: 10px;
    padding: 10px;
    text-align: center;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.pokemon-card img {
    width: 96px;
    height: 96px;
}

.pokemon-name {
    font-weight: bold;
    text-transform: capitalize;
}

.types {
    font-size: 12px;
    margin: 5px 0;
}

.stat {
    font-size: 13px;
    margin-top: 5px;
}
</style>
</head>
<body>

<h1>✨ Poketiba – Shinydex Kanto (Oficial)</h1>

<div id="pokemon-container"></div>

<script>
// ===============================
// 👉 ATUALIZE OS NÚMEROS AQUI 👈
// ===============================
const dataStats = {
    charizard: { shiny: 1, mega: 1 },
    blastoise: { shiny: 0, mega: 0 },
    venusaur: { shiny: 0, mega: 0 },
    beedrill: { shiny: 0, mega: 0 },
    aerodactyl: { shiny: 0, mega: 0 },
    kangaskhan: { shiny: 0, mega: 0 },
    pidgeot: { shiny: 0, mega: 0 },
    alakazam: { shiny: 0, mega: 0 },
    gengar: { shiny: 0, mega: 0 },
    gyarados: { shiny: 0, mega: 0 },
    pinsir: { shiny: 0, mega: 0 }
};

// Pokémon que possuem Mega
const megaPokemon = Object.keys(dataStats);

const container = document.getElementById("pokemon-container");

async function loadPokemon() {
    for (let i = 1; i <= 151; i++) {
        const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${i}`);
        const data = await response.json();

        const card = document.createElement("div");
        card.className = "pokemon-card";

        const img = document.createElement("img");
        img.src = data.sprites.front_default;

        const name = document.createElement("div");
        name.className = "pokemon-name";
        name.textContent = data.name;

        const types = document.createElement("div");
        types.className = "types";
        types.textContent = data.types.map(t => t.type.name).join(" / ");

        const shinyCount = dataStats[data.name]?.shiny ?? 0;

        const shinyText = document.createElement("div");
        shinyText.className = "stat";
        shinyText.textContent = `✨ Shinys capturados: ${shinyCount}`;

        card.appendChild(img);
        card.appendChild(name);
        card.appendChild(types);
        card.appendChild(shinyText);

        if (megaPokemon.includes(data.name)) {
            const megaCount = dataStats[data.name].mega;

            const megaText = document.createElement("div");
            megaText.className = "stat";
            megaText.textContent = `🧬 Megas feitos: ${megaCount}`;

            card.appendChild(megaText);
        }

        container.appendChild(card);
    }
}

loadPokemon();
</script>

</body>
</html>
