# Ex03 To-Do List using JavaScript
## Date: 10/08/2026

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM
### index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>TaskFlow - To-Do List</title>

    <link rel="stylesheet" href="style.css">
</head>

<body>

    <div class="app">

        <!-- Header -->
        <header>
            <div>
                <h1>Task<span>Flow</span> ✨</h1>
                <p>Organize your day. Get things done.</p>
            </div>

            <button id="themeBtn" class="theme-btn">🌙</button>
        </header>

        <!-- Statistics -->
        <section class="stats">

            <div class="stat-card">
                <div class="stat-icon">📋</div>
                <div>
                    <h3 id="totalTasks">0</h3>
                    <p>Total Tasks</p>
                </div>
            </div>

            <div class="stat-card">
                <div class="stat-icon">⏳</div>
                <div>
                    <h3 id="pendingTasks">0</h3>
                    <p>Pending</p>
                </div>
            </div>

            <div class="stat-card">
                <div class="stat-icon">✅</div>
                <div>
                    <h3 id="completedTasks">0</h3>
                    <p>Completed</p>
                </div>
            </div>

            <div class="stat-card">
                <div class="stat-icon">📊</div>
                <div>
                    <h3 id="progress">0%</h3>
                    <p>Progress</p>
                </div>
            </div>

        </section>

        <!-- Add Task -->
        <section class="task-form">

            <input
                type="text"
                id="taskInput"
                placeholder="What do you need to do?"
            >

            <select id="category">
                <option value="General">📌 General</option>
                <option value="Study">📚 Study</option>
                <option value="Work">💼 Work</option>
                <option value="Personal">🏠 Personal</option>
                <option value="Shopping">🛒 Shopping</option>
            </select>

            <select id="priority">
                <option value="Low">🟢 Low</option>
                <option value="Medium">🟡 Medium</option>
                <option value="High">🔴 High</option>
            </select>

            <input type="date" id="dueDate">

            <button onclick="addTask()" class="add-btn">
                + Add Task
            </button>

        </section>

        <!-- Search -->
        <section class="search-box">

            <input
                type="text"
                id="searchInput"
                placeholder="🔍 Search tasks..."
                oninput="displayTasks()"
            >

            <select id="filter" onchange="displayTasks()">
                <option value="all">All Tasks</option>
                <option value="pending">Pending</option>
                <option value="completed">Completed</option>
                <option value="high">High Priority</option>
            </select>

            <select id="sort" onchange="displayTasks()">
                <option value="newest">Newest</option>
                <option value="oldest">Oldest</option>
                <option value="priority">Priority</option>
            </select>

        </section>

        <!-- Progress -->
        <section class="progress-container">

            <div class="progress-info">
                <span>Today's Progress</span>
                <span id="progressText">0%</span>
            </div>

            <div class="progress-bar">
                <div id="progressBar"></div>
            </div>

        </section>

        <!-- Tasks -->
        <section>

            <div class="section-title">
                <h2>My Tasks</h2>

                <button onclick="deleteCompleted()" class="clear-btn">
                    Clear Completed
                </button>
            </div>

            <div id="taskList"></div>

            <div id="emptyMessage" class="empty">
                <div>📝</div>
                <h3>No tasks found</h3>
                <p>Add a task and start being productive!</p>
            </div>

        </section>

        <footer>
            <p>TaskFlow © 2026 | Built with HTML, CSS & JavaScript</p>
        </footer>

    </div>

    <script src="script.js"></script>

</body>
</html>
```
### style.css
```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

:root {
    --primary: #6c63ff;
    --secondary: #8f87ff;
    --background: #f4f6fb;
    --card: #ffffff;
    --text: #222;
    --muted: #777;
    --border: #e5e5e5;
}

body {
    font-family: Arial, sans-serif;
    background: var(--background);
    color: var(--text);
    min-height: 100vh;
}

body.dark {
    --background: #15151d;
    --card: #20202b;
    --text: #ffffff;
    --muted: #aaa;
    --border: #383846;
}

.app {
    width: 92%;
    max-width: 1200px;
    margin: auto;
    padding: 35px 0;
}

/* Header */

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 30px;
}

header h1 {
    font-size: 38px;
}

header h1 span {
    color: var(--primary);
}

header p {
    color: var(--muted);
    margin-top: 6px;
}

.theme-btn {
    width: 45px;
    height: 45px;
    border: none;
    border-radius: 50%;
    background: var(--card);
    box-shadow: 0 4px 15px rgba(0,0,0,0.08);
    cursor: pointer;
    font-size: 20px;
}

/* Statistics */

.stats {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 18px;
    margin-bottom: 25px;
}

.stat-card {
    background: var(--card);
    padding: 20px;
    border-radius: 15px;
    display: flex;
    align-items: center;
    gap: 15px;
    box-shadow: 0 5px 20px rgba(0,0,0,0.05);
}

.stat-icon {
    font-size: 28px;
}

.stat-card h3 {
    font-size: 25px;
}

.stat-card p {
    color: var(--muted);
    font-size: 14px;
}

/* Task Form */

.task-form {
    background: var(--card);
    padding: 20px;
    border-radius: 15px;
    display: grid;
    grid-template-columns: 2fr 1fr 1fr 1fr auto;
    gap: 10px;
    box-shadow: 0 5px 20px rgba(0,0,0,0.05);
    margin-bottom: 20px;
}

input,
select {
    padding: 13px;
    border: 1px solid var(--border);
    border-radius: 8px;
    background: var(--card);
    color: var(--text);
    outline: none;
}

input:focus,
select:focus {
    border-color: var(--primary);
}

.add-btn {
    border: none;
    background: var(--primary);
    color: white;
    padding: 13px 20px;
    border-radius: 8px;
    cursor: pointer;
    font-weight: bold;
}

.add-btn:hover {
    background: var(--secondary);
}

/* Search */

.search-box {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
}

.search-box input {
    flex: 1;
}

/* Progress */

.progress-container {
    background: var(--card);
    padding: 20px;
    border-radius: 15px;
    margin-bottom: 25px;
}

.progress-info {
    display: flex;
    justify-content: space-between;
    margin-bottom: 10px;
    font-weight: bold;
}

.progress-bar {
    height: 10px;
    background: #ddd;
    border-radius: 10px;
    overflow: hidden;
}

#progressBar {
    height: 100%;
    width: 0%;
    background: var(--primary);
    border-radius: 10px;
    transition: 0.4s;
}

/* Section */

.section-title {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 15px;
}

.clear-btn {
    border: none;
    background: transparent;
    color: #e74c3c;
    cursor: pointer;
}

/* Task */

.task {
    background: var(--card);
    padding: 18px;
    margin-bottom: 12px;
    border-radius: 12px;
    display: flex;
    align-items: center;
    gap: 15px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.04);
    border-left: 5px solid var(--primary);
}

.task.completed {
    opacity: 0.65;
}

.check {
    width: 22px;
    height: 22px;
    cursor: pointer;
}

.task-content {
    flex: 1;
}

.task-title {
    font-size: 17px;
    font-weight: bold;
}

.task.completed .task-title {
    text-decoration: line-through;
}

.task-info {
    display: flex;
    gap: 8px;
    margin-top: 7px;
    flex-wrap: wrap;
}

.badge {
    padding: 4px 9px;
    border-radius: 20px;
    font-size: 12px;
    background: #eee;
}

.high {
    background: #ffe0e0;
    color: #d63031;
}

.medium {
    background: #fff3cd;
    color: #856404;
}

.low {
    background: #dff7e7;
    color: #218c4c;
}

.task-actions {
    display: flex;
    gap: 6px;
}

.action-btn {
    border: none;
    padding: 8px 10px;
    border-radius: 7px;
    cursor: pointer;
}

.edit {
    background: #eee;
}

.delete {
    background: #ffe0e0;
    color: #d63031;
}

/* Empty */

.empty {
    text-align: center;
    padding: 60px 20px;
    color: var(--muted);
}

.empty div {
    font-size: 50px;
    margin-bottom: 10px;
}

.empty h3 {
    color: var(--text);
    margin-bottom: 5px;
}

/* Footer */

footer {
    text-align: center;
    color: var(--muted);
    margin-top: 40px;
    padding: 20px;
}

/* Responsive */

@media (max-width: 900px) {

    .stats {
        grid-template-columns: repeat(2, 1fr);
    }

    .task-form {
        grid-template-columns: 1fr 1fr;
    }

    .add-btn {
        grid-column: span 2;
    }
}

@media (max-width: 600px) {

    .app {
        width: 94%;
        padding: 20px 0;
    }

    header h1 {
        font-size: 30px;
    }

    .stats {
        grid-template-columns: 1fr 1fr;
    }

    .task-form {
        grid-template-columns: 1fr;
    }

    .add-btn {
        grid-column: auto;
    }

    .search-box {
        flex-direction: column;
    }

    .task {
        align-items: flex-start;
    }

    .task-actions {
        flex-direction: column;
    }
}
```
### script.js
```js
let tasks = JSON.parse(localStorage.getItem("tasks")) || [];


// Add Task
function addTask() {

    const input = document.getElementById("taskInput");
    const category = document.getElementById("category").value;
    const priority = document.getElementById("priority").value;
    const dueDate = document.getElementById("dueDate").value;

    const title = input.value.trim();

    if (title === "") {
        alert("Please enter a task!");
        return;
    }

    const task = {
        id: Date.now(),
        title: title,
        category: category,
        priority: priority,
        dueDate: dueDate,
        completed: false
    };

    tasks.push(task);

    saveTasks();

    input.value = "";
    document.getElementById("dueDate").value = "";

    displayTasks();
}


// Display Tasks
function displayTasks() {

    const list = document.getElementById("taskList");
    const empty = document.getElementById("emptyMessage");

    const search =
        document.getElementById("searchInput").value.toLowerCase();

    const filter =
        document.getElementById("filter").value;

    const sort =
        document.getElementById("sort").value;

    let filteredTasks = tasks.filter(task => {

        const matchesSearch =
            task.title.toLowerCase().includes(search);

        if (!matchesSearch) return false;

        if (filter === "pending")
            return !task.completed;

        if (filter === "completed")
            return task.completed;

        if (filter === "high")
            return task.priority === "High";

        return true;
    });


    // Sorting

    if (sort === "newest") {
        filteredTasks.sort((a, b) => b.id - a.id);
    }

    if (sort === "oldest") {
        filteredTasks.sort((a, b) => a.id - b.id);
    }

    if (sort === "priority") {

        const priorityValue = {
            "High": 3,
            "Medium": 2,
            "Low": 1
        };

        filteredTasks.sort(
            (a, b) =>
                priorityValue[b.priority] -
                priorityValue[a.priority]
        );
    }


    list.innerHTML = "";

    if (filteredTasks.length === 0) {
        empty.style.display = "block";
    } else {
        empty.style.display = "none";
    }


    filteredTasks.forEach(task => {

        const div = document.createElement("div");

        div.className =
            "task " +
            (task.completed ? "completed" : "");

        let dateText = task.dueDate
            ? `📅 ${task.dueDate}`
            : "📅 No deadline";

        div.innerHTML = `

            <input
                type="checkbox"
                class="check"
                ${task.completed ? "checked" : ""}
                onchange="toggleTask(${task.id})"
            >

            <div class="task-content">

                <div class="task-title">
                    ${task.title}
                </div>

                <div class="task-info">

                    <span class="badge">
                        ${task.category}
                    </span>

                    <span class="badge ${task.priority.toLowerCase()}">
                        ${task.priority}
                    </span>

                    <span class="badge">
                        ${dateText}
                    </span>

                </div>

            </div>

            <div class="task-actions">

                <button
                    class="action-btn edit"
                    onclick="editTask(${task.id})">
                    ✏️
                </button>

                <button
                    class="action-btn delete"
                    onclick="deleteTask(${task.id})">
                    🗑️
                </button>

            </div>
        `;

        list.appendChild(div);
    });

    updateStats();
}


// Complete Task

function toggleTask(id) {

    const task = tasks.find(task => task.id === id);

    if (task) {
        task.completed = !task.completed;
    }

    saveTasks();
    displayTasks();
}


// Delete Task

function deleteTask(id) {

    if (!confirm("Delete this task?")) {
        return;
    }

    tasks = tasks.filter(task => task.id !== id);

    saveTasks();
    displayTasks();
}


// Edit Task

function editTask(id) {

    const task = tasks.find(task => task.id === id);

    if (!task) return;

    const newTitle =
        prompt("Edit your task:", task.title);

    if (newTitle === null) return;

    if (newTitle.trim() === "") {
        alert("Task cannot be empty!");
        return;
    }

    task.title = newTitle.trim();

    saveTasks();
    displayTasks();
}


// Clear Completed

function deleteCompleted() {

    tasks = tasks.filter(task => !task.completed);

    saveTasks();
    displayTasks();
}


// Statistics

function updateStats() {

    const total = tasks.length;

    const completed =
        tasks.filter(task => task.completed).length;

    const pending =
        total - completed;

    const percentage =
        total === 0
            ? 0
            : Math.round((completed / total) * 100);

    document.getElementById("totalTasks").textContent = total;

    document.getElementById("pendingTasks").textContent = pending;

    document.getElementById("completedTasks").textContent = completed;

    document.getElementById("progress").textContent =
        percentage + "%";

    document.getElementById("progressText").textContent =
        percentage + "%";

    document.getElementById("progressBar").style.width =
        percentage + "%";
}


// Local Storage

function saveTasks() {

    localStorage.setItem(
        "tasks",
        JSON.stringify(tasks)
    );
}


// Dark Mode

document.getElementById("themeBtn").onclick = function () {

    document.body.classList.toggle("dark");

    if (document.body.classList.contains("dark")) {
        this.textContent = "☀️";
        localStorage.setItem("theme", "dark");
    } else {
        this.textContent = "🌙";
        localStorage.setItem("theme", "light");
    }
};


// Load Theme

if (localStorage.getItem("theme") === "dark") {

    document.body.classList.add("dark");

    document.getElementById("themeBtn").textContent = "☀️";
}


// Initial Display

displayTasks();
```

## OUTPUT
<img width="1627" height="867" alt="image" src="https://github.com/user-attachments/assets/78d0b54e-3ae2-42b1-b5d5-eb4a95092b33" />


## RESULT
The program for creating To-do list using JavaScript is executed successfully.
