  To use please download this[ai-study-buddy.html](https://github.com/user-attachments/files/27778953/ai-study-buddy.html)
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>AI Study Buddy</title>
    <link rel="stylesheet" href="./styles.css" />
  </head>
  <body>
    <div class="app-shell">
      <aside class="sidebar" aria-label="Study Buddy navigation">
        <div class="brand">
          <div class="brand-mark">SB</div>
          <div>
            <strong>Study Buddy</strong>
            <span>AI learning workspace</span>
          </div>
        </div>
        <nav class="nav-list">
          <button class="nav-item active" data-view="dashboard" title="Dashboard">⌂ <span>Dashboard</span></button>
          <button class="nav-item" data-view="tutor" title="AI tutor">✦ <span>AI Tutor</span></button>
          <button class="nav-item" data-view="notes" title="Notes">✎ <span>Notes</span></button>
          <button class="nav-item" data-view="cards" title="Flashcards">▣ <span>Flashcards</span></button>
          <button class="nav-item" data-view="quiz" title="Quiz">? <span>Quiz</span></button>
          <button class="nav-item" data-view="planner" title="Planner">☑ <span>Planner</span></button>
          <button class="nav-item" data-view="focus" title="Focus timer">◷ <span>Focus</span></button>
        </nav>
        <div class="sidebar-footer">
          <span id="todayLabel"></span>
          <button id="resetApp" class="ghost-button">Reset data</button>
        </div>
      </aside>

      <main class="main-content">
        <header class="topbar">
          <div>
            <p class="eyebrow">Today’s study plan</p>
            <h1 id="pageTitle">Dashboard</h1>
          </div>
          <div class="subject-picker">
            <label for="subjectInput">Subject</label>
            <input id="subjectInput" type="text" placeholder="Biology, math, history..." />
          </div>
        </header>

        <section id="dashboard" class="view active">
          <div class="hero-band">
            <div class="hero-copy">
              <p class="eyebrow">AI Study Buddy</p>
              <h2>Turn messy study time into guided practice.</h2>
              <p>Ask for explanations, convert notes into flashcards, generate quick quizzes, plan sessions, and track focused minutes in one workspace.</p>
              <div class="hero-actions">
                <button class="primary-button" data-jump="tutor">Start studying</button>
                <button class="secondary-button" data-jump="notes">Add notes</button>
              </div>
            </div>
            <div class="hero-panel" aria-label="Study progress summary">
              <div>
                <span class="metric" id="focusMinutes">0</span>
                <span class="metric-label">focused minutes</span>
              </div>
              <div>
                <span class="metric" id="cardsCount">0</span>
                <span class="metric-label">flashcards</span>
              </div>
              <div>
                <span class="metric" id="tasksCount">0</span>
                <span class="metric-label">open tasks</span>
              </div>
            </div>
          </div>

          <div class="dashboard-grid">
            <article class="panel">
              <div class="panel-heading">
                <h3>Smart Suggestions</h3>
                <button class="icon-button" id="refreshSuggestions" title="Refresh suggestions">↻</button>
              </div>
              <ul id="suggestionsList" class="suggestion-list"></ul>
            </article>
            <article class="panel">
              <div class="panel-heading">
                <h3>Next Tasks</h3>
                <button class="ghost-button" data-jump="planner">Open planner</button>
              </div>
              <ul id="miniTasks" class="task-list"></ul>
            </article>
          </div>
        </section>

        <section id="tutor" class="view">
          <div class="workspace two-column">
            <article class="panel chat-panel">
              <div class="panel-heading">
                <h3>AI Tutor</h3>
                <select id="tutorMode">
                  <option value="explain">Explain</option>
                  <option value="quiz">Quiz me</option>
                  <option value="plan">Plan</option>
                  <option value="simplify">Simplify</option>
                </select>
              </div>
              <div id="chatLog" class="chat-log" aria-live="polite"></div>
              <form id="chatForm" class="composer">
                <textarea id="chatInput" rows="3" placeholder="Ask about a topic, paste a confusing paragraph, or request a study plan..."></textarea>
                <button class="primary-button" type="submit">Send</button>
              </form>
            </article>
            <aside class="panel">
              <h3>Quick Prompts</h3>
              <div class="prompt-list">
                <button data-prompt="Explain this topic like I am new to it:">Explain simply</button>
                <button data-prompt="Quiz me with five questions about:">Quiz me</button>
                <button data-prompt="Create a 45-minute study plan for:">Make a plan</button>
                <button data-prompt="Give me memory hooks for:">Memory hooks</button>
              </div>
            </aside>
          </div>
        </section>

        <section id="notes" class="view">
          <div class="workspace two-column">
            <article class="panel">
              <div class="panel-heading">
                <h3>Study Notes</h3>
                <button id="summarizeNotes" class="secondary-button">Summarize</button>
              </div>
              <textarea id="notesInput" class="notes-box" placeholder="Paste lecture notes, textbook sections, or your own rough notes here."></textarea>
              <div class="note-actions">
                <button id="makeCards" class="primary-button">Create flashcards</button>
                <button id="makeQuiz" class="secondary-button">Create quiz</button>
              </div>
            </article>
            <article class="panel">
              <h3>AI Summary</h3>
              <div id="summaryOutput" class="summary-output">Add notes and generate a summary when you are ready.</div>
            </article>
          </div>
        </section>

        <section id="cards" class="view">
          <div class="workspace">
            <article class="panel">
              <div class="panel-heading">
                <h3>Flashcards</h3>
                <button id="addCard" class="secondary-button">Add card</button>
              </div>
              <div class="card-creator">
                <input id="cardQuestion" type="text" placeholder="Question or term" />
                <input id="cardAnswer" type="text" placeholder="Answer or definition" />
                <button id="saveCard" class="primary-button">Save</button>
              </div>
              <div id="flashcardDeck" class="flashcard-deck"></div>
            </article>
          </div>
        </section>

        <section id="quiz" class="view">
          <div class="workspace two-column">
            <article class="panel">
              <div class="panel-heading">
                <h3>Practice Quiz</h3>
                <button id="generateQuiz" class="secondary-button">Generate from notes</button>
              </div>
              <div id="quizArea" class="quiz-area"></div>
            </article>
            <article class="panel">
              <h3>Score</h3>
              <div class="score-box">
                <span id="quizScore">0%</span>
                <p id="quizFeedback">Answer questions to get feedback.</p>
              </div>
            </article>
          </div>
        </section>

        <section id="planner" class="view">
          <div class="workspace two-column">
            <article class="panel">
              <div class="panel-heading">
                <h3>Planner</h3>
                <button id="autoPlan" class="secondary-button">Auto-plan</button>
              </div>
              <form id="taskForm" class="task-form">
                <input id="taskInput" type="text" placeholder="Task, chapter, assignment, or exam topic" />
                <input id="taskDate" type="date" />
                <button class="primary-button" type="submit">Add</button>
              </form>
              <ul id="plannerList" class="task-list large"></ul>
            </article>
            <article class="panel">
              <h3>Study Blocks</h3>
              <div id="studyBlocks" class="study-blocks"></div>
            </article>
          </div>
        </section>

        <section id="focus" class="view">
          <div class="focus-layout">
            <article class="panel timer-panel">
              <p class="eyebrow">Focus session</p>
              <div id="timerDisplay" class="timer-display">25:00</div>
              <div class="timer-controls">
                <button id="startTimer" class="primary-button">Start</button>
                <button id="pauseTimer" class="secondary-button">Pause</button>
                <button id="resetTimer" class="ghost-button">Reset</button>
              </div>
              <div class="timer-settings">
                <label>Minutes <input id="timerMinutes" type="number" min="5" max="90" value="25" /></label>
              </div>
            </article>
            <article class="panel">
              <h3>Focus Tips</h3>
              <ul class="suggestion-list">
                <li>Pick one task before starting the timer.</li>
                <li>Keep a scratch line for distractions and return to them later.</li>
                <li>After each session, write one sentence about what improved.</li>
              </ul>
            </article>
          </div>
        </section>
      </main>
    </div>

    <script src="./app.js"></script>
  </body>
</html>
