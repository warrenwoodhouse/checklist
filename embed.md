```
<!-- Autosave Checklist Template -->
<!-- Template Author: Warren Woodhouse -->
<!-- Template Documentation URL: warrenwoodhouse.blogspot.com/templates/autosavechecklist -->
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Autosave Checklist</title>
    <style>
        body {
            font-family: system-ui, -apple-system, sans-serif;
            background-color: #f4f4f9;
            color: #333;
            max-width: 500px;
            margin: 40px auto;
            padding: 20px;
        }
        
        .card {
            background: white;
            padding: 20px 30px;
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }

        h2 {
            margin-top: 0;
            border-bottom: 2px solid #eee;
            padding-bottom: 10px;
        }

        .checklist {
            list-style-type: none;
            padding: 0;
        }

        .checklist li {
            margin: 12px 0;
            font-size: 1.1em;
            display: flex;
            align-items: center;
        }

        input[type="checkbox"] {
            width: 20px;
            height: 20px;
            margin-right: 15px;
            cursor: pointer;
        }

        label {
            cursor: pointer;
            user-select: none;
            flex-grow: 1;
        }

        /* Strikethrough effect when checked */
        input[type="checkbox"]:checked + label {
            text-decoration: line-through;
            color: #888;
        }

        .status {
            font-size: 0.85em;
            color: #666;
            margin-top: 20px;
            text-align: right;
            font-style: italic;
        }
    </style>
</head>
<body>

    <div class="card">
        <h2>Daily Tasks</h2>
        
        <!-- Checklist items. Make sure every checkbox has a unique 'id' -->
        <ul class="checklist" id="myChecklist">
            <li>
                <input type="checkbox" id="task1"> 
                <label for="task1">Drink water</label>
            </li>
            <li>
                <input type="checkbox" id="task2"> 
                <label for="task2">Read for 30 minutes</label>
            </li>
            <li>
                <input type="checkbox" id="task3"> 
                <label for="task3">Exercise</label>
            </li>
            <li>
                <input type="checkbox" id="task4"> 
                <label for="task4">Review project notes</label>
            </li>
        </ul>

        <div class="status" id="saveStatus">All changes saved automatically.</div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const checkboxes = document.querySelectorAll('#myChecklist input[type="checkbox"]');
            const statusText = document.getElementById('saveStatus');

            // 1. Load saved state from localStorage when the page loads
            checkboxes.forEach(checkbox => {
                const savedState = localStorage.getItem('autosave_task_' + checkbox.id);
                
                // If we found a saved state of 'true', check the box
                if (savedState === 'true') {
                    checkbox.checked = true;
                }

                // 2. Add an event listener to save the state whenever a box is clicked
                checkbox.addEventListener('change', (event) => {
                    // Save to localStorage (Key: "autosave_task_[id]", Value: "true" or "false")
                    localStorage.setItem('autosave_task_' + event.target.id, event.target.checked);
                    
                    // Briefly flash a "Saved!" message for visual feedback
                    statusText.textContent = "Changes saved!";
                    setTimeout(() => {
                        statusText.textContent = "All changes saved automatically.";
                    }, 1500);
                });
            });
        });
    </script>
</body>
</html>
```
