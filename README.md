<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>EchoVault - Personal AI Diary</title>
  <style>
    :root {
      --primary-bg: #020F1D;
      --accent-blue: #0052CC;
      --text-white: #FFFFFF;
      --secondary-gray: #1B1E27;
      --font-inter: 'Inter', sans-serif;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: var(--font-inter);
      background-color: var(--primary-bg);
      color: var(--text-white);
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 20px;
    }

    h1 {
      color: var(--accent-blue);
      text-align: center;
      margin-bottom: 20px;
    }

    input, button, textarea {
      font-size: 16px;
      padding: 10px;
      border-radius: 4px;
      border: none;
      margin-bottom: 15px;
    }

    input, textarea {
      width: 300px;
    }

    button {
      background-color: var(--accent-blue);
      color: white;
      cursor: pointer;
    }

    button:hover {
      background-color: #003366;
    }

    .entry-list {
      margin-top: 20px;
      width: 100%;
      max-width: 500px;
    }

    .entry-card {
      background-color: var(--secondary-gray);
      padding: 15px;
      margin-bottom: 10px;
      border-radius: 8px;
    }

    .entry-date {
      font-size: 12px;
      color: #bbb;
    }

    .mood-tag {
      background-color: #ff6347;
      color: white;
      padding: 5px 10px;
      border-radius: 4px;
      margin-left: 10px;
    }
  </style>
</head>
<body>

  <h1>EchoVault - Personal AI Diary</h1>
  
  <!-- Daily Entry Form -->
  <textarea id="entryText" placeholder="Write your thoughts..."></textarea>
  <div>
    <input type="text" id="moodTag" placeholder="Mood Tag (e.g., Happy, Sad)" />
    <button id="saveEntryBtn">Save Entry</button>
  </div>

  <!-- Time Capsule -->
  <h2>Time Capsule</h2>
  <textarea id="timeCapsuleText" placeholder="Write a message for the future..."></textarea>
  <input type="number" id="timeCapsuleDays" placeholder="Number of days (e.g., 30)" />
  <button id="saveTimeCapsuleBtn">Save Time Capsule</button>

  <!-- Past Entries -->
  <div class="entry-list" id="entryList"></div>

  <script>
    // Save Entry to LocalStorage
    const saveEntryBtn = document.getElementById('saveEntryBtn');
    const saveTimeCapsuleBtn = document.getElementById('saveTimeCapsuleBtn');
    const entryText = document.getElementById('entryText');
    const moodTag = document.getElementById('moodTag');
    const timeCapsuleText = document.getElementById('timeCapsuleText');
    const timeCapsuleDays = document.getElementById('timeCapsuleDays');
    const entryList = document.getElementById('entryList');

    // Load previous entries and time capsules from localStorage
    function loadEntries() {
      const entries = JSON.parse(localStorage.getItem('entries')) || [];
      entryList.innerHTML = '';
      entries.forEach(entry => {
        const entryDiv = document.createElement('div');
        entryDiv.classList.add('entry-card');
        entryDiv.innerHTML = `
          <p><strong>Entry:</strong> ${entry.text}</p>
          <p class="entry-date">${new Date(entry.date).toLocaleString()}</p>
          <p class="mood-tag">${entry.mood}</p>
        `;
        entryList.appendChild(entryDiv);
      });
    }

    // Handle saving new entry
    saveEntryBtn.addEventListener('click', () => {
      const entryTextValue = entryText.value.trim();
      const moodTagValue = moodTag.value.trim();

      if (entryTextValue && moodTagValue) {
        const entries = JSON.parse(localStorage.getItem('entries')) || [];
        entries.push({
          text: entryTextValue,
          mood: moodTagValue,
          date: new Date().toISOString()
        });
        localStorage.setItem('entries', JSON.stringify(entries));
        entryText.value = '';
        moodTag.value = '';
        loadEntries();
      } else {
        alert('Please fill in both the entry and mood.');
      }
    });

    // Handle saving time capsule
    saveTimeCapsuleBtn.addEventListener('click', () => {
      const timeCapsuleTextValue = timeCapsuleText.value.trim();
      const timeCapsuleDaysValue = parseInt(timeCapsuleDays.value, 10);

      if (timeCapsuleTextValue && timeCapsuleDaysValue > 0) {
        const timeCapsules = JSON.parse(localStorage.getItem('timeCapsules')) || [];
        const futureDate = new Date();
        futureDate.setDate(futureDate.getDate() + timeCapsuleDaysValue);

        timeCapsules.push({
          text: timeCapsuleTextValue,
          daysLater: timeCapsuleDaysValue,
          futureDate: futureDate.toISOString()
        });
        localStorage.setItem('timeCapsules', JSON.stringify(timeCapsules));
        timeCapsuleText.value = '';
        timeCapsuleDays.value = '';
        alert(`Your message will be unlocked in ${timeCapsuleDaysValue} days.`);
      } else {
        alert('Please fill in both the message and number of days.');
      }
    });

    // Initial load of entries and time capsules
    loadEntries();
  </script>

</body>
</html>