---
tags:
  - ВПВответы
---
Структура окна сайта зависит от:
![[Pasted image 20250529171928.png]]

**Document Object Model (DOM)**- это программный интерфейс для HTML и XML документов, который представляет документ в виде дерева объектов. DOM предоставляет структурированное представление документа и определяет, как программы могут получать доступ к структуре, содержанию и стилям документа для их изменения.

## Основные концепции DOM

1. **[Дерево DOM](https://learn.javascript.ru/dom-nodes)** - документ представляется в виде дерева узлов (элементов, атрибутов, текста и т.д.)
    
2. **Узлы (Nodes)** - основные строительные блоки DOM (элементы, атрибуты, текстовые узлы и др.)
    
3. **Элементы (Elements)** - узлы, представляющие HTML-теги
    
4. **Свойства и методы** - интерфейс для взаимодействия с элементами

Пример использования DOM через  document. функции 
```html
<!DOCTYPE html>
<html>
<head>
    <title>DOM Пример</title>
</head>
<body>
    <div id="container">
        <h1>Привет, DOM!</h1>
        <p class="text">Это первый абзац.</p>
        <p class="text">Это второй абзац.</p>
    </div>
    <button id="changeBtn">Изменить текст</button>
    <button id="addBtn">Добавить элемент</button>

    <script>
        // Получаем элементы
        const container = document.getElementById('container');
        const paragraphs = document.getElementsByClassName('text');
        const changeBtn = document.getElementById('changeBtn');
        const addBtn = document.getElementById('addBtn');
        
        // Изменяем текст при клике на первую кнопку
        changeBtn.addEventListener('click', function() {
            for (let i = 0; i < paragraphs.length; i++) {
                paragraphs[i].textContent = 'Текст изменен! ' + (i + 1);
                paragraphs[i].style.color = i % 2 === 0 ? 'red' : 'blue';
            }
        });
        
        // Добавляем новый элемент при клике на вторую кнопку
        addBtn.addEventListener('click', function() {
            const newParagraph = document.createElement('p');
            newParagraph.textContent = 'Это новый абзац, добавленный через DOM.';
            newParagraph.classList.add('text');
            container.appendChild(newParagraph);
        });
    </script>
</body>
</html>
```

Как работает DOM?
### 1. Парсинг HTML

Когда браузер получает HTML-документ, он начинает его **парсить** (анализировать) построчно:

- Встречая тег `<html>`, браузер понимает, что это корень документа
    
- Затем анализируются вложенные теги (`<head>`, `<body>` и т.д.)
    
- Для каждого тега создаётся соответствующий **[DOM-узел](https://learn.javascript.ru/dom-nodes)**
    

### 2. Построение DOM-дерева

Браузер строит **[дерево объектов](https://learn.javascript.ru/dom-nodes)** в памяти:
```html
<html>
  <head>
    <title>Страница</title>
  </head>
  <body>
    <h1>Заголовок</h1>
    <p>Абзац</p>
  </body>
</html>
```

### 3. Построение CSSOM (CSS Object Model)

Параллельно браузер анализирует CSS и строит аналогичное дерево стилей.

### 4. Формирование Render Tree

Браузер объединяет DOM и CSSOM в **Render Tree** - дерево только тех элементов, которые будут отображены на странице (например, скрытые элементы не включаются).

### 5. Layout (Reflow)

Браузер вычисляет точное положение и размер каждого элемента на странице (этот процесс называется "layout" или "reflow").

### 6. Painting

На этом этапе браузер рисует пиксели на экране согласно вычисленным данным.

## Как JavaScript взаимодействует с этим процессом?

Когда вы используете JavaScript для изменения DOM:

```js
document.querySelector('h1').textContent = 'Новый текст';
```

Браузер:

1. Находит элемент в DOM
    
2. Изменяет его содержимое
    
3. Запускает процесс **reflow** (перерасчёт layout)
    
4. Запускает **repaint** (перерисовку)