npm init -y
npm install express axios cors
const express = require("express");
const axios = require("axios");
const cors = require("cors");

const app = express();
app.use(cors());
app.use(express.json());

app.post("/download", async (req, res) => {
  const { url } = req.body;

  try {
    // Contoh pakai API pihak ketiga
    const response = await axios.get(
      `https://api.tiklydown.me/api/download?url=${url}`
    );

    res.json(response.data);
  } catch (error) {
    res.status(500).json({ error: "Gagal mengambil video" });
  }
});

app.listen(3000, () => {
  console.log("Server jalan di http://localhost:3000");
});<!DOCTYPE html>
<html>
<head>
  <title>TikTok Downloader</title>
</head>
<body>
  <h2>TikTok Downloader</h2>
  <input type="text" id="url" placeholder="Masukkan link TikTok">
  <button onclick="download()">Download</button>

  <div id="result"></div>

  <script>
    async function download() {
      const url = document.getElementById("url").value;

      const res = await fetch("http://localhost:3000/download", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({ url })
      });

      const data = await res.json();

      document.getElementById("result").innerHTML = `
        <a href="${data.video.noWatermark}" target="_blank">
          Download Tanpa Watermark
        </a>
      `;
    }
  </script>
</body>
</html>
