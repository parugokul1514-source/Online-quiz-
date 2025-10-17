# Online-quiz-<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Online Random Quiz Application</title>
  <style>
    * {box-sizing: border-box;font-family: Arial, sans-serif;}
    body {
      margin: 0; padding: 0;
      background: #f0f4ff;
      display: flex; flex-direction: column;
      align-items: center; min-height: 100vh;
    }
    header {
      background: #2563eb; color: white;
      width: 100%; padding: 1rem;
      text-align: center; font-size: 1.5rem;
      box-shadow: 0 2px 6px rgba(0,0,0,0.2);
    }
    .quiz-container {
      background: white;
      max-width: 600px;
      width: 90%;
      border-radius: 12px;
      padding: 20px;
      margin-top: 30px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    .question {
      font-size: 1.2rem;
      margin-bottom: 15px;
      color: #111827;
    }
    .options {
      display: flex; flex-direction: column;
      gap: 10px;
    }
    .option {
      background: #f3f4f6;
      padding: 10px;
      border-radius: 8px;
      cursor: pointer;
      border: 2px solid transparent;
      transition: 0.2s;
    }
    .option:hover {
      border: 2px solid #2563eb;
      background: #e0ecff;
    }
    .selected {
      background: #2563eb;
      color: white;
    }
    .controls {
      display: flex;
      justify-content: space-between;
      margin-top: 20px;
    }
    button {
      background: #2563eb;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 1rem;
    }
    button:hover { background: #1d4ed8; }
    .result {
      text-align: center;
      font-size: 1.3rem;
      color: #111827;
    }
    .timer {
      text-align: right;
      font-weight: bold;
      color: #dc2626;
    }
  </style>
</head>
<body>
  <header>🎯 Online Random Quiz Application</header>

  <div class="quiz-container" id="quizBox">
    <div class="timer" id="timer">Time Left: 30s</div>
    <div class="question" id="question">Loading question...</div>
    <div class="options" id="options"></div>
    <div class="controls">
      <button id="nextBtn">Next</button>
    </div>
  </div>

  <div class="quiz-container" id="resultBox" style="display:none;">
    <div class="result" id="result"></div>
    <button id="restartBtn">Restart Quiz</button>
  </div>

  <script>
    // ---- Quiz Questions ----
    const questions = [
      {
        question: "Which language is used for web apps?",
        options: ["Python", "JavaScript", "C++", "Java"],
        answer: "JavaScript"
      },
      {
        question: "HTML stands for?",
        options: ["HyperText Markup Language", "HighText Machine Language", "HyperTransfer Markup Language", "None"],
        answer: "HyperText Markup Language"
      },
      {
        question: "CSS is used for?",
        options: ["Styling web pages", "Programming logic", "Database connection", "File management"],
        answer: "Styling web pages"
      },
      {
        question: "Which company developed Java?",
        options: ["Google", "IBM", "Sun Microsystems", "Microsoft"],
        answer: "Sun Microsystems"
      },
      {
        question: "What does SQL stand for?",
        options: ["Structured Query Language", "Stylish Question Language", "Statement Query Language", "None"],
        answer: "Structured Query Language"
      },
      {
        question: "Which tag is used to insert an image in HTML?",
        options: ["<img>", "<image>", "<src>", "<pic>"],
        answer: "<img>"
      },
      {
        question: "Which keyword is used to declare variables in JavaScript?",
        options: ["int", "var", "string", "declare"],
        answer: "var"
      },
      {
        question: "Which protocol is used for secure communication?",
        options: ["HTTP", "HTTPS", "FTP", "SMTP"],
        answer: "HTTPS"
      },
      {
        question: "Which of these is a backend framework?",
        options: ["React", "Django", "Bootstrap", "Vue"],
        answer: "Django"
      },
      {
        question: "What is the full form of API?",
        options: ["Application Programming Interface", "Applied Program Integration", "App Program Internet", "Advanced Programming Interface"],
        answer: "Application Programming Interface"
      },
      {
  question: "What is the main cause of global warming?",
  options: ["Deforestation", "Greenhouse gases", "Ozone layer", "Nuclear energy"],
  answer: "Greenhouse gases"
},
{
  question: "Which gas is known as a greenhouse gas?",
  options: ["Oxygen", "Carbon dioxide", "Nitrogen", "Helium"],
  answer: "Carbon dioxide"
},
{
  question: "Which layer of the atmosphere contains the ozone layer?",
  options: ["Troposphere", "Stratosphere", "Mesosphere", "Exosphere"],
  answer: "Stratosphere"
},
{
  question: "Which of the following is a renewable source of energy?",
  options: ["Coal", "Petroleum", "Solar energy", "Natural gas"],
  answer: "Solar energy"
},
{
  question: "Which country hosted the first Earth Summit in 1992?",
  options: ["USA", "Brazil", "India", "France"],
  answer: "Brazil"
},
{
  question: "Which of the following causes acid rain?",
  options: ["Sulphur dioxide and nitrogen oxides", "Carbon monoxide", "Methane", "CFCs"],
  answer: "Sulphur dioxide and nitrogen oxides"
},
{
  question: "Which gas is responsible for the depletion of the ozone layer?",
  options: ["CFCs", "CO2", "NO2", "Methane"],
  answer: "CFCs"
},
{
  question: "What is the full form of UNEP?",
  options: ["United Nations Environment Programme", "Universal Nature Energy Project", "Union for Natural Ecology Protection", "United Nations Energy Plan"],
  answer: "United Nations Environment Programme"
},
{
  question: "What is the primary greenhouse gas emitted by human activities?",
  options: ["Carbon dioxide", "Nitrous oxide", "Methane", "Ozone"],
  answer: "Carbon dioxide"
},
{
  question: "Which renewable resource is generated by moving air?",
  options: ["Solar", "Geothermal", "Wind", "Hydro"],
  answer: "Wind"
},
{
  question: "Deforestation leads to an increase in which gas?",
  options: ["Oxygen", "Carbon dioxide", "Nitrogen", "Hydrogen"],
  answer: "Carbon dioxide"
},
{
  question: "Which process converts waste into reusable materials?",
  options: ["Recycling", "Decomposition", "Composting", "Evaporation"],
  answer: "Recycling"
},
{
  question: "What type of pollution is caused by excessive noise?",
  options: ["Noise pollution", "Sound pollution", "Audio pollution", "Acoustic pollution"],
  answer: "Noise pollution"
},
{
  question: "What is the main source of water pollution?",
  options: ["Industrial waste", "Wind", "Solar rays", "Rainwater"],
  answer: "Industrial waste"
},
{
  question: "Which gas is used by plants during photosynthesis?",
  options: ["Oxygen", "Carbon dioxide", "Nitrogen", "Hydrogen"],
  answer: "Carbon dioxide"
},
{
  question: "Which is the largest source of renewable energy globally?",
  options: ["Wind", "Hydropower", "Solar", "Geothermal"],
  answer: "Hydropower"
},
{
  question: "Which day is celebrated as World Environment Day?",
  options: ["5th June", "22nd April", "16th September", "1st May"],
  answer: "5th June"
},
{
  question: "Which gas is essential for the survival of aquatic life?",
  options: ["Carbon dioxide", "Oxygen", "Nitrogen", "Methane"],
  answer: "Oxygen"
},
{
  question: "What is the main cause of soil erosion?",
  options: ["Deforestation", "Fertilizers", "Rainwater", "Snowfall"],
  answer: "Deforestation"
},
{
  question: "What is the most common method of waste disposal in India?",
  options: ["Landfilling", "Composting", "Incineration", "Dumping"],
  answer: "Dumping"
},
{
  question: "Which fuel causes the least air pollution?",
  options: ["Coal", "Petrol", "Natural gas", "Diesel"],
  answer: "Natural gas"
},
{
  question: "Which of the following is a non-renewable resource?",
  options: ["Wind energy", "Coal", "Solar power", "Biogas"],
  answer: "Coal"
},
{
  question: "What is the main purpose of afforestation?",
  options: ["Planting trees", "Cutting trees", "Building dams", "Fishing"],
  answer: "Planting trees"
},
{
  question: "Which country emits the highest amount of CO₂ globally?",
  options: ["India", "USA", "China", "Russia"],
  answer: "China"
},
{
  question: "Which gas do plants release during photosynthesis?",
  options: ["Oxygen", "Carbon dioxide", "Nitrogen", "Methane"],
  answer: "Oxygen"
},
{
  question: "Which environmental treaty controls greenhouse gas emissions?",
  options: ["Kyoto Protocol", "Montreal Protocol", "Paris Agreement", "Doha Declaration"],
  answer: "Kyoto Protocol"
},
{
  question: "What is the main pollutant from automobile exhaust?",
  options: ["Carbon monoxide", "Nitrogen", "Sulphur", "Hydrogen"],
  answer: "Carbon monoxide"
},
{
  question: "What is the full form of CFC?",
  options: ["Chloro Fluoro Carbon", "Carbon Fluoro Chloride", "Chemical Fuel Compound", "Chlorine Fuel Cell"],
  answer: "Chloro Fluoro Carbon"
},
{
  question: "Which renewable energy uses moving water?",
  options: ["Wind", "Geothermal", "Hydroelectric", "Solar"],
  answer: "Hydroelectric"
},
{
  question: "What is the term for species that are in danger of extinction?",
  options: ["Endangered", "Vulnerable", "Extinct", "Threatened"],
  answer: "Endangered"
},
{
  question: "What is biodiversity?",
  options: ["Variety of life forms", "Pollution control", "Weather pattern", "Type of soil"],
  answer: "Variety of life forms"
},
{
  question: "Which of these is not biodegradable?",
  options: ["Paper", "Plastic", "Vegetable peel", "Cotton cloth"],
  answer: "Plastic"
},
{
  question: "What does recycling help to conserve?",
  options: ["Resources", "Waste", "Land", "Rain"],
  answer: "Resources"
},
{
  question: "Which is an example of non-biodegradable waste?",
  options: ["Paper", "Plastic", "Food waste", "Cotton"],
  answer: "Plastic"
},
{
  question: "What does EIA stand for?",
  options: ["Environmental Impact Assessment", "Earth Inspection Agency", "Energy Investigation Association", "Eco Integrity Act"],
  answer: "Environmental Impact Assessment"
},
{
  question: "Which of these can cause waterborne diseases?",
  options: ["Contaminated water", "Clean air", "Pure rainwater", "Filtered water"],
  answer: "Contaminated water"
},
{
  question: "Which phenomenon leads to the rise of global temperature?",
  options: ["Greenhouse effect", "Acid rain", "Deforestation", "Smog"],
  answer: "Greenhouse effect"
},
{
  question: "Which renewable source uses sunlight?",
  options: ["Wind", "Solar", "Hydro", "Geothermal"],
  answer: "Solar"
},
{
  question: "What type of pollution affects aquatic life the most?",
  options: ["Water pollution", "Air pollution", "Noise pollution", "Soil pollution"],
  answer: "Water pollution"
},
{
  question: "Which energy source is formed from dead plants and animals?",
  options: ["Fossil fuels", "Solar", "Hydro", "Geothermal"],
  answer: "Fossil fuels"
},
{
  question: "Which process releases oxygen into the atmosphere?",
  options: ["Photosynthesis", "Respiration", "Combustion", "Evaporation"],
  answer: "Photosynthesis"
},
{
  question: "Which metal is most harmful in industrial waste?",
  options: ["Iron", "Mercury", "Aluminum", "Copper"],
  answer: "Mercury"
},
{
  question: "Which device reduces air pollution from factories?",
  options: ["Electrostatic precipitator", "Generator", "Transformer", "Condenser"],
  answer: "Electrostatic precipitator"
},
{
  question: "What is the primary aim of sustainable development?",
  options: ["To meet present needs without harming future generations", "To increase consumption", "To industrialize rapidly", "To exploit natural resources"],
  answer: "To meet present needs without harming future generations"
},
{
  question: "What type of waste are vegetable peels?",
  options: ["Biodegradable", "Non-biodegradable", "Industrial", "Hazardous"],
  answer: "Biodegradable"
},
{
  question: "Which organization monitors global climate change?",
  options: ["IPCC", "UNICEF", "WHO", "NASA"],
  answer: "IPCC"
},
{
  question: "Which gas causes acid rain when mixed with water?",
  options: ["SO₂ and NO₂", "CO₂ and O₂", "N₂ and H₂", "CH₄ and O₃"],
  answer: "SO₂ and NO₂"
},
{
  question: "Which of these is a greenhouse gas?",
  options: ["Methane", "Helium", "Hydrogen", "Argon"],
  answer: "Methane"
},
{
  question: "Which country has the Amazon Rainforest?",
  options: ["Brazil", "India", "Congo", "Indonesia"],
  answer: "Brazil"
},
{
  question: "Which renewable energy comes from Earth’s internal heat?",
  options: ["Geothermal", "Solar", "Wind", "Hydro"],
  answer: "Geothermal"
},
{
  question: "Which is the best way to reduce plastic pollution?",
  options: ["Recycling and reusing", "Burning plastic", "Throwing in landfills", "Dumping in oceans"],
  answer: "Recycling and reusing"
}
    ];

    // ---- Variables ----
    let currentIndex = 0;
    let score = 0;
    let timer;
    let timeLeft = 30;
    let randomQuestions = [];

    const questionBox = document.getElementById('question');
    const optionsBox = document.getElementById('options');
    const nextBtn = document.getElementById('nextBtn');
    const timerDisplay = document.getElementById('timer');
    const quizBox = document.getElementById('quizBox');
    const resultBox = document.getElementById('resultBox');
    const resultText = document.getElementById('result');
    const restartBtn = document.getElementById('restartBtn');

    // ---- Shuffle and Start Quiz ----
    function startQuiz() {
      score = 0;
      timeLeft = 30;
      randomQuestions = questions.sort(() => Math.random() - 0.5).slice(0, 5);
      currentIndex = 0;
      quizBox.style.display = "block";
      resultBox.style.display = "none";
      loadQuestion();
      startTimer();
    }

    // ---- Timer ----
    function startTimer() {
      clearInterval(timer);
      timer = setInterval(() => {
        timeLeft--;
        timerDisplay.textContent = `Time Left: ${timeLeft}s`;
        if (timeLeft <= 0) {
          clearInterval(timer);
          showResult();
        }
      }, 1000);
    }

    // ---- Load Question ----
    function loadQuestion() {
      const q = randomQuestions[currentIndex];
      questionBox.textContent = `${currentIndex + 1}. ${q.question}`;
      optionsBox.innerHTML = "";
      q.options.forEach(opt => {
        const div = document.createElement("div");
        div.classList.add("option");
        div.textContent = opt;
        div.onclick = () => selectOption(div, q.answer);
        optionsBox.appendChild(div);
      });
    }

    // ---- Select Option ----
    function selectOption(selected, correct) {
      document.querySelectorAll(".option").forEach(opt => opt.classList.remove("selected"));
      selected.classList.add("selected");
      if (selected.textContent === correct) score++;
    }

    // ---- Next Question ----
    nextBtn.addEventListener("click", () => {
      if (currentIndex < randomQuestions.length - 1) {
        currentIndex++;
        loadQuestion();
      } else {
        showResult();
      }
    });

    // ---- Show Result ----
    function showResult() {
      clearInterval(timer);
      quizBox.style.display = "none";
      resultBox.style.display = "block";
      resultText.textContent = `🎉 You scored ${score} out of ${randomQuestions.length}`;
    }

    restartBtn.addEventListener("click", startQuiz);

    // ---- Start Automatically ----
    startQuiz();
  </script>
</body>
</html>
