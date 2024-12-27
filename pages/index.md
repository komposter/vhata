---
layout: page
title: Valentin Hata
permalink: /
---

## A page in memory of one good man

[<button class="btn btn-warning">Стихи</button>](poems)    [<button class="btn btn-info">Проза</button>](prose)

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

          // Извлекаем заголовок и содержимое поста
          const postTitle = doc.querySelector('h1').textContent;
          const postContent = doc.querySelector('.post-content') || doc.querySelector('.page-content');

          // Отображаем содержимое в контейнере
          const postContainer = document.getElementById('random-post');
          postContainer.innerHTML = `
            <h2>${postTitle}</h2>
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
