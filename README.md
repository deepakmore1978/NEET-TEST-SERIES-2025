MHT CET TEST SERIES
<!DOCTYPE html>
<div class="container">
        <header>
            <h1>MHT CET 2026 Mock Test (PCM)</h1>
            <p>Total Marks: 200 | No Negative Marking</p>
        </header>

        <div class="timer" id="timer">
            Time Left: <span id="time">180:00</span>
        </div>

        <div id="test-container">
            <!-- Questions will be loaded here by JavaScript -->
        </div>

        <div class="result" id="result">
            <h2>Your Final Score</h2>
            <div class="score" id="score">0 / 200</div>
            <p id="percentage" style="font-size:24px; margin:15px 0;"></p>
            <button onclick="location.reload()">Restart Mock Test</button>
        </div>
    </div>

    <script>
        // ==================== MHT CET SAMPLE QUESTIONS ====================
        const questions = [
            // Physics (10 Questions)
            {
                q: "1. A body moving with uniform acceleration has a velocity of 12 m/s at t=0 and 18 m/s at t=3s. The displacement in 3 seconds is:",
                options: ["45 m", "27 m", "36 m", "54 m"],
                correct: 0
            },
            {
                q: "2. The dimensional formula of Planck's constant is:",
                options: ["[ML²T⁻¹]", "[MLT⁻¹]", "[M⁰L²T⁻¹]", "[ML²T⁻²]"],
                correct: 0
            },
            {
                q: "3. The SI unit of electric flux is:",
                options: ["N m²/C", "N/C", "V m", "Coulomb"],
                correct: 0
            },

            // Chemistry (10 Questions)
            {
                q: "11. The IUPAC name of CH₃CH₂COOH is:",
                options: ["Propanoic acid", "Ethanoic acid", "Butanoic acid", "Pentanoic acid"],
                correct: 0
            },
            {
                q: "12. Which of the following is a strong electrolyte?",
                options: ["Glucose", "Urea", "NaCl", "Ethanol"],
                correct: 2
            },
            {
                q: "13. The number of sigma and pi bonds in C₂H₂ are respectively:",
                options: ["3, 2", "2, 3", "3, 1", "2, 2"],
                correct: 0
            },

            // Mathematics (10 Questions)
            {
                q: "21. The value of ∫ from 0 to π/2 of sin x dx is:",
                options: ["1", "0", "π/2", "2"],
                correct: 0
            },
            {
                q: "22. If the roots of the equation x² - 5x + 6 = 0 are α and β, then α + β is:",
                options: ["5", "-5", "6", "-6"],
                correct: 0
            },
            {
                q: "23. The derivative of sin(2x) with respect to x is:",
                options: ["2 cos(2x)", "cos(2x)", "-2 sin(2x)", "2 sin(2x)"],
                correct: 0
            }
            // You can add 120 more questions here following the same format
        ];

        let answers = {};
        let timeLeft = 10800; // 180 minutes in seconds
        let timer;

        function startTimer() {
            timer = setInterval(() => {
                timeLeft--;
                let minutes = Math.floor(timeLeft / 60);
                let seconds = timeLeft % 60;
                document.getElementById("time").textContent = 
                    `${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;

                if (timeLeft <= 300) {
                    document.getElementById("timer").style.color = "#b91c1c";
                }

                if (timeLeft <= 0) {
                    clearInterval(timer);
                    submitTest();
                }
            }, 1000);
        }

        function renderQuestions() {
            let html = '';
            questions.forEach((q, index) => {
                html += `
                    <div class="question">
                        <div class="question-number">Question ${index + 1}</div>
                        <div class="question-text">${q.q}</div>
                        <div class="options">
                            ${q.options.map((option, i) => `
                                <div class="option" onclick="selectAnswer(${index}, ${i})">
                                    <input type="radio" name="q${index}" id="q${index}o${i}" ${answers[index] === i ? 'checked' : ''}>
                                    <label for="q${index}o${i}">${String.fromCharCode(65 + i)}. ${option}</label>
                                </div>
                            `).join('')}
                        </div>
                    </div>`;
            });

            html += `<button onclick="submitTest()">Submit Test & See Score</button>`;
            document.getElementById("test-container").innerHTML = html;
        }

        function selectAnswer(qIndex, optionIndex) {
            answers[qIndex] = optionIndex;
        }

        function submitTest() {
            clearInterval(timer);
            
            let score = 0;
            let totalPossible = 0;

            questions.forEach((q, index) => {
                const userAnswer = answers[index];
                if (userAnswer !== undefined && userAnswer === q.correct) {
                    // Physics & Chemistry = 1 mark, Maths = 2 marks (based on question number)
                    const marks = (index < 20) ? 1 : 2;
                    score += marks;
                }
                totalPossible += (index < 20) ? 1 : 2;
            });

            document.getElementById("test-container").style.display = "none";
            const resultDiv = document.getElementById("result");
            resultDiv.style.display = "block";

            const percentage = ((score / 200) * 100).toFixed(1);

            document.getElementById("score").textContent = `${score} / 200`;
            document.getElementById("percentage").innerHTML = `
                Percentage: <strong>${percentage}%</strong><br>
                ${percentage >= 85 ? "🎉 Excellent Performance!" : 
                  percentage >= 70 ? "👍 Very Good!" : 
                  percentage >= 55 ? "✅ Good! Keep Improving" : "📚 Need More Practice"}
            `;
        }

        // Initialize the test
        window.onload = function() {
            renderQuestions();
            startTimer();
        };
    </script>
</body>
