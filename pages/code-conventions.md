# Code Conventions

В этом разделе описываются требования к коду и архитектуре компонентов, следование
которым обязательно для участия в разработке проекта.


## Общие принципы

Перед началом работы рекомендуется прочитать [clean code javascript](https://github.com/ryanmcdermott/clean-code-javascript).

**Именование файлов**

Все директории, .js и .less файлы называются в стиле camelCase, все компоненты называются
в стиле PascalCase.

**Дублирование кода запрещено**

Если для решения задачи не используется готовый mixin из библиотеки ui, для этого
должно быть обоснование, иначе задача не считается выполенной. Это касается и js, и
стилей. См. https://ru.vuejs.org/v2/guide/mixins.html

Исключением является вызов $emit, если событие не требует дополнительных параметров:

```js
export default {
  methods: {
    handleBlur() {
      this.emitBlur();
    },
    handleOtherEvent() {
      this.emitBlur();
    },
    // можно не делать этот метод
    emitBlur() {
      this.$emit('blur');
    }
  }
}
```


## Code Style

Для проверки базовых требований к стилю кода используется eslint (для настройки 
см. раздел [Getting Started](getting-started.md)).

#### Vue

1. **Стили обязательно должны быть помечены scoped!**

2. Обязательно использование препроцессора **less**, это облегчает чтение и изменение стилей.

3. Компоненты должны быть разделены и независимы, запрещено неявное изменение отображения и логики дочерних компонентов
родительским, для этого есть свойства и методы.


Правильный порядок тегов в компоненте:

```vue
<template>
  <div>Component</div>
</template>

<script>
  export default {};
</script>

<style lang="less" scoped>

</style>
```

Пустые теги рекомендуется убирать. Если в компоненте отсутствует шаблон или стили, лучше
их удалить из файла. Порядок полей в объекте должен быть следующим:

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

Неправильно:

```html
<template>

  <div>{{ message }}</div>
</template>


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
```

Правильно:

```html
<template>
  <div>{{ message }}</div>
</template>

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
