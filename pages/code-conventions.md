# Code Conventions

В этом разделе описываются требования к коду и архитектуре компонентов.


## Общие принципы

Перед началом работы необходимо прочитать [clean code javascript](https://github.com/ryanmcdermott/clean-code-javascript).
Следование этим правилам обязательно.

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

Для проверки базовых требований к стилю кода используется eslint. Сборка должна проходить без ошибок.

## Компоненты Vue

Компоненты должны быть разделены и независимы, запрещено неявное изменение отображения и логики дочерних компонентов
родительским, для этого есть свойства и методы.

События должны именоваться в стиле kebab-case **без** префикса `on`, а методы, котрые их обрабатывают, 
должны иметь префикс `handle`:

Неправильно:

```vue
<template>
  <some-component @childEvent="onChildEvent" />
</template>

<script>
export default {
  methods: {
    onChildEvent() {
      this.$emit('onParentEvent');
    }
  }
};
</script>
```

Правильно:

```vue
<template>
  <some-component @new-event="handleNewEvent" />
</template>

<script>
export default {
  methods: {
    handleNewEvent() {
      this.$emit('parent-event');
    }
  }
};
</script>
```

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
их удалить из файла.

Нельзя оставлять пустые строки между контентом и тегами, при этом должны быть разделены 
script, template и style.

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

## Стили

1. **Стили обязательно должны быть помечены scoped!**

0. Обязательно использование препроцессора **less**, это облегчает чтение и изменение стилей.

0. Родительские компоненты не должны иметь padding или margin вокруг.

0. Пример правильного оформления стиля UI элемента:

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

0. Стили должны быть названы в `kebab-case`
