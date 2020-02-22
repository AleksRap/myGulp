# Сборщик проектов Gulp

## Инициализация

Запускаем установку зависимостей

    npm i
    
## Запуск сборщика

Сборщик имеет два режима:

1. dev (по умолчанию) - режим разработки в котором:

        - Используется инкрементная сборка шаблонов
        - Создается локальный сервер
        - НЕ сжимаются изображения,
        - НЕ добавляются префиксы,
        - НЕ минифицируется код,
        - НЕ создаются карты для отладки
        - НЕ заменяются ссылки подключенных файлов на их сжатые версии
    
2. prod - режим сборки для продакшена. Процесс проихсодит со всеми опитмизациями файлов, соответсвтенно длится дольше

        - НЕ создается локальный сервер
        - используется обычная сборка шаблонов

Режим разработки запускается **NPM** командой

    default dev
    
Чтобы собрать проект для продакшена используйте команду 

    default prod
    
## Эффективная разработка

Моменты, которые стоит учитывать, для более эффективной разработки:

#### src/js/libs.js
    
    Новые библиотеки добавлять в формате:
    @@include('./имя библиотеки/внутренний путь до файла')
    
Папка node_modules указана по дефолту

    Пример:
    @@include('./jquery/dist/jquery.js')
    
-
    
#### src/js/script.js
    
    Новые модули добавлять в формате:
    {@@include('имя модуля.js')}
    
Папка src/js/modules указана по дефолту. Не забывайте про фигурные скобки {}. Они предотвращают конфликт имен создавая для каждого модуля свою область видимости
    
    Пример:
    {@@include('svg4evrybody.js')}
    
-

#### src/styles/libs.css
    
    Новые библиотеки добавлять в формате:
    @@include('./имя библиотеки/внутренний путь до файла')
    
Папка node_modules указана по дефолту
    
    Пример:
    @@include('./bootstrap/dist/css/bootstrap.css')
    
-

#### SVG спрайт
`Иконки отображаются ТОЛЬКО при просмотре на сервере! Не важно каком локальном или удаленном`

Для спрайта **НЕ** использовать многоцветные иконки, т.к при сборке в спрайт все стили внутри svg сбрасываются и иконки становятся одного цвета.

При добавлении новой иконки в папку ***src/svg/sprite*** она автоматически добавляется в спрайт, а ее размеры добавляются в файл ***src/styles/sprite/sprite.scss***. В этом же файле можно изменить/добавить стили для каждой иконки.

Для добавления иконки на страничку используйте миксин **svg-icon** в параметрах которого нужно указать имя иконки (должно соответсвовать названию файла иконки в папке ***src/svg/sprite***) и модификатор, если таковой имеется.

Не забывайте инклудить миксин на страницу, где он используется!

    
До сборки:
    
    include mixins/svg-icon
    +svg-icon('arrow-left', 'red')
    
После:
    
```html
<svg class="sprite sprite__arrow-left sprite__arrow-left_red">
  <use xlink:href="svg/sprite.svg#arrow-left"></use>
</svg>
```