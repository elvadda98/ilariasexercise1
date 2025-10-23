<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Everyday Terms</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #6a93cb 0%, #a4bfef 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .word-bank h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(74, 111, 165, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(74, 111, 165, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #4a6fa5;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .option.selected {
            background: #4a6fa5;
            color: white;
            border-color: #4a6fa5;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #4a6fa5;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #4a6fa5;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #4a6fa5;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #4a6fa5;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #4a6fa5;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #4a6fa5;
            margin-top: 10px;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/12</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Everyday Terms</h1>
            <p>Test your knowledge of these English terms!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Vocabulary Explanations</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>advise</h3>
                    <p><strong>Definition:</strong> To offer suggestions about the best course of action to someone.</p>
                    <p><strong>Usage:</strong> Used when giving recommendations or guidance.</p>
                    <p class="example"><strong>Example:</strong> "I would advise you to arrive early for the interview."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>day-off</h3>
                    <p><strong>Definition:</strong> A day when you do not have to work or go to school.</p>
                    <p><strong>Usage:</strong> Refers to a free day from work or regular duties.</p>
                    <p class="example"><strong>Example:</strong> "I'm taking a day-off next Friday to go to the dentist."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>manner</h3>
                    <p><strong>Definition:</strong> A way in which something is done or happens; method or style.</p>
                    <p><strong>Usage:</strong> Describes how someone behaves or how something is done.</p>
                    <p class="example"><strong>Example:</strong> "She spoke in a polite and respectful manner."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>wild</h3>
                    <p><strong>Definition:</strong> Living or growing in natural environments; not domesticated or cultivated.</p>
                    <p><strong>Usage:</strong> Describes animals, plants, or areas in their natural state.</p>
                    <p class="example"><strong>Example:</strong> "We saw wild deer in the forest during our hike."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>plains</h3>
                    <p><strong>Definition:</strong> Large areas of flat land with few trees.</p>
                    <p><strong>Usage:</strong> Refers to extensive flat geographical areas.</p>
                    <p class="example"><strong>Example:</strong> "The American plains are known for their vast open spaces."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>in the end</h3>
                    <p><strong>Definition:</strong> Finally; after everything has been considered.</p>
                    <p><strong>Usage:</strong> Used to indicate the final outcome or conclusion.</p>
                    <p class="example"><strong>Example:</strong> "We had many difficulties, but in the end we succeeded."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>shame</h3>
                    <p><strong>Definition:</strong> A painful feeling of humiliation or distress caused by wrong or foolish behavior.</p>
                    <p><strong>Usage:</strong> Describes the emotion of guilt or embarrassment.</p>
                    <p class="example"><strong>Example:</strong> "He felt deep shame after lying to his friend."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>furthermore</h3>
                    <p><strong>Definition:</strong> In addition; besides (used to introduce a fresh consideration in an argument).</p>
                    <p><strong>Usage:</strong> A formal transition word to add more information.</p>
                    <p class="example"><strong>Example:</strong> "The product is affordable; furthermore, it's environmentally friendly."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>due to</h3>
                    <p><strong>Definition:</strong> Because of; as a result of.</p>
                    <p><strong>Usage:</strong> Used to indicate the cause of something.</p>
                    <p class="example"><strong>Example:</strong> "The flight was cancelled due to bad weather conditions."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>issues</h3>
                    <p><strong>Definition:</strong> Important topics or problems for debate or discussion.</p>
                    <p><strong>Usage:</strong> Refers to problems, concerns, or subjects of discussion.</p>
                    <p class="example"><strong>Example:</strong> "The company is addressing several technical issues with the software."</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">advise</span>
                    <span class="word-option">day-off</span>
                    <span class="word-option">manner</span>
                    <span class="word-option">wild</span>
                    <span class="word-option">plains</span>
                    <span class="word-option">in the end</span>
                    <span class="word-option">shame</span>
                    <span class="word-option">furthermore</span>
                    <span class="word-option">due to</span>
                    <span class="word-option">issues</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="advise" onclick="selectMatch(this)">advise</div>
                    <div class="match-item" data-word="day-off" onclick="selectMatch(this)">day-off</div>
                    <div class="match-item" data-word="manner" onclick="selectMatch(this)">manner</div>
                    <div class="match-item" data-word="wild" onclick="selectMatch(this)">wild</div>
                    <div class="match-item" data-word="plains" onclick="selectMatch(this)">plains</div>
                    <div class="match-item" data-word="in the end" onclick="selectMatch(this)">in the end</div>
                    <div class="match-item" data-word="shame" onclick="selectMatch(this)">shame</div>
                    <div class="match-item" data-word="furthermore" onclick="selectMatch(this)">furthermore</div>
                    <div class="match-item" data-word="due to" onclick="selectMatch(this)">due to</div>
                    <div class="match-item" data-word="issues" onclick="selectMatch(this)">issues</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "advise" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To ignore someone's opinion</div>
                    <div class="option" onclick="selectOption(this, true)">To offer suggestions about the best course of action</div>
                    <div class="option" onclick="selectOption(this, false)">To criticize someone harshly</div>
                    <div class="option" onclick="selectOption(this, false)">To agree with someone completely</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: What is a "day-off"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A very busy work day</div>
                    <div class="option" onclick="selectOption(this, true)">A day when you don't have to work</div>
                    <div class="option" onclick="selectOption(this, false)">A day with extra work hours</div>
                    <div class="option" onclick="selectOption(this, false)">A day for important meetings</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: What does "manner" refer to?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">The time something happens</div>
                    <div class="option" onclick="selectOption(this, true)">The way in which something is done</div>
                    <div class="option" onclick="selectOption(this, false)">The place where something occurs</div>
                    <div class="option" onclick="selectOption(this, false)">The reason something happens</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: What does "wild" describe?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Domesticated animals</div>
                    <div class="option" onclick="selectOption(this, true)">Living in natural environments</div>
                    <div class="option" onclick="selectOption(this, false)">Urban areas</div>
                    <div class="option" onclick="selectOption(this, false)">Industrial zones</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: What are "plains"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Mountainous regions</div>
                    <div class="option" onclick="selectOption(this, true)">Large areas of flat land</div>
                    <div class="option" onclick="selectOption(this, false)">Coastal areas</div>
                    <div class="option" onclick="selectOption(this, false)">Forest areas</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: What does "in the end" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">At the beginning</div>
                    <div class="option" onclick="selectOption(this, true)">Finally; after everything</div>
                    <div class="option" onclick="selectOption(this, false)">During the process</div>
                    <div class="option" onclick="selectOption(this, false)">Unexpectedly</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 7: What is "shame"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A feeling of pride</div>
                    <div class="option" onclick="selectOption(this, true)">A painful feeling of humiliation</div>
                    <div class="option" onclick="selectOption(this, false)">A sense of accomplishment</div>
                    <div class="option" onclick="selectOption(this, false)">A moment of happiness</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 8: What does "furthermore" do in a sentence?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Contradicts previous information</div>
                    <div class="option" onclick="selectOption(this, true)">Adds more information</div>
                    <div class="option" onclick="selectOption(this, false)">Summarizes the main point</div>
                    <div class="option" onclick="selectOption(this, false)">Introduces a different topic</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 9: What does "due to" indicate?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">The solution to a problem</div>
                    <div class="option" onclick="selectOption(this, true)">The cause of something</div>
                    <div class="option" onclick="selectOption(this, false)">The timing of an event</div>
                    <div class="option" onclick="selectOption(this, false)">The location of something</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 10: What are "issues"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Simple solutions</div>
                    <div class="option" onclick="selectOption(this, true)">Important topics or problems</div>
                    <div class="option" onclick="selectOption(this, false)">Celebrations</div>
                    <div class="option" onclick="selectOption(this, false)">Daily routines</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>
            
            <button class="reset-btn" onclick="resetMultipleChoice()">Reset Answers</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let multipleChoiceCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "advise", text: "To offer suggestions about the best course of action" },
            { meaning: "day-off", text: "A day when you do not have to work" },
            { meaning: "manner", text: "The way in which something is done" },
            { meaning: "wild", text: "Living in natural environments" },
            { meaning: "plains", text: "Large areas of flat land" },
            { meaning: "in the end", text: "Finally; after everything has been considered" },
            { meaning: "shame", text: "A painful feeling of humiliation" },
            { meaning: "furthermore", text: "In addition; besides" },
            { meaning: "due to", text: "Because of; as a result of" },
            { meaning: "issues", text: "Important topics or problems for discussion" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "I would <input type='text' class='fill-blank' data-answer='advise' placeholder='answer'> you to arrive early for the interview.", answer: "advise" },
            { text: "I'm taking a <input type='text' class='fill-blank' data-answer='day-off' placeholder='answer'> next Friday to go to the dentist.", answer: "day-off" },
            { text: "She spoke in a polite and respectful <input type='text' class='fill-blank' data-answer='manner' placeholder='answer'>.", answer: "manner" },
            { text: "We saw <input type='text' class='fill-blank' data-answer='wild' placeholder='answer'> deer in the forest during our hike.", answer: "wild" },
            { text: "The American <input type='text' class='fill-blank' data-answer='plains' placeholder='answer'> are known for their vast open spaces.", answer: "plains" },
            { text: "We had many difficulties, but <input type='text' class='fill-blank' data-answer='in the end' placeholder='answer'> we succeeded.", answer: "in the end" },
            { text: "He felt deep <input type='text' class='fill-blank' data-answer='shame' placeholder='answer'> after lying to his friend.", answer: "shame" },
            { text: "The product is affordable; <input type='text' class='fill-blank' data-answer='furthermore' placeholder='answer'>, it's environmentally friendly.", answer: "furthermore" },
            { text: "The flight was cancelled <input type='text' class='fill-blank' data-answer='due to' placeholder='answer'> bad weather conditions.", answer: "due to" },
            { text: "The company is addressing several technical <input type='text' class='fill-blank' data-answer='issues' placeholder='answer'> with the software.", answer: "issues" },
            { text: "My doctor <input type='text' class='fill-blank' data-answer='advised' placeholder='answer'> me to exercise regularly.", answer: "advised" },
            { text: "After working for six days straight, I really need a <input type='text' class='fill-blank' data-answer='day-off' placeholder='answer'>.", answer: "day-off" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences
            const shuffledSentences = shuffleArray([...sentences]);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Question ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            
            // Count correct answers in multiple choice
            multipleChoiceCorrect = document.querySelectorAll('#multiple-choice .option.correct.selected').length;
            updateScore();
        }

        function resetMultipleChoice() {
            document.querySelectorAll('#multiple-choice .option').forEach(option => {
                option.classList.remove('selected', 'correct', 'incorrect');
            });
            
            document.querySelectorAll('#multiple-choice .feedback').forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            multipleChoiceCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score
            score = fillBlanksCorrect + matchingCorrect + multipleChoiceCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
