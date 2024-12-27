---
layout: page
title: Valentin Hata
permalink: /
---

## A page in memory of one good man

<div style="display: flex;">

<div style="flex: 1; padding: 10px;">
    [<button class="btn btn-warning">Стихи</button>](poems)

</div>

<div style="flex: 1; padding: 10px;">
    [<button class="btn btn-info">Проза</button>](prose)

</div>

---

<div id="random-post">
  <!-- Здесь будет отображаться случайное произведение -->
  <h4>Загрузка случайного произведения...</h4>
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

          // Извлекаем содержимое поста
          const postContent = doc.querySelector('.post-content') || doc.querySelector('.page-content');

          // Извлекаем дату поста
          const postDateElement = doc.querySelector('.post-date');
          const postDate = postDateElement ? postDateElement.textContent : 'Дата не указана';

          // Отображаем заголовок, дату и содержимое в контейнере
          const postContainer = document.getElementById('random-post');
          postContainer.innerHTML = `
            <h2><a href="${randomPost.url}">${randomPost.title}</a></h2>
            <p style="font-style: italic; color: gray;">${postDate}</p>
            <div>${postContent ? postContent.innerHTML : 'Содержимое не найдено.'}</div>
          `;
        });
    })
    .catch(error => {
      console.error('Ошибка загрузки:', error);
      const postContainer = document.getElementById('random-post');
      postContainer.innerHTML = '<h5>Ошибка загрузки случайного произведения.</h5>';
    });
</script>
