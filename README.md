# Grade12-all-subjects-
Flash cards website 
<!DOCTYPE html>
<html lang="my">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Grade 12 Flashcards & Quiz</title>
<style>
:root {
  --primary: #3b82f6;
  --primary-hover: #2563eb;
  --bg-color: #f8fafc;
  --card-bg: #ffffff;
  --text-main: #1e293b;
  --text-muted: #64748b;
  --border-color: #e2e8f0;
  --success: #10b981;
}

body {
  font-family: system-ui, -apple-system, sans-serif;
  background: var(--bg-color);
  margin: 0;
  color: var(--text-main);
  line-height: 1.5;
}

header {
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
  color: white;
  padding: 32px 16px;
  text-align: center;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
}

header h1 {
  margin: 0 0 8px 0;
  font-size: 1.75rem;
}

header p {
  margin: 0;
  opacity: 0.9;
  font-size: 0.95rem;
}

main {
  max-width: 650px;
  margin: 24px auto;
  padding: 0 16px;
}

.box {
  background: var(--card-bg);
  padding: 24px;
  border-radius: 16px;
  margin-bottom: 20px;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1);
  border: 1px solid var(--border-color);
}

.tabs {
  display: flex;
  gap: 8px;
  margin-bottom: 20px;
}

.tabs button {
  flex: 1;
  padding: 10px;
  border: 1px solid var(--border-color);
  background: #f1f5f9;
  color: var(--text-main);
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
}

.tabs button.active {
  background: var(--primary);
  color: white;
  border-color: var(--primary);
}

label {
  display: block;
  margin: 16px 0 6px;
  font-weight: 600;
  font-size: 0.9rem;
}

select, input, textarea {
  width: 100%;
  box-sizing: border-box;
  padding: 12px;
  border: 1px solid var(--border-color);
  border-radius: 8px;
  font-size: 1rem;
  background: #fff;
  color: var(--text-main);
  transition: border-color 0.2s;
}

select:focus, input:focus, textarea:focus {
  outline: none;
  border-color: var(--primary);
}

button.action-btn {
  padding: 12px 20px;
  border: 0;
  border-radius: 8px;
  background: var(--primary);
  color: white;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s;
}

button.action-btn:hover {
  background: var(--primary-hover);
}

.card {
  background: #f8fafc;
  border: 2px dashed var(--border-color);
  border-radius: 12px;
  padding: 24px;
  text-align: center;
  min-height: 160px;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-bottom: 16px;
  transition: border-color 0.2s;
}

.card:hover {
  border-color: var(--primary);
}

.card h3 {
  margin: 0 0 12px 0;
  font-size: 1.2rem;
}

#answer {
  display: none;
  color: var(--success);
  font-weight: 600;
  margin-top: 10px;
  white-space: pre-wrap;
}

.nav-controls {
  display: flex;
  gap: 10px;
  justify-content: space-between;
}

.nav-controls button {
  flex: 1;
}

.hidden {
  display: none !important;
}

.option {
  display: block;
  width: 100%;
  text-align: left;
  background: #f8fafc;
  border: 1px solid var(--border-color);
  color: var(--text-main);
  padding: 12px;
  border-radius: 8px;
  margin-bottom: 8px;
  cursor: pointer;
  font-size: 1rem;
  transition: all 0.2s;
}

.option:hover:not(:disabled) {
  background: #f1f5f9;
  border-color: var(--primary);
}

.option.correct {
  background: #d1fae5;
  border-color: var(--success);
  color: #065f46;
}

.option.wrong {
  background: #fee2e2;
  border-color: #ef4444;
  color: #991b1b;
}

.small {
  color: var(--text-muted);
  font-size: 0.85rem;
  text-align: center;
}

#count {
  font-weight: 600;
  color: var(--text-muted);
  margin-bottom: 12px;
}

#message {
  margin-top: 12px;
  font-weight: 600;
  color: var(--success);
}
</style>
</head>
<body>

<header>
<h1>📚 Grade 12 Flashcards & Quiz</h1>
<p>လေ့လာရန် • မေးခွန်းဖြေဆိုရန် • မေးခွန်းအသစ်များထည့်ရန်</p>
</header>

<main>

<div class="box">
  <div class="tabs">
    <button id="tabStudyBtn" onclick="switchTab('study')">Flashcards</button>
    <button id="tabQuizBtn" onclick="switchTab('quiz')">Quiz</button>
    <button id="tabAddBtn" onclick="switchTab('add')">Add Questions</button>
  </div>

  <label for="subject">Subject / ဘာသာရပ်</label>
  <select id="subject" onchange="onSubjectChange()">
    <option value="Myanmar">Myanmar</option>
    <option value="English">English</option>
    <option value="Chemistry">Chemistry</option>
    <option value="Biology">Biology</option>
  </select>

  <label for="chapter" id="chapterLabel">Category / အခန်း</label>
  <select id="chapter" onchange="renderFlashcard()"></select>
</div>

<!-- Flashcard Section -->
<section id="study" class="box">
  <div id="count"></div>
  <div class="card" onclick="toggleAnswer()">
    <h3 id="question">Question</h3>
    <div id="answer">Answer</div>
    <p class="small" style="margin-top: 15px;">(ကတ်ကိုနှိပ်၍ အဖြေကြည့်ပါ)</p>
  </div>
  <div class="nav-controls">
    <button class="action-btn" onclick="moveCard(-1)">← ရှေ့သို့</button>
    <button class="action-btn" onclick="toggleAnswer()">အဖြေပြမည်</button>
    <button class="action-btn" onclick="moveCard(1)">နောက်သို့ →</button>
  </div>
</section>

<!-- Quiz Section -->
<section id="quiz" class="box hidden">
  <h2>Quiz စာမေးပွဲ</h2>
  <p id="quizQuestion" style="font-weight: 600; margin: 16px 0;">Quiz စတင်ရန် ခလုတ်ကိုနှိပ်ပါ။</p>
  <div id="options"></div>
  <p id="result" style="font-weight: 600; margin: 12px 0;"></p>
  <button class="action-btn" id="quizActionBtn" onclick="handleQuizAction()">Start Quiz</button>
</section>

<!-- Add Question Section -->
<section id="add" class="box hidden">
  <h2>မေးခွန်းအသစ်ထည့်ရန်</h2>

  <label for="newSubject">Subject</label>
  <select id="newSubject" onchange="updateNewChapters()">
    <option value="Myanmar">Myanmar</option>
    <option value="English">English</option>
    <option value="Chemistry">Chemistry</option>
    <option value="Biology">Biology</option>
  </select>

  <label for="newChapter" id="newChapterLabel">Category</label>
  <select id="newChapter"></select>

  <label for="title" id="titleLabel">ခေါင်းစဉ်အမည် (လိုအပ်ပါက)</label>
  <input id="title" placeholder="ဥပမာ - ကဗျာခေါင်းစဉ်">

  <label for="newQ">Question / မေးခွန်း</label>
  <textarea id="newQ" rows="3" placeholder="မေးခွန်းရေးပါ"></textarea>

  <label for="newA">Answer / အဖြေ</label>
  <textarea id="newA" rows="3" placeholder="အဖြေရေးပါ"></textarea>

  <button class="action-btn" style="margin-top: 12px;" onclick="addCard()">Save Question</button>
  <p id="message"></p>
</section>

<p class="small">Your personal Grade 12 study website</p>
</main>

<script>
const config = {
  Myanmar: { label: "Category / အမျိုးအစား", items: ["ကဗျာ", "ဝတ္ထု", "စာစီစာကုံး", "သဒ္ဒါ", "ဖတ်စာ", "အခြားခေါင်းစဉ်"] },
  English: { label: "Unit", items: Array.from({ length: 12 }, (_, i) => "Unit " + (i + 1)) },
  Chemistry: { label: "Chapter", items: Array.from({ length: 8 }, (_, i) => "Chapter " + (i + 1)) },
  Biology: { label: "Chapter", items: Array.from({ length: 6 }, (_, i) => "Chapter " + (i + 1)) }
};

const sampleData = [
  { subject: "English", chapter: "Unit 1", title: "Vocabulary", q: "What is a synonym?", a: "A word with the same or nearly the same meaning." },
  { subject: "Chemistry", chapter: "Chapter 1", title: "Chemistry", q: "What is the formula of baking soda?", a: "NaHCO₃" },
  { subject: "Biology", chapter: "Chapter 1", title: "Cell", q: "Which organelle produces most ATP?", a: "Mitochondria" }
];

let cards = [];
try {
  cards = JSON.parse(localStorage.getItem("grade12_v2")) || sampleData;
} catch (e) {
  cards = [...sampleData];
}

let currentIdx = 0;
let quizList = [], quizIdx = 0, score = 0, answered = false;

const $ = id => document.getElementById(id);

function saveData() {
  try {
    localStorage.setItem("grade12_v2", JSON.stringify(cards));
  } catch (e) {
    alert("ဒေတာသိမ်းဆည်းရာတွင် အမှားအယွင်းရှိပါသည်။");
  }
}

function populateChapters(subjectKey, selectId, labelId) {
  const selectElem = $(selectId);
  selectElem.innerHTML = "";
  config[subjectKey].items.forEach(item => {
    const opt = document.createElement("option");
    opt.value = item;
    opt.textContent = item;
    selectElem.appendChild(opt);
  });
  if (labelId && config[subjectKey]) {
    $(labelId).textContent = config[subjectKey].label;
  }
}

function onSubjectChange() {
  populateChapters($("subject").value, "chapter", "chapterLabel");
  currentIdx = 0;
  renderFlashcard();
  resetQuizState();
}

function updateNewChapters() {
  const subj = $("newSubject").value;
  populateChapters(subj, "newChapter", "newChapterLabel");
  $("titleLabel").textContent = subj === "Myanmar" ? "ခေါင်းစဉ်အမည်" : "ခေါင်းစဉ်အမည် (လိုအပ်ပါက)";
}

function getFilteredCards() {
  const subj = $("subject").value;
  const chap = $("chapter").value;
  return cards.filter(c => c.subject === subj && c.chapter === chap);
}

function renderFlashcard() {
  const list = getFilteredCards();
  if (currentIdx >= list.length) currentIdx = 0;
  
  if (list.length === 0) {
    $("count").textContent = "ဒီအခန်းမှာ မေးခွန်းမရှိသေးပါ။";
    $("question").textContent = "မေးခွန်းအသစ် ထည့်ပါ";
    $("answer").textContent = "";
    $("answer").style.display = "none";
    return;
  }

  $("count").textContent = `မေးခွန်း ${currentIdx + 1} / ${list.length}`;
  const current = list[currentIdx];
  $("question").textContent = (current.title ? current.title + " — " : "") + current.q;
  $("answer").textContent = current.a;
  $("answer").style.display = "none";
}

function toggleAnswer() {
  const ansElem = $("answer");
  ansElem.style.display = ansElem.style.display === "block" ? "none" : "block";
}

function moveCard(step) {
  const list = getFilteredCards();
  if (list.length === 0) return;
  currentIdx = (currentIdx + step + list.length) % list.length;
  renderFlashcard();
}

function switchTab(tabId) {
  ["study", "quiz", "add"].forEach(id => {
    $(id).classList.toggle("hidden", id !== tabId);
  });
  ["tabStudyBtn", "tabQuizBtn", "tabAddBtn"].forEach((btnId, idx) => {
    const tabs = ["study", "quiz", "add"];
    $(btnId).classList.toggle("active", tabs[idx] === tabId);
  });
}

function addCard() {
  const subject = $("newSubject").value;
  const chapter = $("newChapter").value;
  const title = $("title").value.trim();
  const q = $("newQ").value.trim();
  const a = $("newA").value.trim();

  if (!q || !a) {
    $("message").style.color = "#ef4444";
    $("message").textContent = "မေးခွန်းနှင့် အဖြေကို မဖြစ်မနေ ဖြည့်သွင်းပါ။";
    return;
  }

  cards.push({ subject, chapter, title, q, a });
  saveData();

  $("message").style.color = "var(--success)";
  $("message").textContent = "မေးခွန်းအသစ် သိမ်းဆည်းပြီးပါပြီ။";
  $("newQ").value = "";
  $("newA").value = "";
  $("title").value = "";

  $("subject").value = subject;
  onSubjectChange();
  $("chapter").value = chapter;
  currentIdx = getFilteredCards().length - 1;
  renderFlashcard();
}

function resetQuizState() {
  quizList = [];
  quizIdx = 0;
  score = 0;
  answered = false;
  $("quizQuestion").textContent = "Quiz စတင်ရန် ခလုတ်ကိုနှိပ်ပါ။";
  $("options").innerHTML = "";
  $("result").textContent = "";
  $("quizActionBtn").textContent = "Start Quiz";
  $("quizActionBtn").classList.remove("hidden");
}

function handleQuizAction() {
  const list = getFilteredCards();
  if (list.length === 0) {
    $("quizQuestion").textContent = "ဒီအခန်းမှာ မေးခွန်းမရှိသေးပါ။ အရင်မေးခွန်းထည့်ပါ။";
    return;
  }
  
  if (quizList.length === 0) {
    // Start Quiz
    quizList = [...list].sort(() => Math.random() - 0.5);
    quizIdx = 0;
    score = 0;
    $("quizActionBtn").classList.add("hidden");
    showQuizQuestion();
  }
}

function showQuizQuestion() {
  answered = false;
  const current = quizList[quizIdx];
  $("quizQuestion").textContent = `မေးခွန်း ${quizIdx + 1} / ${quizList.length}: ${current.q}`;
  $("options").innerHTML = "";
  $("result").textContent = "";

  // Get wrong options
  const wrongOptions = cards
    .filter(c => c.a !== current.a)
    .sort(() => Math.random() - 0.5)
    .slice(0, 3)
    .map(c => c.a);

  const choices = [...new Set([current.a, ...wrongOptions])].sort(() => Math.random() - 0.5);

  choices.forEach(ansText => {
    const btn = document.createElement("button");
    btn.className = "option";
    btn.textContent = ansText;
    btn.onclick = () => checkAnswer(btn, ansText, current.a);
    $("options").appendChild(btn);
  });
}

function checkAnswer(selectedBtn, selectedAns, correctAns) {
  if (answered) return;
  answered = true;

  const optionButtons = $("options").children;
  Array.from(optionButtons).forEach(btn => {
    btn.disabled = true;
    if (btn.textContent === correctAns) {
      btn.classList.add("correct");
    } else if (btn === selectedBtn) {
      btn.classList.add("wrong");
    }
  });

  if (selectedAns === correctAns) {
    score++;
    $("result").style.color = "var(--success)";
    $("result").textContent = "မှန်ပါတယ်! 🎉";
  } else {
    $("result").style.color = "#ef4444";
    $("result").textContent = `အမှားပါ။ အဖြေမှန်မှာ: ${correctAns}`;
  }

  // Show Next Button
  const actionBtn = $("quizActionBtn");
  actionBtn.classList.remove("hidden");
  actionBtn.textContent = quizIdx < quizList.length - 1 ? "နောက်မေးခွန်းသို့ →" : "ရလဒ်ကြည့်ရန်";
  actionBtn.onclick = proceedQuiz;
}

function proceedQuiz() {
  quizIdx++;
  if (quizIdx < quizList.length) {
    $("quizActionBtn").classList.add("hidden");
    showQuizQuestion();
  } else {
    $("quizQuestion").textContent = `🎉 Quiz ပြီးဆုံးပါပြီ! သင်ရရှိသည့်အမှတ်: ${score} / ${quizList.length}`;
    $("options").innerHTML = "";
    $("result").textContent = "";
    $("quizActionBtn").textContent = "Quiz အသစ်စတင်ရန်";
    $("quizActionBtn").onclick = () => {
      resetQuizState();
      handleQuizAction();
    };
  }
}

// Initializing application
populateChapters("Myanmar", "chapter", "chapterLabel");
populateChapters("Myanmar", "newChapter", "newChapterLabel");
switchTab("study");
renderFlashcard();
</script>

</body>
</html>
