---
layout: base 
title: Accounts
search_exclude: true
permalink: /tools/accounts
---

## What Is PII?
**PII (Personal Identifiable Information)** is any detail that can identify you—like your name, address, or account info.
In this course, you may share or work with PII. Let’s make sure it’s handled wisely.

<div style="display: flex; align-items: flex-start; gap: 24px; margin-top: 20px;">
  <img src="{{site.baseurl}}/images/accounts.png" alt="PII graphic" style="width:50%; max-width:400px; border-radius: 12px;"/>
  <div id="pii-container"></div>
</div>

<script>
  const piiData = {
    Public: [
      "Name, Email, Photo",
      "Schools, City, Property",
      "Credit Reports, Router Info"
    ],
    Sensitive: [
      "Birthdate, Address, Phone",
      "Place of Birth, Maiden Names",
      "Driver’s License"
    ],
    Private: [
      "Social Security Number",
      "Login Credentials",
      "Two-Factor Sources"
    ]
  };
  const container = document.getElementById("pii-container");
  const heading = document.createElement("h3");
  heading.textContent = "Know Your PII";
  container.appendChild(heading);
  Object.entries(piiData).forEach(([category, items]) => {
    const button = document.createElement("button");
    button.textContent = `▶ ${category}`;
    button.style.margin = "10px 0";
    button.style.padding = "8px 14px";
    button.style.border = "none";
    button.style.borderRadius = "8px";
    button.style.backgroundColor = "#2c2a5d";  // dark blue/purple
    button.style.color = "white";
    button.style.fontSize = "16px";
    button.style.cursor = "pointer";
    button.style.transition = "background-color 0.3s";
    button.onmouseover = () => button.style.backgroundColor = "#3a3770";
    button.onmouseout = () => button.style.backgroundColor = "#2c2a5d";
    const list = document.createElement("ul");
    list.style.display = "none";
    list.style.margin = "8px 0 16px 20px";
    items.forEach(item => {
      const li = document.createElement("li");
      li.textContent = item;
      li.style.padding = "4px 0";
      list.appendChild(li);
    });
    button.addEventListener("click", () => {
      list.style.display = list.style.display === "none" ? "block" : "none";
    });
    container.appendChild(button);
    container.appendChild(list);
  });
</script>

<!-- Section 1 -->
<section id="section1" style="display: none;">
  <div style="display: flex; align-items: flex-start; gap: 24px; margin-top: 12px;">
    <img src="{{site.baseurl}}/images/mfa.jpg" alt="Multi-Factor-Authentication" style="width:50%; min-width:120px; border-radius: 12px;" title='This is an Multi-Factor-Authentication'/>
    <div>
      <strong>Protect Your Information</strong>
      <ul>
        <li>Use <strong>Multi-Factor Authentication (MFA)</strong></li>
        <li>Create <strong>strong, unique passwords</strong></li>
        <li>Keep your <strong>software updated</strong></li>
        <li><strong>Encrypt</strong> data and backups</li>
        <li>Secure your <strong>Wi-Fi and router</strong></li>
        <li>Use <strong>biometrics</strong> where possible</li>
      </ul>
    </div>
  </div>

  <!-- Question for Section 1 -->
  <div id="question1" style="margin-top: 24px;"></div>
</section>

<!-- Section 2 -->
<br>
<br>
<section id="section2" style="display: none;">
  <h3>Nighthawk Coders Accounts</h3>
  In this lesson, you'll create several accounts and provide a public-facing name and email for some of them.
  <div style="display: flex; align-items: flex-start; gap: 32px; margin-top: 16px;">
    <div>
      <h3><u style="color:green">Email Accounts</u></h3>
      Used for communication with your teacher and classmates.<br>
      Tip: Use different emails for junk, school, and important info.
      <h3><u style="color:green">Github Account</u></h3>
      Create a public-facing account for coding.<br>
      Use a junk/common email, not your school email.
      <h3><u style="color:green">GitHub Pages</u></h3>
      Build a public portfolio site.<br>
      It will be Google-indexed and viewable by anyone.
      <h3><u style="color:green">Slack Account</u></h3>
      Class-only communication tool.<br>
      Use a junk/common email. PII is limited to classmates and teacher.
      <h3><u style="color:green">Portfolio 2026 Account</u></h3>
      Tied to your GitHub ID.<br>
      Used for course tools, services, and analytics.
    </div>
    <img src="{{site.baseurl}}/images/12we.png" alt="Account Types" style="width:600px; border-radius: 12px;"/>
  </div>
  <p><strong>PII Strategy on Account Creation:</strong><br>
    It is in your interest to establish and continually refine your PII strategy. As you progress in the digital world, adapt what you're comfortable sharing.</p>

  <!-- Question for Section 2 -->
  <div id="question2" style="margin-top: 24px;"></div>
</section>

<!-- Section 3 -->
<section id="section3" style="display: none;">
  <h3>Key Points to Consider:</h3>
  <ol>
    <li><strong>Categorize Information:</strong>
      <ul>
        <li><strong>Public Information:</strong> Information you are comfortable sharing publicly, such as your name and general interests.</li>
        <li><strong>Sensitive Information:</strong> Information that should be shared cautiously, such as your full birth date and phone number.</li>
        <li><strong>Highly Confidential Information:</strong> Information that should be kept strictly private, like social security number and internet access credentials.</li>
      </ul>
      <br>
      <img src="{{site.baseurl}}/images/confidential.jpeg" alt="Multi-Factor-Authentication" style="width:40%; min-width:120px; border-radius: 12px;"/>
    </li>
    <li><strong>Use Different Email Accounts:</strong> Maintain different email accounts for different purposes (e.g., junk email, common email, work/school email, important email).</li>
    <li><strong>Be Prepared for Security Incidents:</strong> Anticipate that you may be hacked and will need to secure any vulnerabilities.</li>
    <li><strong>Adapt and Evolve:</strong> Reassess your PII strategy regularly.</li>
  </ol>

  <!-- Question for Section 3 -->
  <div id="question3" style="margin-top: 24px;"></div>
</section>

<!-- Final Parting Advice -->
<section id="partingAdvice" style="display: none;">
  <h3>✅ Parting Advice:</h3>
  <p>Be cautious with the information you share online. Protect your personal data by using separate email accounts, staying aware of security risks, and adapting your practices as the digital world evolves. Taking steps now helps safeguard your digital identity in the future.</p>
</section>

<script>
  function unlockSection(sectionId, questionDivId, questionText, keywords, feedbackHTML) {
    const section = document.getElementById(sectionId);
    const questionDiv = document.getElementById(questionDivId);

    if (!section || !questionDiv) return;

    const wrapper = document.createElement("div");
    wrapper.style.margin = "24px 0";
    wrapper.style.padding = "16px";
    wrapper.style.border = "1px solid #ccc";
    wrapper.style.borderRadius = "10px";
    wrapper.style.backgroundColor = "#f6f8fa";

    const q = document.createElement("p");
    q.innerHTML = `<strong>Question:</strong> ${questionText}`;

    const textarea = document.createElement("textarea");
    textarea.rows = 4;
    textarea.style.width = "100%";
    textarea.style.margin = "8px 0";

    const btn = document.createElement("button");
    btn.textContent = "Submit Answer";
    btn.style.marginBottom = "10px";
    btn.style.padding = "6px 14px";
    btn.style.borderRadius = "6px";
    btn.style.border = "none";
    btn.style.backgroundColor = "#2c2a5d";
    btn.style.color = "white";
    btn.style.cursor = "pointer";

    const content = document.createElement("div");
    content.innerHTML = feedbackHTML;
    content.style.display = "none";
    content.style.marginTop = "16px";

    const continueBtn = document.createElement("button");
    continueBtn.textContent = "Continue";
    continueBtn.style.display = "none";
    continueBtn.style.marginTop = "16px";
    continueBtn.style.padding = "6px 14px";
    continueBtn.style.borderRadius = "6px";
    continueBtn.style.border = "none";
    continueBtn.style.backgroundColor = "green";
    continueBtn.style.color = "white";
    continueBtn.style.cursor = "pointer";

    continueBtn.onclick = () => {
      section.style.display = "none";
      if (sectionId === "section1") document.getElementById("section2").style.display = "block";
      if (sectionId === "section2") document.getElementById("section3").style.display = "block";
      if (sectionId === "section3") document.getElementById("partingAdvice").style.display = "block";
    };

    btn.onclick = () => {
      const answer = textarea.value.toLowerCase();
      const passed = keywords.some(k => answer.includes(k));
      if (passed) {
        content.style.display = "block";
        btn.disabled = true;
        textarea.disabled = true;
        btn.textContent = "✅ Unlocked";
        btn.style.backgroundColor = "green";
        continueBtn.style.display = "inline-block";
      } else {
        alert("Try again. Think about key terms like 'security', 'privacy', or 'exposure'.");
      }
    };

    wrapper.appendChild(q);
    wrapper.appendChild(textarea);
    wrapper.appendChild(btn);
    wrapper.appendChild(content);
    wrapper.appendChild(continueBtn);
    questionDiv.appendChild(wrapper);
  }

  document.addEventListener("DOMContentLoaded", () => {
    // Show first section
    document.getElementById("section1").style.display = "block";

    unlockSection(
      "section1",
      "question1",
      "Why should we avoid using the same email for school, coding, and junk accounts?",
      ["security", "privacy", "organization", "spam"],
      `<p><strong>Great!</strong> Let’s look at different types of accounts you'll create in this course:</p>
       <ul>
         <li><strong>Email Accounts</strong>: Use different emails for school, GitHub, and junk to manage risk.</li>
         <li><strong>GitHub Account</strong>: Create a coding identity that reflects your work but protects your personal details.</li>
       </ul>`
    );

    unlockSection(
      "section2",
      "question2",
      "What risks might come from using your real name and birthdate on public accounts?",
      ["identity", "privacy", "stalking", "phishing"],
      `<p>Excellent point! Now let’s talk about how to manage <strong>public profiles</strong> responsibly:</p>
       <ul>
         <li>Use <em>general info</em> instead of full birthdates or addresses</li>
         <li>Link to work, not personal life</li>
       </ul>`
    );

    unlockSection(
      "section3",
      "question3",
      "Why is it helpful to understand what kind of PII you are sharing?",
      ["control", "exposure", "oversharing", "security"],
      `<p>Great awareness! Here’s a breakdown of <strong>PII categories</strong> again:</p>
       <ul>
         <li><strong>Public</strong>: School name, city, GitHub username</li>
         <li><strong>Sensitive</strong>: Phone number, address</li>
         <li><strong>Private</strong>: SSN, login credentials, MFA sources</li>
       </ul>`
    );
  });
</script>