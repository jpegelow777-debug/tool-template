# tool-template[index.html](https://github.com/user-attachments/files/23814414/index.html)

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tool Template</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="tool-container">
        <h1 id="tool-name">Tool Name</h1>

        <form id="tool-form">
            <div id="inputs-container">
                <!-- Inputs will be dynamically injected here -->
            </div>
            <button type="submit" id="run-tool">Run Tool</button>
        </form>

        <div class="output-container">
            <h2>AI Output</h2>
            <div id="ai-output"></div>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
[style.css](https://github.com/user-attachments/files/23814416/style.css)
body {
    font-family: Arial, sans-serif;
    background-color: #f5f5f5;
    padding: 20px;
    display: flex;
    justify-content: center;
}

.tool-container {
    background-color: #ffffff;
    padding: 20px;
    border-radius: 10px;
    max-width: 600px;
    width: 100%;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

#inputs-container {
    margin-bottom: 20px;
}

input, select {
    width: 100%;
    padding: 8px;
    margin-bottom: 10px;
    border-radius: 5px;
    border: 1px solid #ccc;
}

button {
    padding: 10px 20px;
    background-color: #ff6b3b;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #e85a2a;
}

.output-container {
    margin-top: 20px;
    background-color: #f1f1f1;
    padding: 15px;
    border-radius: 5px;
}
[script.js](https://github.com/user-attachments/files/23814419/script.js)
// Example tool setup
const toolData = {
    toolName: "Fishing Lure Color Selector",
    aiPrompt: "You are an AI expert in fishing. Recommend lure colors based on user inputs.",
    inputs: [
        { name: "Fish Type", type: "dropdown", options: ["Bass", "Trout", "Pike"] },
        { name: "Water Type", type: "dropdown", options: ["Freshwater", "Saltwater"] },
        { name: "Weather", type: "text", placeholder: "e.g., sunny, cloudy" }
    ]
};

// Populate tool name
document.getElementById("tool-name").innerText = toolData.toolName;

// Dynamically create inputs
const inputsContainer = document.getElementById("inputs-container");

toolData.inputs.forEach((input, index) => {
    let inputElement;
    if (input.type === "text") {
        inputElement = document.createElement("input");
        inputElement.type = "text";
        inputElement.placeholder = input.placeholder || "";
    } else if (input.type === "dropdown") {
        inputElement = document.createElement("select");
        input.options.forEach(opt => {
            const option = document.createElement("option");
            option.value = opt;
            option.innerText = opt;
            inputElement.appendChild(option);
        });
    }
    inputElement.id = `input-${index}`;
    inputsContainer.appendChild(inputElement);
});

// Handle form submission
document.getElementById("tool-form").addEventListener("submit", async function(e) {
    e.preventDefault();

    const inputValues = {};
    toolData.inputs.forEach((input, index) => {
        const value = document.getElementById(`input-${index}`).value;
        inputValues[input.name] = value;
    });

    // Prepare AI prompt dynamically
    const finalPrompt = `${toolData.aiPrompt}\nUser Inputs: ${JSON.stringify(inputValues)}`;

    // For now, just display the prompt in the output
    document.getElementById("ai-output").innerText = finalPrompt;

    // TODO: Add API call to OpenAI here
});
