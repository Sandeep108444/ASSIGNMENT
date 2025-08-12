<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Student Registration Form</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    :root {
      --radius: 8px;
      --shadow: rgba(0,0,0,0.1) 0px 4px 12px;
      font-family: system-ui,-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,sans-serif;
    }
    * { box-sizing: border-box; }
    body {
      background: #f5f7fa;
      margin: 0;
      padding: 1.5rem;
      display: flex;
      justify-content: center;
    }
    .container {
      max-width: 520px;
      width: 100%;
      background: #fff;
      padding: 1.75rem 2rem;
      border-radius: var(--radius);
      box-shadow: var(--shadow);
    }
    h1 {
      margin-top: 0;
      font-size: 1.75rem;
      text-align: center;
    }
    form {
      display: grid;
      gap: 1rem;
    }
    .grid-2 {
      display: grid;
      grid-template-columns: repeat(auto-fit,minmax(120px,1fr));
      gap: 1rem;
    }
    label {
      display: block;
      font-size: 0.85rem;
      margin-bottom: 4px;
      font-weight: 600;
    }
    input, select {
      width: 100%;
      padding: 0.65rem 0.75rem;
      border: 1px solid #cfd8e4;
      border-radius: 6px;
      font-size: 1rem;
    }
    .small {
      font-size: 0.75rem;
      color: #555;
    }
    .inline {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      flex-wrap: wrap;
    }
    .error {
      color: #b00020;
      font-size: 0.75rem;
    }
    button {
      background: #4f46e5;
      color: #fff;
      border: none;
      padding: 0.85rem 1rem;
      font-size: 1rem;
      border-radius: 10px;
      cursor: pointer;
      width: 100%;
      font-weight: 600;
      box-shadow: rgba(79,70,229,0.35) 0px 8px 24px;
    }
    button:disabled {
      opacity: 0.6;
      cursor: not-allowed;
    }
    .checkbox {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      font-size: 0.9rem;
    }
    .note {
      font-size: 0.7rem;
      color: #666;
    }
  </style>
</head>
<body>
  <div class="container" aria-label="Student registration form container">
    <h1>Student Registration</h1>
    <form id="regForm" novalidate>
      <div class="grid-2">
        <div>
          <label for="firstName">First Name *</label>
          <input type="text" id="firstName" name="firstName" required minlength="2" maxlength="30" placeholder="John" aria-required="true" />
        </div>
        <div>
          <label for="lastName">Last Name *</label>
          <input type="text" id="lastName" name="lastName" required minlength="2" maxlength="30" placeholder="Doe" />
        </div>
      </div>

      <div>
        <label for="email">Email *</label>
        <input type="email" id="email" name="email" required placeholder="student@example.com" />
      </div>

      <div>
        <label for="studentId">Student ID *</label>
        <input type="text" id="studentId" name="studentId" required pattern="^[A-Za-z0-9]{8}$" placeholder="8 alphanumeric chars" aria-describedby="studentIdHelp" />
        <div class="small" id="studentIdHelp">Format: exactly 8 letters/numbers (e.g., A1B2C3D4)</div>
      </div>

      <div class="grid-2">
        <div>
          <label for="password">Password *</label>
          <input type="password" id="password" name="password" required minlength="8" placeholder="At least 8 characters" aria-describedby="passwordHelp" />
          <div class="small" id="passwordHelp">Must be 8+ characters.</div>
        </div>
        <div>
          <label for="confirmPassword">Confirm Password *</label>
          <input type="password" id="confirmPassword" name="confirmPassword" required placeholder="Re-enter password" />
        </div>
      </div>

      <div class="grid-2">
        <div>
          <label for="dob">Date of Birth *</label>
          <input type="date" id="dob" name="dob" required aria-describedby="ageHelp" max="" />
          <div class="small" id="ageHelp">You must be at least 13 years old.</div>
        </div>
        <div>
          <label for="phone">Phone Number *</label>
          <input type="tel" id="phone" name="phone" required pattern="^\+?[0-9]{7,15}$" placeholder="+1234567890" />
        </div>
      </div>

      <div>
        <fieldset style="border:1px solid #cfd8e4; padding:0.75rem; border-radius:6px;">
          <legend style="font-weight:600;">Gender *</legend>
          <div class="inline">
            <label><input type="radio" name="gender" value="male" required /> Male</label>
            <label><input type="radio" name="gender" value="female" /> Female</label>
            <label><input type="radio" name="gender" value="other" /> Other</label>
            <label><input type="radio" name="gender" value="prefer_not" /> Prefer not to say</label>
          </div>
        </fieldset>
      </div>

      <div>
        <label for="course">Course Enrolled *</label>
        <select id="course" name="course" required>
          <option value="">-- Select Course --</option>
          <option value="cs">Computer Science</option>
          <option value="eng">Engineering</option>
          <option value="bus">Business</option>
          <option value="art">Arts</option>
          <option value="sci">Sciences</option>
        </select>
      </div>

      <div class="checkbox">
        <input type="checkbox" id="terms" name="terms" required />
        <label for="terms">I agree to the <a href="#" target="_blank" rel="noopener">terms and conditions</a>. *</label>
      </div>

      <div id="formError" class="error" aria-live="polite" style="display:none;"></div>

      <button type="submit" id="submitBtn">Register</button>
    </form>
    <div class="note">Fields marked with * are required. The browser will highlight invalid inputs automatically.</div>
  </div>

  <script>
    // Set max date for DOB so that user is at least 13 years old
    (function(){
      const dobInput = document.getElementById('dob');
      const today = new Date();
      const minAge = 13;
      const cutoff = new Date(today.getFullYear() - minAge, today.getMonth(), today.getDate());
      dobInput.max = cutoff.toISOString().split('T')[0];
    })();

    const form = document.getElementById('regForm');
    const password = document.getElementById('password');
    const confirmPassword = document.getElementById('confirmPassword');
    const formError = document.getElementById('formError');

    function passwordsMatch() {
      return password.value === confirmPassword.value;
    }

    form.addEventListener('submit', function(e){
      formError.style.display = 'none';
      formError.textContent = '';

      // Let HTML5 do its built-in validation first
      if (!form.checkValidity()) {
        // will trigger browser UI
        return;
      }

      // Custom: password confirmation
      if (!passwordsMatch()) {
        e.preventDefault();
        formError.style.display = 'block';
        formError.textContent = 'Passwords do not match.';
        confirmPassword.focus();
        return;
      }

      // Age verification (redundant with max on date but double-check)
      const dobVal = document.getElementById('dob').value;
      if (dobVal) {
        const dobDate = new Date(dobVal);
        const today = new Date();
        const ageDifMs = today - dobDate;
        const ageDate = new Date(ageDifMs);
        const age = Math.abs(ageDate.getUTCFullYear() - 1970);
        if (age < 13) {
          e.preventDefault();
          formError.style.display = 'block';
          formError.textContent = 'You must be at least 13 years old to register.';
          document.getElementById('dob').focus();
          return;
        }
      }

      // All validations passed. In a real application, you'd submit to server here.
      e.preventDefault(); // prevent actual submission for demo
      alert('Registration successful! (This is a demo; no data was sent.)');
      form.reset();
    });

    // Real-time password match feedback
    confirmPassword.addEventListener('input', () => {
      if (password.value && confirmPassword.value && !passwordsMatch()) {
        confirmPassword.setCustomValidity('Passwords do not match');
      } else {
        confirmPassword.setCustomValidity('');
      }
    });
  </script>
</body>
</html>
