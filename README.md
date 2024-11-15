# todolistaryansh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Enhanced Todo App</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            transition: background-color 0.3s, color 0.3s;
        }
        .light-mode {
            background-color: #f5f5f5;
            color: #333;
        }
        .dark-mode {
            background-color: #333;
            color: #f5f5f5;
        }
        .container {
            background-color: white;
            padding: 2rem;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 400px;
            transition: background-color 0.3s, color 0.3s;
        }
        .dark-mode .container {
            background-color: #444;
            color: #f5f5f5;
        }
        h1 {
            text-align: center;
            margin-bottom: 1.5rem;
        }
        input, button {
            width: 100%;
            padding: 0.5rem;
            margin-bottom: 1rem;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        button {
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .add-btn {
            background-color: #4CAF50;
            color: white;
            border: none;
        }
        .add-btn:hover {
            background-color: #45a049;
        }
        .clear-btn, .toggle-dark-mode {
            background-color: #333;
            color: white;
        }
        .clear-btn:hover, .toggle-dark-mode:hover {
            background-color: #555;
        }
        .todo-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0.5rem;
            border-bottom: 1px solid #eee;
        }
        .todo-item:last-child {
            border-bottom: none;
        }
        .todo-item button {
            width: auto;
            padding: 0.25rem 0.5rem;
            margin-left: 0.5rem;
        }
        .completed {
            text-decoration: line-through;
            color: #888;
        }
    </style>
</head>
<body class="light-mode">
    <div class="container">
        <h1>Enhanced Todo App</h1>
        <input type="text" id="todo_title" placeholder="Enter todo title">
        <input type="text" id="todo_desc" placeholder="Enter todo description">
        <button class="add-btn" onclick="performOperation()">Add Todo</button>
        <button class="clear-btn" onclick="clearTodos()">Clear All Todos</button>
        <button class="toggle-dark-mode" onclick="toggleDarkMode()">Toggle Dark Mode</button>
        <div id="todo_display"></div>
    </div>

    <script>
        const titleInput = document.getElementById("todo_title");
        const descInput = document.getElementById("todo_desc");
        const todoDisplay = document.getElementById("todo_display");
        const todos = [];

        function performOperation() {
            const newTodo = {
                title: titleInput.value,
                desc: descInput.value,
                completion: false
            };
            todos.push(newTodo);
            updateTodoDisplay();
            titleInput.value = "";
            descInput.value = "";
        }

        function updateTodoDisplay() {
            todoDisplay.innerHTML = "";
            todos.forEach(function(element, index) {
                const todoItem = document.createElement("div");
                todoItem.className = "todo-item";
                todoItem.innerHTML = `
                    <span class="${element.completion ? 'completed' : ''}">
                        ${element.title}: ${element.desc}
                    </span>
                    <button onclick="toggleCompletion(${index})">
                        ${element.completion ? 'Completed' : 'Incomplete'}
                    </button>
                    <button onclick="deleteTodoItem(${index})">Delete</button>
                `;
                todoDisplay.appendChild(todoItem);
            });
        }

        function toggleCompletion(index) {
            todos[index].completion = !todos[index].completion;
            updateTodoDisplay();
        }

        function deleteTodoItem(index) {
            todos.splice(index, 1);
            updateTodoDisplay();
        }

        function clearTodos() {
            todos.length = 0;
            updateTodoDisplay();
        }

        function toggleDarkMode() {
            document.body.classList.toggle("dark-mode");
            document.body.classList.toggle("light-mode");
        }
    </script>
</body>
</html>
