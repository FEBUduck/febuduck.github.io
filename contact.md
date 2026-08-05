---
layout: page
title: Contact Us
subtitle: Send a question or comment
---
<style>
.contact-wrapper {
  max-width: 500px;
  margin: 2rem auto;
  padding: 2rem;
  background: #ffffff;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.08);
  font-family: system-ui, sans-serif;

  border-left: 6px solid #154734;
}

.contact-wrapper label {
  font-weight: 600;
  margin-bottom: 6px;
  display: block;
}

.contact-wrapper input,
.contact-wrapper textarea {
  width: 100%;
  padding: 12px;
  margin-bottom: 1rem;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 15px;
}

.contact-wrapper button {
  width: 100%;
  padding: 12px;
  background: #154734;  /*Ducks green */
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  cursor: pointer;
  font-weight: 600;
}

.contact-wrapper button:hover {
  background: #0f3528;
}
</style>

<div class="contact-wrapper">
<form action="https://formspree.io/f/mjybvgrl" method="POST">
  <label for="email">Your Email</label>
  <input
    type="email"
    id="email"
    name="email"
    placeholder="you@example.com"
    required
  />

  <label for="message">Your Message</label>
  <textarea
    id="message"
    name="message"
    placeholder="Tell us what's on your mind..."
    rows="6"
    required
  ></textarea>

  <button type="submit">Send Message</button>
  <input type="hidden" name="_redirect" value="https://febuducks.com/thanks">
</form>
</div>
