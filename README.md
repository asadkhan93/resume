<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Base64 to PDF Converter</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background-color: #f4f4f9;
    }
    .container {
      text-align: center;
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }
    textarea {
      width: 100%;
      height: 150px;
      margin-bottom: 10px;
      border: 1px solid #ddd;
      border-radius: 5px;
      padding: 10px;
      font-size: 14px;
      resize: none;
    }
    button {
      padding: 10px 20px;
      background-color: #007bff;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
    }
    button:hover {
      background-color: #0056b3;
    }
    .hidden {
      display: none;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Base64 to PDF Converter</h1>
    <textarea id="base64Input" placeholder="Paste your Base64 string here..."></textarea>
    <br>
    <button onclick="convertToPDF()">Convert to PDF</button>
    <a id="downloadLink" class="hidden" href="#" download="output.pdf">Download PDF</a>
  </div>

  <script>
    function convertToPDF() {
      const base64Input = document.getElementById("base64Input").value;
      const downloadLink = document.getElementById("downloadLink");

      if (!base64Input.trim()) {
        alert("Please enter a Base64 string.");
        return;
      }

      try {
        // Decode the Base64 string and create a Blob
        const pdfData = atob(base64Input);
        const uint8Array = new Uint8Array(pdfData.length);

        for (let i = 0; i < pdfData.length; i++) {
          uint8Array[i] = pdfData.charCodeAt(i);
        }

        const pdfBlob = new Blob([uint8Array], { type: "application/pdf" });

        // Create a downloadable link
        const pdfURL = URL.createObjectURL(pdfBlob);
        downloadLink.href = pdfURL;
        downloadLink.classList.remove("hidden");
        downloadLink.click();
      } catch (error) {
        alert("Invalid Base64 string.");
        console.error(error);
      }
    }
  </script>
</body>
</html>
