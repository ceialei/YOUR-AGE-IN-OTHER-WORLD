<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Your Age on Other Worlds</title>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: Arial, sans-serif;
    color: white;
    background: linear-gradient(180deg, #080b24, #17113b, #070b1c);
}

header {
    text-align: center;
    padding: 35px 15px;
    background: #101632;
    border-bottom: 2px solid #7c5cff;
}

header h1 {
    color: #f8d66d;
    margin-bottom: 10px;
    font-size: 2.2rem;
}

header p {
    color: #d7d9f5;
}

.student {
    line-height: 1.8;
    color: #c9d2ff;
    margin-top: 20px;
}

.container {
    max-width: 1100px;
    margin: auto;
    padding: 25px 16px;
}

.calculator {
    background: rgba(255,255,255,0.08);
    padding: 25px;
    border-radius: 18px;
    text-align: center;
    border: 1px solid #514b87;
}

label {
    display: block;
    margin: 15px 0 8px;
    font-weight: bold;
}

input, select {
    width: 100%;
    max-width: 350px;
    padding: 12px;
    border-radius: 8px;
    border: none;
    font-size: 16px;
}

button {
    background: #8b72ff;
    color: white;
    border: none;
    padding: 12px 20px;
    margin: 12px 5px 0;
    border-radius: 8px;
    font-size: 15px;
    font-weight: bold;
    cursor: pointer;
}

button:hover {
    background: #6b50e8;
}

#message {
    color: #ffd6d6;
    margin-top: 12px;
}

#result {
    display: none;
    background: #131a3b;
    padding: 20px;
    margin-top: 20px;
    border-radius: 12px;
    overflow-wrap: anywhere;
}

#result h2 {
    color: #f8d66d;
}

.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 18px;
    margin-top: 30px;
}

.planet {
    background: rgba(255,255,255,0.08);
    border: 1px solid #44436e;
    padding: 20px;
    border-radius: 15px;
    text-align: center;
    transition: transform 0.2s;
}

.planet:hover {
    transform: translateY(-5px);
    border-color: #a997ff;
}

.planet-symbol {
    font-size: 55px;
    margin: 8px;
}

.planet h3 {
    color: #f8d66d;
    margin: 8px 0;
}

.planet p {
    color: #d6d9f4;
    font-size: 14px;
    line-height: 1.6;
}

.age {
    font-size: 21px;
    color: #9ee8ff;
    font-weight: bold;
    margin-top: 12px;
}

footer {
    text-align: center;
    padding: 25px 10px;
    color: #bfc3e9;
    font-size: 13px;
}

@media (max-width: 480px) {
    header h1 {
        font-size: 1.7rem;
    }

    .calculator {
        padding: 18px;
    }
}
</style>
</head>

<body>

<header>
    <h1>🚀 Your Age on Other Worlds</h1>
    <p>Discover how old you would be on the planets of our solar system!</p>

    <div class="student">
        <strong>Student Name:</strong> YOUR FULL NAME<br>
        <strong>Course:</strong> YOUR COURSE<br>
        <strong>Section:</strong> YOUR SECTION
    </div>
</header>

<main class="container">

    <section class="calculator">
        <h2>🌎 Calculate Your Space Age</h2>
        <p>Enter your birthday to discover your age on other worlds.</p>

        <label for="birthday">Your Birthday</label>
        <input type="date" id="birthday">

        <label for="planetChoice">Choose a Planet or World</label>
        <select id="planetChoice">
            <option value="all">All Nine Worlds</option>
            <option value="Mercury">Mercury</option>
            <option value="Venus">Venus</option>
            <option value="Earth">Earth</option>
            <option value="Mars">Mars</option>
            <option value="Jupiter">Jupiter</option>
            <option value="Saturn">Saturn</option>
            <option value="Uranus">Uranus</option>
            <option value="Neptune">Neptune</option>
            <option value="Pluto">Pluto (Dwarf Planet)</option>
        </select>

        <br>
        <button onclick="calculateAge()">Calculate My Age</button>
        <button onclick="resetCalculator()">Reset</button>

        <p id="message"></p>
        <div id="result" aria-live="polite"></div>
    </section>

    <section>
        <h2 style="text-align:center; margin-top:40px;">
            🪐 Meet the Nine Worlds
        </h2>
        <p style="text-align:center; color:#d6d9f4;">
            Each world takes a different amount of time to orbit the Sun.
        </p>

        <div class="grid" id="planetGrid"></div>
    </section>

</main>

<footer>
    <p>Made for an educational project about our solar system.</p>
    <p>Note: Pluto is classified as a dwarf planet.</p>
</footer>

<script>
const planets = [
    {
        name: "Mercury",
        symbol: "☿️",
        days: 88,
        description: "The smallest planet and the closest planet to the Sun."
    },
    {
        name: "Venus",
        symbol: "♀️",
        days: 225,
        description: "A very hot planet with a thick atmosphere."
    },
    {
        name: "Earth",
        symbol: "🌍",
        days: 365,
        description: "Our home planet, where life is known to exist."
    },
    {
        name: "Mars",
        symbol: "🔴",
        days: 687,
        description: "The Red Planet, known for its dusty surface."
    },
    {
        name: "Jupiter",
        symbol: "🟠",
        days: 4380,
        description: "The largest planet in our solar system."
    },
    {
        name: "Saturn",
        symbol: "🪐",
        days: 10767.5,
        description: "A gas giant famous for its beautiful rings."
    },
    {
        name: "Uranus",
        symbol: "🔵",
        days: 30660,
        description: "An ice giant that rotates on its side."
    },
    {
        name: "Neptune",
        symbol: "🔷",
        days: 60152,
        description: "A distant, cold world with powerful winds."
    },
    {
        name: "Pluto",
        symbol: "❄️",
        days: 248 * 365,
        description: "A dwarf planet in the distant Kuiper Belt."
    }
];

// Display all nine worlds on the page.
function displayPlanets() {
    const grid = document.getElementById("planetGrid");

    grid.innerHTML = planets.map(planet => `
        <article class="planet">
            <div class="planet-symbol">${planet.symbol}</div>
            <h3>${planet.name}</h3>
            <p>${planet.description}</p>
            <p><strong>One year:</strong><br>
            ${planet.days.toLocaleString()} Earth days</p>
            <div class="age" id="age-${planet.name}">
                Enter your birthday!
            </div>
        </article>
    `).join("");
}

// Calculate the number of Earth days lived.
function calculateAge() {
    const birthdayValue = document.getElementById("birthday").value;
    const choice = document.getElementById("planetChoice").value;
    const message = document.getElementById("message");
    const result = document.getElementById("result");

    message.textContent = "";
    result.style.display = "none";

    if (!birthdayValue) {
        message.textContent = "Please enter your birthday first.";
        return;
    }

    const birthday = new Date(birthdayValue + "T00:00:00");
    const today = new Date();

    // Compare calendar dates without including the current time.
    const birthUTC = Date.UTC(
        birthday.getFullYear(),
        birthday.getMonth(),
        birthday.getDate()
    );

    const todayUTC = Date.UTC(
        today.getFullYear(),
        today.getMonth(),
        today.getDate()
    );

    if (Number.isNaN(birthUTC) || birthUTC > todayUTC) {
        message.textContent = "Please enter a valid birthday that is not in the future.";
        return;
    }

    const earthDaysLived = Math.floor(
        (todayUTC - birthUTC) / (1000 * 60 * 60 * 24)
    );

    const selectedPlanets = choice === "all"
        ? planets
        : planets.filter(planet => planet.name === choice);

    // Clear old ages before showing the new calculation.
    planets.forEach(planet => {
        document.getElementById("age-" + planet.name).textContent =
            "Enter your birthday!";
    });

    let output = `
        <h2>Your Space Age Results</h2>
        <p><strong>Earth days lived:</strong>
        ${earthDaysLived.toLocaleString()} days</p>
    `;

    selectedPlanets.forEach(planet => {
        const age = earthDaysLived / planet.days;

        document.getElementById("age-" + planet.name).textContent =
            age.toFixed(2) + " years old";

        output += `
            <p>
                ${planet.symbol} <strong>${planet.name}:</strong>
                ${age.toFixed(2)} years old
            </p>
        `;
    });

    output += `
        <p><em>Your planetary age is calculated by dividing your
        Earth days lived by the length of one year on that world.</em></p>
    `;

    result.innerHTML = output;
    result.style.display = "block";
}

function resetCalculator() {
    document.getElementById("birthday").value = "";
    document.getElementById("planetChoice").value = "all";
    document.getElementById("message").textContent = "";
    document.getElementById("result").style.display = "none";

    planets.forEach(planet => {
        document.getElementById("age-" + planet.name).textContent =
            "Enter your birthday!";
    });
}

displayPlanets();
</script>

</body>
</html>
