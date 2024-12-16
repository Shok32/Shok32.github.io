<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <title>Обои</title>
  <style>
      body {
          font-family: Arial, sans-serif;
          margin: 0;
          padding: 0;
          background-color: #121212;
          color: #ffffff;
          transition: background-color 0.3s, color 0.3s;
          overflow-x: hidden;
          user-select: none;
      }
      header {
          background-color: #1e1e1e;
          padding: 20px;
          text-align: center;
          box-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
          width: 100%;
          box-sizing: border-box;
      }
      h1 {
          margin: 0;
          font-size: 24px;
      }
      .container {
          max-width: 100%;
          margin: 20px auto;
          display: grid;
          grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
          gap: 10px;
          padding-bottom: 20px;
          justify-content: center;
          align-items: start;
      }
      .upload-form {
          max-width: 800px;
          margin: 20px auto;
          text-align: center;
      }
      .upload-form input[type="file"],
      .upload-form input[type="text"] {
          margin: 10px 0;
          background-color: #2a2a2a;
          color: #ffffff;
          border: 1px solid #444;
          border-radius: 4px;
          padding: 10px;
          width: calc(100% - 20px);
          box-sizing: border-box;
      }
      .upload-form button {
          background-color: #28a745;
          color: white;
          border: none;
          padding: 10px 20px;
          cursor: pointer;
          border-radius: 4px;
          transition: background-color 0.3s;
      }
      .upload-form button:hover {
          background-color: #218838;
      }
      .wallpaper {
          position: relative;
          background-color: #1e1e1e;
          border-radius: 8px;
          overflow: hidden;
          box-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
          transition: transform 0.3s;
          width: 100%;
          max-width: 120px;
          margin: auto;
      }
      .wallpaper img {
          width: 100%;
          height: auto;
          display: block;
          cursor: pointer;
      }
      .wallpaper button {
          background-color: #007bff;
          color: white;
          border: none;
          padding: 10px;
          cursor: pointer;
          width: 100%;
          border-radius: 0 0 8px 8px;
          transition: background-color 0.3s;
      }
      .wallpaper button:hover {
          background-color: #0056b3;
      }
      .delete-button {
          position: absolute;
          top: -0px;
          background-color: #ff6b6b;
          color: white;
          border: none;
          border-radius: 4px;
          width: 25px;
          height: 25px;
          cursor: pointer;
          display: flex;
          justify-content: center;
          align-items: center;
          font-size: 16px;
          box-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
          transition: background-color 0.3s;
      }
      .delete-button:hover {
          background-color: #ff4d4d;
      }
      footer {
          text-align: center;
          padding: 20px;
          box-shadow: 0 -2px 4px rgba(0, 0, 0, 0.5);
          position: relative;
          bottom: 0;
          width: 100%;
      }
      .theme-toggle {
          margin: 20px;
          cursor: pointer;
          padding: 10px;
          background-color: #444;
          color: white;
          border: none;
          border-radius: 4px;
      }
      .fade-out {
          animation: fadeOut 0.5s forwards;
      }
      @keyframes fadeOut {
          0% {
              opacity: 1;
              transform: scale(1);
          }
          100% {
              opacity: 0;
              transform: scale(0.5);
          }
      }
      .modal {
          display: none;
          position: fixed;
          z-index: 1000;
          left: 0;
          top: 0;
          width: 100%;
          height: 100%;
          overflow: hidden;
          background-color: rgba(0,0,0,0.8);
          backdrop-filter: blur(5px);
      }
      .modal-content {
          position: relative;
          margin: 10% auto;
          padding: 0;
          border-radius: 12px;
          width: 52%; /* Увеличено для мобильных устройств */
          max-width: 241px;
          background-color: rgba(0, 0, 0, 0.5);
          box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
          color: #ffffff; /* Цвет текста в модальном окне */
      }
      .close {
          color: #ffffff;
          font-size: 24px;
          font-weight: bold;
          position: absolute;
          top: 10px;
          right: 15px;
          cursor: pointer;
          transition: color 0.3s;
      }
      .close:hover {
          color: #ff6b6b;
      }
      .modal-content img {
          width: 100%;
          max-height: 70vh; /* Ограничение высоты для предотвращения прокрутки */
          object-fit: contain; /* Сохранение пропорций изображения */
          border-radius: 12px 12px 0 0;
      }
      .share-button {
          background-color: #28a745;
          color: white;
          border: none;
          padding: 10px;
          cursor: pointer;
          border-radius: 4px;
          margin: 10px;
          width: calc(100% - 20px);
          display: block;
          margin-left: auto;
          margin-right: auto;
      }
      .info-button {
          background-color: #007bff;
          color: white;
          border: none;
          padding: 10px;
          cursor: pointer;
          border-radius: 4px;
          transition: background-color 0.3s;
      }
      .info-button:hover {
          background-color: #0056b3;
      }
  </style>
</head>
<body>
  <header>
      <h1>Моя коллекция обоев</h1>
      <button class="theme-toggle" onclick="toggleTheme()">Сменить тему</button>
  </header>
  <div class="upload-form">
      <h2>Загрузить новые обои</h2>
      <input type="file" id="fileInput" accept="image/*">
      <input type="text" id="urlInput" placeholder="Введите URL изображения">
      <button id="uploadButton">Загрузить</button>
  </div>
  <div class="container" id="wallpaperContainer">
      <!-- Здесь будут отображаться загруженные обои -->
  </div>
  <footer>
      <p>&copy; Created by Shokov</p>
      <button class="info-button" onclick="openInfoModal()">О проекте</button>
  </footer>

  <!-- Модальное окно для просмотра изображения -->
  <div id="myModal" class="modal">
      <span class="close" onclick="closeModal()">&times;</span>
      <div class="modal-content">
          <img id="modalImage">
          <button class="share-button" id="shareButton">Поделиться</button>
      </div>
  </div>

  <!-- Модальное окно для информации о проекте -->
  <div id="infoModal" class="modal">
      <span class="close" onclick="closeInfoModal()">&times;</span>
      <div class="modal-content">
          <h2>О проекте</h2>
          <p>
Зачем мы создали этот ресурс? Мы создали контейнер для сохранения ваших любимых изображений на компьютере. Это позволит вам быстро находить их и освободит место на устройстве. Кроме того, вы сможете поделиться ссылкой на обои с друзьями и коллегами.
</p>
<p1>
  Как это работает? Вы можете загрузить свои обои на наш сайт, выбрав один из поддерживаемых форматов: jpeg, jpg или png. Также предусмотрена загрузка обоев по ссылке. После этого вы сможете посмотреть сохранённые обои, просто нажав на них. Если вы передумали сохранять изображение, вы можете удалить его с сайта.
          </p1>
      </div>
  </div>

  <script>
      window.onload = function() {
          loadTheme();
          loadWallpapers();
      };

      const uploadButton = document.getElementById('uploadButton');
      const fileInput = document.getElementById('fileInput');
      const urlInput = document.getElementById('urlInput');
      const wallpaperContainer = document.getElementById('wallpaperContainer');
      const modal = document.getElementById("myModal");
      const modalImage = document.getElementById("modalImage");
      const shareButton = document.getElementById("shareButton");

      uploadButton.addEventListener('click', () => {
          const file = fileInput.files[0];
          const url = urlInput.value.trim();
          if (file) {
              const reader = new FileReader();
              reader.onload = function(e) {
                  addWallpaper(e.target.result);
                  saveToLocalStorage(e.target.result);
                  fileInput.value = ''; // Очистка поля ввода
              };
              reader.readAsDataURL(file);
          } else if (url) {
              addWallpaper(url);
              saveToLocalStorage(url);
              urlInput.value = ''; // Очистка поля ввода
          } else {
              alert('Пожалуйста, выберите изображение или введите URL.');
          }
      });

      function addWallpaper(src) {
          const wallpaperDiv = document.createElement('div');
          wallpaperDiv.classList.add('wallpaper');
          wallpaperDiv.draggable = true;
          wallpaperDiv.innerHTML = `
              <button class="delete-button" onclick="deleteImage(this)">×</button>
              <img src="${src}" alt="Обои" oncontextmenu="return false;" onclick="openModal('${src}')"> 
              <button onclick="downloadImage('${src}')">Скачать</button>
          `;
          wallpaperContainer.appendChild(wallpaperDiv);
      }

      function openModal(src) {
          modal.style.display = "block";
          modalImage.src = src;
          shareButton.onclick = () => {
              if (navigator.share) {
                  navigator.share({
                      title: 'Посмотрите на эти обои!',
                      url: src,
                  })
                  .then(() => console.log('Успешно поделились!'))
                  .catch(error => console.log('Ошибка при попытке поделиться:', error));
              } else {
                  alert("Ваш браузер не поддерживает функцию обмена.");
              }
          };
      }

      function closeModal() {
          modal.style.display = "none";
      }

      function deleteImage(button) {
          const wallpaperDiv = button.parentElement;
          const imageSrc = wallpaperDiv.querySelector('img').src;

          wallpaperDiv.classList.add('fade-out');

          setTimeout(() => {
              wallpaperContainer.removeChild(wallpaperDiv);
              removeFromLocalStorage(imageSrc);
          }, 500);
      }

      function saveToLocalStorage(src) {
          let wallpapers = JSON.parse(localStorage.getItem('wallpapers')) || [];
          if (!wallpapers.includes(src)) {
              wallpapers.push(src);
              localStorage.setItem('wallpapers', JSON.stringify(wallpapers));
          }
      }

      function loadWallpapers() {
          const wallpapers = JSON.parse(localStorage.getItem('wallpapers')) || [];
          wallpaperContainer.innerHTML = '';
          wallpapers.forEach(src => {
              addWallpaper(src);
          });
      }

      function downloadImage(imageSrc) {
          const a = document.createElement('a');
          a.href = imageSrc;
          a.download = 'wallpaper.jpg';
          document.body.appendChild(a);
          a.click();
          document.body.removeChild(a);
      }

      function removeFromLocalStorage(src) {
          let wallpapers = JSON.parse(localStorage.getItem('wallpapers')) || [];
          wallpapers = wallpapers.filter(wallpaper => wallpaper !== src);
          localStorage.setItem('wallpapers', JSON.stringify(wallpapers));
      }

      function toggleTheme() {
          const currentBackground = document.body.style.backgroundColor;
          if (currentBackground === 'rgb(18, 18, 18)') {
              document.body.style.backgroundColor = '#f5f5dc';
              document.body.style.color = '#000000';
              document.querySelector('header').style.backgroundColor = '#e0e0e0';
              document.querySelector('footer').style.backgroundColor = '#e0e0e0';
              document.querySelectorAll('.wallpaper').forEach(wallpaper => {
                  wallpaper.style.backgroundColor = '#ffffff';
              });
              localStorage.setItem('theme', 'light');
          } else {
              document.body.style.backgroundColor = '#121212';
              document.body.style.color = '#ffffff';
              document.querySelector('header').style.backgroundColor = '#1e1e1e';
              document.querySelector('footer').style.backgroundColor = '#1e1e1e';
              document.querySelectorAll('.wallpaper').forEach(wallpaper => {
                  wallpaper.style.backgroundColor = '#1e1e1e';
              });
              localStorage.setItem('theme', 'dark');
          }
      }

      function loadTheme() {
          const theme = localStorage.getItem('theme');
          if (theme === 'light') {
              document.body.style.backgroundColor = '#f5f5dc';
              document.body.style.color = '#000000';
              document.querySelector('header').style.backgroundColor = '#e0e0e0';
              document.querySelector('footer').style.backgroundColor = '#e0e0e0';
              document.querySelectorAll('.wallpaper').forEach(wallpaper => {
                  wallpaper.style.backgroundColor = '#ffffff';
              });
          }
      }

      function openInfoModal() {
          document.getElementById("infoModal").style.display = "block";
      }

      function closeInfoModal() {
          document.getElementById("infoModal").style.display = "none";
      }
  </script>
</body>
</html>
