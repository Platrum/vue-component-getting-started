# Getting started

Для начала работы у вас должен быть установлен npm (https://nodejs.org/en/download/). Команды 
запускаются в терминале.

## Создание проекта для разработки

Сначала надо установить консольную утилиту `vue`:
```
npm install -g vue-cli
```

После этого можно инициализировать проект:
```
vue init platrum/vue-component-template platrum-components
```

Перейдите в директорию и установите зависимости:

```
cd platrum-components
npm install
```

Сгенерируйте шаблон компонентов, требуемых в ТЗ:

```
node generate.js path/to/file.json
```

Запустите веб-сервер для разработки:

```
npm run dev
```
