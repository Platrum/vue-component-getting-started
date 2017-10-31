# Code Conventions

В этом разделе описываются требования к коду и архитектуре компонентов, следование
которым обязательно для участия в разработке проекта.

## Общие принципы

**Дублирование кода запрещено**

    Если для решения задачи не используется готовый mixin из библиотеки ui, для этого
    должно быть обоснование, иначе задача не считается выполенной.

    Функции общего назначения должны быть вынесены в отдельные js файлы с соответствующим
    названием.

## Code Style

Для проверки базовых требований к стилю кода используется eslint (для настройки 
см. раздел Getting Started).

#### Vue

Пустые теги рекомендуется убирать. Если в компоненте отсутствует шаблон или стили, лучше
их удалить из файла.
Порядок полей в объекте должен быть следующим:

* mixins
* components
* props
* beforeCreate
* created
* beforeMount
* mounted
* beforeUpdate
* updated
* activated
* deactivated
* beforeDestroy
* destroyed
* data
* computed
* watch
* methods

Нельзя оставлять пустые строки между контентом и тегами, при этом должны быть разделены 
script, template и style

Правильно:

```html
<script>
  import 'module';
  
  export default {
    data() {
      return {
        message: 'test'
      };
    }
  };
</script>

<template>
  <div>{{ message }}</div>
</template>
```

Неправильно:

```html
<script>

  import 'module';
  
  export default {
    data() {
      return {
        message: 'test'
      };
    }
  };
  
</script>
<template>

  <div>{{ message }}</div>
</template>
```

#### Less

1. Пример правильного оформления стиля UI элемента:

    ```less
    @color1: white; /* переменные без отступа сверху, всегда выше стилей */
    
    .module-wrapper { /* всегда отступ в одну строку сверху */
      @color2: black;
      background-color: @color2; /* стили без отступа сверху */
      border-color: @color1;
      
      .module-internal-content {
      
        &:hover { /* рекомендуется использовать & */
          color: red;
        }
      }
    }
    ```
    
0. Запрещено дублировать стили. Если одинаковый стиль используется в нескольких 
компонентах, надо вынести его в отдельный файл в виде миксина или переменной.
