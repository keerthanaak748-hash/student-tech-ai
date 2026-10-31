# student-tech-ai

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Student Tech AI</title>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
}

body {
  background: #eef2ff;
  min-height: 100vh;
}

header {
  background: #263b80;
  color: white;
  padding: 20px;
  text-align: center;
}

.page {
  display: none;
  max-width: 650px;
  margin: 35px auto;
  padding: 20px;
}

.active {
  display: block;
}

.login-box {
  background: white;
  padding: 30px 22px;
  border-radius: 15px;
  box-shadow: 0 4px 15px #0002;
  text-align: center;
}

input {
  width: 100%;
  padding: 14px;
  margin: 15px 0;
  border: 1px solid #bbb;
  border-radius: 8px;
  font-size: 16px;
}

button {
  background: #263b80;
  color: white;
  border: none;
  padding: 13px 20px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 15px;
}

button:hover {
  background: #405bb5;
}

#chatbox {
  background: white;
  height: 430px;
  overflow-y: auto;
  padding: 15px;
  border-radius: 12px;
  margin: 15px 0;
}

.message {
  padding: 12px;
  border-radius: 10px;
  margin: 10px 0;
  max-width: 90%;
  line-height: 1.5;
  white-space: pre-wrap;
}

.user {
  background: #dbeafe;
  margin-left: auto;
}

.bot {
  background: #e9e9f5;
  margin-right: auto;
}

.chat-input {
  display: flex;
  gap: 8px;
}

.chat-input input {
  margin: 0;
  min-width: 0;
}

.chat-input button {
  min-width: 75px;
}

.top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
}

.small {
  font-size: 13px;
  color: #666;
  margin-top: 12px;
}

@media(max-width: 600px) {
  .page {
    margin: 15px auto;
  }
  #chatbox {
    height: 55vh;
  }
}
</style>
</head>

<body>

<header>
  <h2>🎓 Student Tech AI</h2>
  <p>Learn Technology • Ask Questions • Grow Your Skills</p>
</header>

<!-- LOGIN PAGE -->
<section id="loginPage" class="page active">

  <div class="login-box">
    <h2>Student Login</h2>
    <p style="margin-top:12px">
      Enter your mobile number to continue
    </p>

    <input
      type="tel"
      id="phone"
      placeholder="Enter 10-digit phone number"
      maxlength="10"
      inputmode="numeric"
    >

    <button onclick="login()">Login</button>

    <p class="small">
      Demo login: no OTP verification is enabled yet.
    </p>
  </div>

</section>

<!-- CHAT PAGE -->
<section id="chatPage" class="page">

  <div class="top">
    <div>
      <h2>Hello, Student!</h2>
      <p id="studentNumber"></p>
    </div>
    <button onclick="logout()">Logout</button>
  </div>

  <h3 style="margin-top:25px">💬 Technical Learning Chat</h3>

  <div id="chatbox">
    <div class="message bot">
      Hello! 👋 Welcome to Student Tech AI.

      Ask me any technical learning question.

      Examples:
      • What is Data Structure?
      • Explain Python.
      • What is an algorithm?
      • Explain DBMS.
      • What is Artificial Intelligence?
    </div>
  </div>

  <div class="chat-input">
    <input
      type="text"
      id="question"
      placeholder="Ask your technical question..."
      onkeydown="if(event.key==='Enter') sendMessage()"
    >
    <button onclick="sendMessage()">Send</button>
  </div>

  <p class="small">
    Current version: Demo learning assistant.
  </p>

</section>

<script>

// STUDENT LOGIN
function login() {
  let phone = document.getElementById("phone").value.trim();

  if (!/^[0-9]{10}$/.test(phone)) {
    alert("Please enter a valid 10-digit phone number");
    return;
  }

  localStorage.setItem("studentPhone", phone);
  openChat(phone);
}

// OPEN CHAT PAGE
function openChat(phone) {
  document.getElementById("loginPage").classList.remove("active");
  document.getElementById("chatPage").classList.add("active");

  document.getElementById("studentNumber").innerText =
    "Phone: " + phone;
}

// LOGOUT
function logout() {
  localStorage.removeItem("studentPhone");
  document.getElementById("chatPage").classList.remove("active");
  document.getElementById("loginPage").classList.add("active");
  document.getElementById("phone").value = "";
}

// ADD MESSAGE
function addMessage(message, type) {
  let chatbox = document.getElementById("chatbox");
  let div = document.createElement("div");

  div.className = "message " + type;
  div.textContent = message;

  chatbox.appendChild(div);
  chatbox.scrollTop = chatbox.scrollHeight;
}

// DEMO TECHNICAL ANSWERS
function getAnswer(question) {
  let q = question.toLowerCase();

  if (q.includes("data structure")) {
    return "Data Structure is a way of organizing and storing data efficiently.\n\nExamples:\n1. Array\n2. Stack\n3. Queue\n4. Linked List\n5. Tree\n6. Graph";
  }

  if (q.includes("python")) {
    return "Python is a high-level programming language. It is easy to learn and is used in AI, machine learning, web development and data science.";
  }

  if (q.includes("algorithm")) {
    return "An algorithm is a step-by-step procedure used to solve a problem.\n\nExample: An algorithm to add two numbers:\n1. Start\n2. Read A and B\n3. Calculate Sum = A + B\n4. Display Sum\n5. Stop";
  }

  if (q.includes("stack")) {
    return "Stack is a linear data structure that follows LIFO (Last In First Out).\n\nMain operations:\n1. Push - Insert an element.\n2. Pop - Remove an element.\n3. Peek - View the top element.\n\nExample: Stack of plates.";
  }

  if (q.includes("queue")) {
    return "Queue is a linear data structure that follows FIFO (First In First Out).\n\nOperations:\n1. Enqueue - Insert an element.\n2. Dequeue - Remove an element.\n\nExample: People standing in a line.";
  }

  if (q.includes("dbms")) {
    return "DBMS stands for Database Management System. It is software used to create, store, organize and manage data.\n\nExamples: MySQL, Oracle and PostgreSQL.";
  }

  if (q.includes("artificial intelligence") || q.includes("what is ai")) {
    return "Artificial Intelligence (AI) is a branch of computer science that enables machines to perform tasks that normally require human intelligence.\n\nExamples:\n1. Chatbots\n2. Voice assistants\n3. Image recognition\n4. Recommendation systems";
  }

  if (q.includes("html")) {
    return "HTML stands for HyperText Markup Language. It is used to create the structure of web pages.\n\nCommon tags:\n1. <html>\n2. <head>\n3. <body>\n4. <h1>\n5. <p>";
  }

  if (q.includes("java")) {
    return "Java is a high-level, object-oriented programming language. It is used for application development, enterprise software and Android development.";
  }

  if (q.includes("computer network")) {
    return "A Computer Network is a group of interconnected computers that share information and resources.\n\nExamples: LAN, MAN and WAN.";
  }

  if (q.includes("operating system")) {
    return "An Operating System (OS) is system software that manages computer hardware and software resources.\n\nExamples: Windows, Linux, Android and macOS.";
  }

  return "I don't have a prepared answer for this question in the demo version.\n\nTry asking about Python, Java, HTML, Stack, Queue, DBMS, Algorithms or Data Structures.\n\nA real AI connection will allow me to answer a much wider range of technical questions.";
}

// SEND CHAT MESSAGE
function sendMessage() {
  let input = document.getElementById("question");
  let question = input.value.trim();

  if (question === "") {
    return;
  }

  addMessage(question, "user");
  input.value = "";

  setTimeout(function() {
    let answer = getAnswer(question);
    addMessage(answer, "bot");
  }, 500);
}

// RESTORE LOGIN
window.onload = function() {
  let phone = localStorage.getItem("studentPhone");

  if (phone) {
    openChat(phone);
  }
};

</script>

</body>
</html>

