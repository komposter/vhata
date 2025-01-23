---
layout: page
title: Valentin Hata
permalink: /
---
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
    
            // Генерируем хлебные крошки
            const crumbs = randomPost.url.split('/').filter(Boolean); // Разбиваем URL на части
            let breadcrumbHtml = '<nav aria-label="breadcrumb" class="breadcrumb-nav"><ol class="breadcrumb">';
            let crumbPath = '/'; // Начальный путь
    
            crumbs.forEach((crumb, index) => {
              crumbPath += crumb + '/'; // Строим путь по мере итерации
              const crumbName = decodeURIComponent(crumb) // Декодируем URL
                .replace('-', ' ') // Заменяем дефисы на пробелы
                .replace('.html', '') // Убираем расширение .html
                .charAt(0).toUpperCase() + crumb.slice(1); // Преобразуем в заголовок
              if (index === crumbs.length - 1) {
                breadcrumbHtml += `<li class="breadcrumb-item active" aria-current="page">
                  <a href="${randomPost.url}">${crumbName}</a>
                </li>`;
              } else {
                breadcrumbHtml += `<li class="breadcrumb-item"><a href="${crumbPath}">${crumbName}</a></li>`;
              }
            });
    
            breadcrumbHtml += '</ol></nav>';
    
            // Отображаем хлебные крошки и содержимое в контейнере
            const postContainer = document.getElementById('random-post');
            postContainer.innerHTML = `
              ${breadcrumbHtml}
              ${postContent ? postContent.outerHTML : '<p>Содержимое не найдено.</p>'}
            `;
          });
      })
      .catch(error => {
        console.error('Ошибка загрузки:', error);
        const postContainer = document.getElementById('random-post');
        postContainer.innerHTML = '<h5>Ошибка загрузки случайного произведения.</h5>';
      });
</script>