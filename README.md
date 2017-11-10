


1. Создаем папку *loftschool-webpack-2*, инициализируем npm пакет запустив комманду `npm init -y` в терманале внутрий этой папки. 
2. Инициализируем git запустив `git init` в терминале. Добавляем файл .gitignore в папку и напишем внутрии
    ```
    /node_modules/
    /.git/
    ```
3. Создаем новый репозиторий в github, и коммиттем наш проект туда, как "first commit".
4. Устанавливаем **Webpack2** в наш проект запустив `npm i --save-dev webpack@2`.
5. Добавляем файл **webpack.config.js** для конфигурации webpack.
6. Добавляем javascript модулей для примера
    * Добавим папку *source*
    * Создаем две js файла: index.js и menu.js
    * В файл *menu.js* мы поместим функцию, которая будет создавать список пунктов меню, где `array` массив пунктов меню, а `className` это класс которую нужно присвоить тэгу `ul`. После вызова данная функция будет возвращать html элемент, а именно не нумерованный список. Перед нами **ES6 модул**, изолированный код, которую можно использовать с проекта в проект.
    ```js
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
    * В *index.js* мы импортируем функцию переданную во вне по умолчанию из *menu.js* и присваиваем ей имя `createMenu`. Создаем меню, состоящий из трех пунктов и с классом `menu` в body.
    ```js
    import createMenu from './menu';
    var menu = createMenu(['Главная', 'Обо мне', 'Портфолио'], 'menu');
    document.body.appendChild(menu);
    ``` 
7. Создаем html файлы при помощи **html-webpack-plugin**
    * Установим html-webpack-plugin запустив `npm i --save-dev html-webpack-plugin`;
    * Поместим в файл *webpack.config.js*:
    ```js
    const path = require('path');
    const HTMLWebpackPlugin = require('html-webpack-plugin');

    const PATHS = {
        source: path.join(__dirname, 'source'),
        build: path.join(__dirname, 'build')
    };

    module.exports = {
        entry: PATHS.source + '/index.js',
        output: {
            path: PATHS.build,
            filename: '[name].js'
        },
        plugins: [
            new HTMLWebpackPlugin({
                title: 'Webpack app'
            })
        ]
    };
    ```
    > **path**: базовый модул NodeJS для нахождении пути к проекту    
    > **entry**: точка входа нашего приложения. Точками входа могут являтся те модули, которые не используется другими модулями вашего приложения.     
    > **output**: описывает результат работы Webpack    
    > **plugins**: плагины, которые кастимизирует процесс сборки Webpack. В нашем случае, это HTMLWebpackPlugin, который создает html файл с заданным заголовком. 
8. Запуск Webpack при помощи **npm-скриптов**:
    * В файле *package.json* напишем в формате ключ-значение, где ключ название скрипта, которго мы придумываем, а значение, то что должно запуститься. В нашем случае, это Webpack.
    ```json
    {
        ...
        "scripts": {
            ...
            "start": "webpack"
        }
        ...
    }
    ```
    * Запустим команду `npm start` в терминале. Появится папка *build*, где будет находится два файла: *index.html* и *main.js*;
