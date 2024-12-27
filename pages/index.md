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

      // Находим контейнер для отображения
      const postContainer = document.getElementById('random-post');
      postContainer.innerHTML = `
        <h2>${randomPost.title}</h2>
        <div>${randomPost.content}</div>
      `;
    })
    .catch(error => {
      console.error('Ошибка загрузки списка произведений:', error);
      const postContainer = document.getElementById('random-post');
      postContainer.innerHTML = '<h5>Ошибка загрузки случайного произведения.</h5>';
    });
</script>
