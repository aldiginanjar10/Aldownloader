
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
