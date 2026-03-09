# thomas-meals
Created with CodeSandbox
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Toddler Lunch Planner</title>
  <style>
    /* Minimal slate-based design */
    :root {
      --bg: #f8fafc;
      --card-bg: #ffffff;
      --border: #e2e8f0;
      --text: #1e293b;
      --text-muted: #64748b;
      --text-xs: #94a3b8;
      --main: #475569;
      --side: #0ea5e9;
      --fruit: #f43f5e;
      --snack: #f59e0b;
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      padding: 1.5rem;
      font-family: system-ui, -apple-system, sans-serif;
      background-color: var(--bg);
      color: var(--text);
      line-height: 1.5;
    }

    .container {
      max-width: 860px;
      margin: 0 auto;
      display: flex;
      flex-wrap: wrap;
      gap: 1.5rem;
    }

    .header {
      width: 100%;
      margin-bottom: 1.5rem;
    }
    .header label {
      font-size: 0.75rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.08rem;
      color: var(--text-xs);
    }
    .header h1 {
      font-size: 1.875rem;
      font-weight: 300;
      margin: 0;
      color: var(--text);
    }
    .header p {
      font-size: 0.875rem;
      color: var(--text-muted);
      margin-top: 0.5rem;
    }

    .weekdays {
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
      flex: 1 1 400px;
    }
    .card {
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 1rem;
      padding: 1.25rem;
      flex: 1;
      min-width: 240px;
      box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1);
      transition: box-shadow 0.2s ease;
    }
    .card:hover {
      box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1);
    }
    .card h3 {
      font-size: 0.875rem;
      font-weight: 600;
      margin: 0 0 1.5rem;
      color: var(--text);
    }

    .field {
      margin-bottom: 1rem;
    }
    .field label {
      display: flex;
      align-items: center;
      gap: 0.375rem;
      font-size: 0.625rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.1rem;
      color: var(--text-xs);
      margin-bottom: 0.375rem;
    }
    .dot {
      width: 0.375rem;
      height: 0.375rem;
      border-radius: 50%;
    }
    .dot.main  { background: var(--main); }
    .dot.side  { background: var(--side); }
    .dot.fruit { background: var(--fruit); }
    .dot.snack { background: var(--snack); }

    select {
      width: 100%;
      padding: 0.625rem;
      border: 1px solid #cbd5e1;
      border-radius: 0.5rem;
      background: #f1f5f9;
      font-size: 0.875rem;
      color: var(--text);
      appearance: none;
    }
    select:focus {
      outline: none;
      border-color: var(--main);
      box-shadow: 0 0 0 3px rgba(71, 85, 105, 0.1);
    }

    .pantry {
      flex: 0 0 240px;
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 1rem;
      padding: 1.25rem;
      box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1);
      position: sticky;
      top: 1.5rem;
      align-self: flex-start;
    }
    .pantry label {
      font-size: 0.625rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.1rem;
      color: var(--text-xs);
      margin-bottom: 0.25rem;
    }
    .pantry h2 {
      font-size: 1.125rem;
      font-weight: 300;
      margin: 0.25rem 0 1.25rem 0;
      color: var(--text);
    }

    .cat {
      margin-bottom: 1.25rem;
    }
    .cat h3 {
      display: flex;
      align-items: center;
      gap: 0.375rem;
      font-size: 0.75rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.1rem;
      color: var(--text-muted);
      margin: 0 0 0.5rem 0;
    }

    .cat input {
      width: 100%;
      padding: 0.5rem;
      border: 1px solid #cbd5e1;
      border-radius: 0.375rem 0 0 0.375rem;
      background: #f1f5f9;
      font-size: 0.875rem;
    }
    .cat input:focus {
      outline: none;
      border-color: var(--main);
    }
    .cat button {
      padding: 0.5rem 0.75rem;
      border: none;
      border-radius: 0 0.375rem 0.375rem 0;
      background: var(--main);
      color: #fff;
      font-size: 0.75rem;
      font-weight: 600;
    }
    .cat button:hover {
      opacity: 0.9;
    }

    .cat ul {
      list-style: none;
      padding: 0;
      margin: 0;
      max-height: 9rem;
      overflow-y: auto;
    }
    .cat li {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0.375rem 0.5rem;
      border-radius: 0.375rem;
      font-size: 0.875rem;
      color: var(--text-muted);
      cursor: default;
    }
    .cat li:hover {
      background: #f8fafc;
    }
    .cat li .remove {
      opacity: 0.4;
      font-size: 0.875rem;
      cursor: pointer;
    }
    .cat li:hover .remove {
      opacity: 1;
    }

    .divider {
      border-bottom: 1px solid #e2e8f0;
      margin-top: 0.5rem;
    }
  </style>
</head>
<body>

  <div class="container">

    <div class="header">
      <label>Weekday Lunch Planner</label>
      <h1>Toddler Lunch Planner</h1>
      <p>Plan one lunch per weekday from your custom food lists.</p>
    </div>

    <div class="weekdays">
      <!-- Will be filled by JS -->
    </div>

    <div class="pantry">
      <label>Manage Lists</label>
      <h2>Pantry Inventory</h2>
      <div id="inventory-list">
        <!-- Will be filled by JS -->
      </div>
    </div>

  </div>

  <script>
    const days = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"];
    const categories = {
      Main:  { color: "var(--main)", list: ["Cheese Quesadilla", "Turkey Roll-up", "Mac & Cheese", "PB&J"] },
      Side:  { color: "var(--side)", list: ["Steamed Carrots", "Cucumber Slices", "Peas", "Sweet Potato Tots"] },
      Fruit: { color: "var(--fruit)", list: ["Apple Slices", "Banana", "Berries", "Mango Dices"] },
      Snack: { color: "var(--snack)", list: ["Goldfish Crackers", "Yogurt", "Pretzels", "Cheese Stick"] }
    };

    // Current plan for each day
    const plan = {};
    days.forEach(day => {
      plan[day] = { Main: "", Side: "", Fruit: "", Snack: "" };
    });

    // Render weekday cards
    const weekdaysEl = document.querySelector(".weekdays");
    days.forEach(day => {
      const card = document.createElement("div");
      card.classList.add("card");

      // Add space BEFORE the day (margin-top)
      card.innerHTML = `
        <h3 style="margin-top: 0.75rem; margin-bottom: 1.5rem;">${day}</h3>
      `;

      categoriesArray = Object.entries(categories);
      categoriesArray.forEach(([cat, cfg]) => {
        const row = document.createElement("div");
        row.classList.add("field");

        row.innerHTML = `
          <label>
            <span class="dot ${cat.toLowerCase()}"></span>
            ${cat}
          </label>
          <select data-day="${day}" data-cat="${cat}">
            <option value="">Select ${cat}…</option>
          </select>
        `;
        card.appendChild(row);

        const select = row.querySelector("select");
        cfg.list.forEach(item => {
          const opt = document.createElement("option");
          opt.value = item;
          opt.textContent = item;
          select.appendChild(opt);
        });
        select.value = plan[day][cat] || "";

        select.addEventListener("change", () => {
          plan[day][cat] = select.value;
        });
      });

      weekdaysEl.appendChild(card);
    });

    // Render the pantry (inventory lists)
    const invListEl = document.getElementById("inventory-list");

    categoriesArray.forEach(([cat, cfg]) => {
      const catEl = document.createElement("div");
      catEl.classList.add("cat");

      catEl.innerHTML = `
        <h3>
          <span class="dot ${cat.toLowerCase()}" style="background:${cfg.color}"></span>
          ${cat}
        </h3>
        <div class="input-group">
          <input type="text" placeholder="Add ${cat.toLowerCase()}…" />
          <button>Add</button>
        </div>
        <ul id="list-${cat.toLowerCase()}"></ul>
        <div class="divider"></div>
      `;
      invListEl.appendChild(catEl);

      const input = catEl.querySelector("input");
      const button = catEl.querySelector("button");
      const ul = catEl.querySelector("ul");

      function renderItems() {
        ul.innerHTML = "";
        cfg.list.forEach(item => {
          const li = document.createElement("li");
          li.innerHTML = `
            <span>${item}</span>
            <span class="remove">×</span>
          `;
          li.querySelector(".remove").addEventListener("click", () => {
            const idx = cfg.list.indexOf(item);
            if (idx !== -1) {
              cfg.list.splice(idx, 1);
              renderItems();

              // Clear this item from
