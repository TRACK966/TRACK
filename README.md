<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>TRACK.966</title>
    <style>
        body { background: #000; color: #fff; font-family: sans-serif; text-align: center; padding: 20px; }
        .gallery { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 15px; margin-top: 20px; }
        .gallery img { width: 100%; height: 200px; object-fit: cover; border-radius: 8px; }
        .admin-panel { background: #1a1a1a; padding: 20px; margin: 30px auto; max-width: 500px; border-radius: 10px; }
        input[type="file"] { margin: 10px 0; }
        button { background: #ff0000; color: #fff; padding: 10px 20px; border: none; cursor: pointer; border-radius: 5px; }
    </style>
</head>
<body>

    <h1>TRACK.966</h1>
    <p>معرض الأعمال</p>

    <div class="admin-panel">
        <h3>لوحة التحكم (رفع الصور)</h3>
        <input type="file" id="imageLoader" accept="image/*">
        <button onclick="addImage()">إضافة للصورة للمعرض</button>
    </div>

    <div class="gallery" id="gallery"></div>

    <script>
        // دالة لإضافة الصورة وحفظها
        function addImage() {
            const input = document.getElementById('imageLoader');
            const file = input.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(e) {
                const imgData = e.target.result;
                // حفظ الصورة في ذاكرة المتصفح
                localStorage.setItem('img_' + Date.now(), imgData);
                renderGallery();
            };
            reader.readAsDataURL(file);
        }

        // دالة لعرض الصور
        function renderGallery() {
            const gallery = document.getElementById('gallery');
            gallery.innerHTML = '';
            for (let i = 0; i < localStorage.length; i++) {
                const key = localStorage.key(i);
                if (key.startsWith('img_')) {
                    const img = document.createElement('img');
                    img.src = localStorage.getItem(key);
                    gallery.appendChild(img);
                }
            }
        }
        renderGallery();
    </script>
</body>
</html>
