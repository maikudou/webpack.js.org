---
title: Вывод
sort: 3
contributors:
  - TheLarkInn
  - chyipin
  - rouzbeh84
  - byzyk
  - maikudou
---

Настройка `output` в конфигурационном файле указывает webpack'у как сохранять скомпилированные файлы на диск. Обратите внимание, что несмотря на то, что допустимо наличие нескольких точек входа, в конфигурации возможен только один вывод в поле `output`. 


## Использование

Минимальным требованием для указанять свойства `output` в вашей конфигурации является передача в него объекта, состоящего из:

- Аттрибута `filename`, который будет использоваться для выводимого файла(ов).

__webpack.config.js__

```javascript
module.exports = {
  output: {
    filename: 'bundle.js',
  }
};
```

Эта конфигурация выведет в папку `dist` единственный файл `bundle.js`.


## Несколько Входных Точек

Если ваша конфигурация подразумевает более одного "чанка" (например, если указано несколько входных точек или если используется плагин CommonsChunkPlugin), то чтобы быть уверенным, что каждый файл получит уникальное имя, вам следует использовать [подстановки](/configuration/output#output-filename).

```javascript
module.exports = {
  entry: {
    app: './src/app.js',
    search: './src/search.js'
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/dist'
  }
};

// пишет на диск: ./dist/app.js, ./dist/search.js
```


## Продвинутое использование

Вот более сложный пример, использующий CDN и хеши ресурсов:

__config.js__

```javascript
module.exports = {
  //...
  output: {
    path: '/home/proj/cdn/assets/[hash]',
    publicPath: 'https://cdn.example.com/assets/[hash]/'
  }
};
```

В случае если путь, указанный в `publicPath` еще не известен в момент компиляции, его можно опустить и указать динамически во время выполнения, переопределив переменную `__webpack_public_path__` в файле-точке входа.

```javascript
__webpack_public_path__ = myRuntimePublicPath;

// остальной код приложения
```
