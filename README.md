<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>AI Content Generator</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        text-align: center;
        padding: 20px;
      }
      input,
      button {
        padding: 10px;
        margin: 10px;
        font-size: 16px;
      }
      #output {
        margin-top: 20px;
        padding: 15px;
        border: 1px solid #ddd;
        display: inline-block;
        max-width: 400px;
      }
    </style>
  </head>
  <body>
    <h1>AI Content Generator</h1>
    <input
      type="text"
      id="userInput"
      placeholder="Enter your instructions..."
    />
    <button onclick="generateContent()">Generate</button>

    <div id="output"></div>

    <script>
      async function generateContent() {
        const input = document.getElementById("userInput").value;
        if (!input) return alert("Please enter instructions.");

        document.getElementById("output").innerText = "Generating...";

        try {
          const response = await fetch(
            "https://api.openai.com/v1/completions",
            {
              method: "POST",

              headers: {
                "Content-Type": "application/json",
                Authorization: `Bearer 8oed3366e72ca42et0cf2f4b44f179e7`,
              },
              body: JSON.stringify({
                model: "gpt-3.5-turbo",
                prompt: input,
                max_tokens: 100,
              }),
            }
          );

          if (!response.ok) {
            throw new Error(
              `API error: ${response.status} ${response.statusText}`
            );
          }

          const data = await response.json();
          document.getElementById("output").innerText =
            data.choices[0].text.trim();
        } catch (error) {
          console.error("Error:", error);
          document.getElementById("output").innerText =
            "Error generating content.";
        }
      }
    </script>
  </body>
</html>
