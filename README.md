<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JS Event Playground</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Interactive Playground </h1>

  <button id="magicBtn">Click Me!</button>
  <p id="textOutput"></p>

  <div id="gallery">
    <img id="galleryImg" src="image1.jpg" alt="Gallery" />
    <button onclick="nextImage()">Next</button>
  </div>

  <div class="tabs">
    <button onclick="openTab('tab1')">Tab 1</button>
    <button onclick="openTab('tab2')">Tab 2</button>
    <div id="tab1" class="tab-content">Content for Tab 1</div>
    <div id="tab2" class="tab-content" style="display:none;">Content for Tab 2</div>
  </div>

  <form id="signupForm" class="form-container">
  <h2>Sign Up</h2>

  <div class="form-group">
    <label for="name">Full Name</label>
    <input type="text" id="name" placeholder="Enter your name" required>
  </div>

  <div class="form-group">
    <label for="email">Email Address</label>
    <input type="email" id="email" placeholder="you@example.com" required>
  </div>

  <div class="form-group">
    <label for="password">Password</label>
    <input type="password" id="password" placeholder="Min 8 characters" required>
  </div>

  <button type="submit" class="form-button">Register</button>

  <p id="formFeedback" class="form-feedback"></p>
</form>

  <script src="script.js"></script>
</body>
</html>

body {
  font-family: sans-serif;
  padding: 2rem;
  background: #f9f9f9;
}

button {
  padding: 0.5rem 1rem;
  border-radius: 10px;
  cursor: pointer;
}

.tab-content {
  border: 1px solid #ccc;
  padding: 1rem;
  margin-top: 1rem;
  background: white;
}
.form-container {
  max-width: 400px;
  margin: 3rem auto;
  padding: 2rem;
  background: white;
  border-radius: 15px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
  font-family: 'Segoe UI', sans-serif;
}

.form-container h2 {
  text-align: center;
  margin-bottom: 1.5rem;
  color: #333;
}

.form-group {
  margin-bottom: 1.2rem;
}

label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 600;
  color: #555;
}

input {
  width: 100%;
  padding: 0.7rem;
  border: 1px solid #ccc;
  border-radius: 8px;
  transition: border 0.3s ease;
}

input:focus {
  border-color: #4a90e2;
  outline: none;
  box-shadow: 0 0 5px rgba(74, 144, 226, 0.5);
}

.form-button {
  width: 100%;
  padding: 0.75rem;
  border: none;
  border-radius: 8px;
  background: #4a90e2;
  color: white;
  font-size: 1rem;
  cursor: pointer;
  transition: red 0.3s ease;
}

.form-button:hover {
  background: #357ab8;
}

.form-feedback {
  margin-top: 1rem;
  font-weight: 500;
  text-align: center;
  color: #c0392b; /* red for error by default */
}

.form-feedback.valid {
  color: #27ae60; /* green for valid */
}

// Button Click
document.getElementById("magicBtn").addEventListener("click", () => {
  document.getElementById("textOutput").innerText = "You clicked the button!";
});

// Hover
document.getElementById("magicBtn").addEventListener("mouseover", () => {
  document.getElementById("magicBtn").style.backgroundColor = "#ffcc00";
});

// Keypress
document.addEventListener("keydown", (e) => {
  console.log(`You pressed: ${e.key}`);
});

// Double-click
document.getElementById("magicBtn").addEventListener("dblclick", () => {
  alert("Secret double-click activated!");
});

// Tabs
function openTab(tabId) {
  document.querySelectorAll(".tab-content").forEach(tab => tab.style.display = "none");
  document.getElementById(tabId).style.display = "block";
}

// Slideshow logic
let images = ["image1.jpg", "image2.jpg", "image3.jpg"];
let currentImg = 0;
function nextImage() {
  currentImg = (currentImg + 1) % images.length;
  document.getElementById("galleryImg").src = images[currentImg];
}

// Form Validation
document.getElementById("signupForm").addEventListener("submit", function(e) {
  e.preventDefault();

  const email = document.getElementById("email").value;
  const password = document.getElementById("password").value;
  const feedback = document.getElementById("formFeedback");

  const emailValid = /^[\w-.]+@([\w-]+\.)+[\w-]{2,4}$/.test(email);
  if (!emailValid) {
    feedback.textContent = "Invalid email format.";
    return;
  }

  if (password.length < 8) {
    feedback.textContent = "Password must be at least 8 characters.";
    return;
  }

  feedback.textContent = "Form is valid!";
});

const emailInput = document.getElementById("email");
const passwordInput = document.getElementById("password");
const feedback = document.getElementById("formFeedback");

emailInput.addEventListener("input", () => {
  const email = emailInput.value;
  const valid = /^[\w-.]+@([\w-]+\.)+[\w-]{2,4}$/.test(email);
  feedback.textContent = valid ? "Valid email" : "Invalid email";
  feedback.className = valid ? "form-feedback valid" : "form-feedback";
});

passwordInput.addEventListener("input", () => {
  const password = passwordInput.value;
  if (password.length < 8) {
    feedback.textContent = "Password must be at least 8 characters";
    feedback.className = "form-feedback";
  } else {
    feedback.textContent = "Strong password";
    feedback.className = "form-feedback valid";
  }
});
