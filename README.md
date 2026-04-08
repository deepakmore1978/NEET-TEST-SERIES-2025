MHT CET TEST SERIES
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MHT CET 2026 Mock Test | PCM</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 0; padding: 20px; background: #f4f4f4; }
        .container { max-width: 900px; margin: auto; background: white; padding: 20px; border-radius: 10px; box-shadow: 0 0 15px rgba(0,0,0,0.2); }
        h1 { text-align: center; color: #1e3a8a; }
        .timer { text-align: center; font-size: 24px; font-weight: bold; color: #dc2626; margin: 15px 0; }
        .section { margin: 30px 0; }
        .question { margin-bottom: 25px; padding: 15px; border: 1px solid #ddd; border-radius: 8px; background: #fafafa; }
        .options label { display: block; margin: 8px 0; cursor: pointer; }
        button { padding: 12px 25px; margin: 10px 5px; background: #1e40af; color: white; border: none; border-radius: 6px; cursor: pointer; font-size: 16px; }
        button:hover { background: #1e3a8a; }
        .result { display: none; text-align: center; font-size: 20px; margin-top: 30px; padding: 20px; background: #ecfdf5; border-radius: 10px; }
        .nav { text-align: center; margin-top: 20px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>MHT CET 2026 Mock Test (PCM)</h1>
        <div class="timer" id="timer">Time Left: <span id="time">180:00</span></div>

        <div id="instructions">
            <h2>Instructions</h2>
            <p>• Total Questions: 150 (Physics 50 + Chemistry 50 + Mathematics 50)</p>
            <p>• Total Marks: 200 (Phy+Chem: 1 mark each | Maths: 2 marks each)</p>
            <p>• No Negative Marking | Attempt All Questions</p>
            <p>• Section 1 (Physics + Chemistry): First 90 minutes</p>
            <p>• Section 2 (Mathematics): Next 90 minutes</p>
            <button onclick="startTest()">Start Mock Test</button>
        </div>

        <div id="test" style="display: none;">
            <!-- Questions will be injected by JavaScript -->
        </div>

        <div class="result" id="result">
            <h2>Your Score</h2>
            <p id="scoreDetails"></p>
            <p id="percentage"></p>
            <button onclick="location.reload()">Restart Test</button>
        </div>
    </div>

    <script>
        // Sample Questions (You can add more or replace with your own)
        const questions = [
            // Physics (Questions 0-49 in real test)
            { q: "1. The SI unit of force is:", options: ["Newton", "Joule", "Watt", "Pascal"], ans: 0, subject: "Physics", marks: 1 },
            { q: "2. Dimensional formula of Planck's constant is:", options: ["[ML²T⁻¹]", "[MLT⁻¹]", "[M⁰L²T⁻¹]", "[ML²T⁻²]"], ans: 0, subject: "Physics", marks: 1 },
            // Add more Physics questions here...

            // Chemistry (50 questions)
            { q: "51. IUPAC name of CH₃COOH is:", options: ["Ethanoic acid", "Methanoic acid", "Propanoic acid", "Butanoic acid"], ans: 0, subject: "Chemistry", marks: 1 },
            // Add more Chemistry questions...

            // Mathematics (50 questions)
            { q: "101. Value of ∫ dx/(x²+1) from 0 to 1 is:", options: ["π/4", "π/2", "1", "∞"], ans: 0, subject: "Mathematics", marks: 2 },
            { q: "102. If sinθ + cosθ = 1, then sin2θ =", options: ["0", "1", "2", "-1"], ans: 0, subject: "Mathematics", marks: 2 }
            // Add total 150 questions for full mock
        ];

        // For demo, we are using only a few questions. You can expand the array to 150.

        let currentTime = 10800; // 180 minutes in seconds
        let timerInterval;
        let answers = {};

        function startTest() {
            document.getElementById("instructions").style.display = "none";
            document.getElementById("test").style.display = "block";
            renderQuestions();
            startTimer();
        }

        function startTimer() {
            timerInterval = setInterval(() => {
                currentTime--;
                let min = Math.floor(currentTime / 60);
                let sec = currentTime % 60;
                document.getElementById("time").textContent = `${min}:${sec < 10 ? '0' : ''}${sec}`;

                if (currentTime <= 0) {
                    clearInterval(timerInterval);
                    submitTest();
                }
            }, 1000);
        }

        function renderQuestions() {
            let html = `<h2>Section 1: Physics & Chemistry</h2>`;
            questions.forEach((q, index) => {
                html += `
                    <div class="question">
                        <p><strong>${q.q}</strong></p>
                        <div class="options">
                            ${q.options.map((opt, i) => `
                                <label>
                                    <input type="radio" name="q${index}" value="${i}" onclick="saveAnswer(${index}, ${i})">
                                    ${opt}
                                </label>
                            `).join('')}
                        </div>
                    </div>`;
            });
            html += `<div class="nav"><button onclick="submitTest()">Submit Test</button></div>`;
            document.getElementById("test").innerHTML = html;
        }

        function saveAnswer(qIndex, option) {
            answers[qIndex] = option;
        }

        function submitTest() {
            clearInterval(timerInterval);
            let score = 0;

            questions.forEach((q, index) => {
                if (answers[index] !== undefined && answers[index] === q.ans) {
                    score += q.marks;
                }
            });

            const totalMarks = 200;
            const percentage = ((score / totalMarks) * 100).toFixed(2);

            document.getElementById("test").style.display = "none";
            document.getElementById("result").style.display = "block";

            document.getElementById("scoreDetails").innerHTML = `
                Your Score: <strong>${score} / 200</strong><br>
                Physics + Chemistry: ${Math.min(score, 100)} / 100 (approx)<br>
                Mathematics: ${score > 100 ? (score - 100) : 0} / 100
            `;
            document.getElementById("percentage").innerHTML = `
                Percentage: <strong>${percentage}%</strong><br>
                ${percentage >= 90 ? "Excellent Performance!" : percentage >= 75 ? "Very Good!" : "Keep Practicing!"}
            `;
        }
    </script>
</body>
</html>
