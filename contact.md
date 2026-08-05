---
layout: page
title: Contact Us
subtitle: Send a question or comment
---

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
