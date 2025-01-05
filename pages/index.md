---
layout: page
title: Valentin Hata
permalink: /
---


[//]: # ([<button class="btn btn-warning">&nbsp;&nbsp;&nbsp;Все стихи&nbsp;&nbsp;&nbsp;</button>]&#40;poems&#41;&nbsp;&nbsp;&nbsp;&nbsp;[<button class="btn btn-info">&nbsp;&nbsp;&nbsp;Вся проза&nbsp;&nbsp;&nbsp;</button>]&#40;prose&#41;&nbsp;&nbsp;&nbsp;&nbsp;[<button class="btn btn-success">&nbsp;&nbsp;&nbsp;Загрузить случайное&nbsp;&nbsp;&nbsp;</button>]&#40;&#41;)

[//]: # (<br>)

<div id="random-post">
  <!-- Здесь будет отображаться случайное произведение -->
  <h4> </h4>
</div>

<script>
  // Загружаем список из JSON-файла
  fetch('/vhata/posts.json')
    .then(response => response.json())
    .then(posts => {
      // Выбираем случайное произведение из списка
      const randomPost = posts[Math.floor(Math.random() * posts.length)];

      // Загружаем содержимое страницы выбранного поста
      return fetch(randomPost.url)
        .then(response => response.text())
        .then(html => {
          // Парсим HTML содержимое страницы
          const parser = new DOMParser();
          const doc = parser.parseFromString(html, 'text/html');

          // Извлекаем только содержимое поста
          const postContent = doc.querySelector('.post-content');

          // Отображаем содержимое в контейнере
          const postContainer = document.getElementById('random-post');
          postContainer.innerHTML = postContent ? postContent.outerHTML : 'Содержимое не найдено.';
        });
    })
    .catch(error => {
      console.error('Ошибка загрузки:', error);
      const postContainer = document.getElementById('random-post');
      postContainer.innerHTML = '<h5>Ошибка загрузки случайного произведения.</h5>';
    });
</script>
