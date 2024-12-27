---
layout: page
title: Valentin Hata
permalink: /
---

### A page in memory of one good man

[<button class="btn btn-warning">Стихи</button>](poems)

[<button class="btn btn-info">Проза</button>](prose)


<br /><br />

#### Random poem


<br /><br />

<div id="random-post">
  <!-- Здесь будет отображаться случайный пост -->
  <h2>Загрузка случайного поста...</h2>
</div>

<script>
  // Загружаем список постов из JSON-файла
  fetch('/posts.json')
    .then(response => response.json())
    .then(posts => {
      // Выбираем случайный пост
      const randomPost = posts[Math.floor(Math.random() * posts.length)];

      // Находим контейнер для отображения поста
      const postContainer = document.getElementById('random-post');
      postContainer.innerHTML = `
        <h2>${randomPost.title}</h2>
        <div>${randomPost.content}</div>
      `;
    })
    .catch(error => {
      console.error('Ошибка загрузки списка постов:', error);
      const postContainer = document.getElementById('random-post');
      postContainer.innerHTML = '<h2>Ошибка загрузки случайного поста.</h2>';
    });
</script>
