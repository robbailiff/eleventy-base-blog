---
layout: layouts/post.njk
title: Contact
templateClass: tmpl-post
eleventyNavigation:
  key: Contact
  order: 4
---

<form name="contact" method="POST" data-netlify="true">
  <div class="mb-3">
    <label class="form-label">Your Name: <input class="form-control" type="text" name="name" required /></label>   
  </div>
  <div class="mb-3">
    <label class="form-label">Your Email: <input class="form-control" type="email" name="email" required /></label>
  </div>
  <div class="mb-3 col-md-2">
    <select class="form-select" name="role[]" multiple>
    <option selected>Select Your Role</option>
    <option value="leader">Leader</option>
    <option value="follower">Follower</option>
  </select>
  </div>
  <div class="mb-3">
    <label class="form-label">Message: <textarea class="form-control" name="message"></textarea></label>
  </div>
  <div class="mb-3 form-check">
    <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" required>
    <label class="form-check-label" for="flexCheckDefault">
      I accept the Terms and Conditions
    </label>
  </div>
  <button type="submit" class="btn btn-primary" >Send</button>
</form>