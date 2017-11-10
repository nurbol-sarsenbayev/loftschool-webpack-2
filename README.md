


1. Создаем папку `loftschool-webpack-2`, инициализируем npm пакет запустив комманду `npm init -y` в терманале внутрий этой папки. 
2. Добавляем файл .gitignore в папку и напишем внутрии и инициализируем git запустив `git init` в терминале.
    ```
    /node_modules/
    /.git/
    ```
3. Создаем новый репозиторий в github, и коммиттем наш проект туда, как "first commit".
4. Устанавливаем Webpack2 в наш проект запустив `npm i --save-dev webpack@2`.
5. Добавляем файл webpack.config.js для конфигурации webpack.
6. Добавляем javascript модулей для примера
    1. Добавим папку sources
    2. Создаем два js файла: index.js и menu.js
    3. В файл menu.js мы поместим функцию, которая будет создавать список пунктов меню,```js
    export default function (array, className) {
        var menu = document.createElement("ul");
        menu.className = className;
        var listItems = '';
        array.forEach(function(item) {
            listItems += '<li>' + item + '</li>'; 
        });
        menu.innerHTML = listItems;
        return menu;
    }
    ```     
    где *array* массив пунктов меню, а *className* это класс которую нужно присвоить тэгу ul. После вызова данная функция будет возвращать html элемент, а именно не нумерованный список. Перед нами ES6 модул, изолированный код, которую можно использовать с проекта в проект.
    4. В index.js мы импортируем функцию переданную во вне по умолчанию из menu.js и присваиваем ей имя *createMenu*. Создаем меню, состоящий из трех пунктов с классом *menu* в body.
    ```js
    import createMenu from './menu';
    var menu = createMenu(['Главная', 'Обо мне', 'Портфолио'], 'menu');
    document.body.appendChild(menu);
    ``` 