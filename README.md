<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>قائمة المهام</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f3f4f6;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .app-container {
            background: #fff;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            width: 90%;
            max-width: 400px;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        input, select, button {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
        }
        button {
            background-color: #4caf50;
            color: white;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        ul {
            list-style: none;
            padding: 0;
        }
        li {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin-bottom: 10px;
        }
        .completed {
            text-decoration: line-through;
            color: #aaa;
        }
        .category {
            color: #007bff;
            font-size: 14px;
        }
        .actions button {
            margin-left: 5px;
        }
    </style>
</head>
<body>
    <div class="app-container">
        <h1>قائمة المهام</h1>
        <input id="taskInput" type="text" placeholder="أدخل المهمة...">
        <select id="categoryInput">
            <option value="شخصية">شخصية</option>
            <option value="مدرسية">مدرسية</option>
            <option value="صحية">صحية</option>
        </select>
        <button onclick="addTask()">إضافة المهمة</button>
        <ul id="taskList"></ul>
        <h2>إضافة نوع جديد</h2>
        <input id="newCategoryInput" type="text" placeholder="أدخل نوع المهمة الجديد...">
        <button onclick="addCategory()">إضافة النوع</button>
    </div>
    <script>
        function addTask() {
            const taskInput = document.getElementById("taskInput");
            const categoryInput = document.getElementById("categoryInput");
            const taskList = document.getElementById("taskList");

            if (taskInput.value.trim() === "") {
                alert("يرجى إدخال اسم المهمة!");
                return;
            }

            const li = document.createElement("li");
            li.innerHTML = `
                <span>${taskInput.value}</span>
                <span class="category">(${categoryInput.value})</span>
                <div class="actions">
                    <button onclick="completeTask(this)">تمت</button>
                    <button onclick="deleteTask(this)">حذف</button>
                </div>
            `;
            taskList.appendChild(li);

            taskInput.value = "";
            categoryInput.selectedIndex = 0;
        }

        function deleteTask(button) {
            const li = button.parentElement.parentElement;
            li.remove();
        }

        function completeTask(button) {
            const li = button.parentElement.parentElement;
            li.querySelector("span").classList.add("completed");
        }

        function addCategory() {
            const newCategoryInput = document.getElementById("newCategoryInput");
            const categoryInput = document.getElementById("categoryInput");

            if (newCategoryInput.value.trim() === "") {
                alert("يرجى إدخال اسم النوع الجديد!");
                return;
            }

            const newOption = document.createElement("option");
            newOption.value = newCategoryInput.value;
            newOption.textContent = newCategoryInput.value;
            categoryInput.appendChild(newOption);

            newCategoryInput.value = "";
            alert("تمت إضافة النوع الجديد!");
        }
    </script>
</body>
</html>
