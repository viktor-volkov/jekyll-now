---
layout: post
title: Selectize, проброс data-атрибутов
---

[Selectize.js](https://github.com/selectize/selectize.js) - js-библиотека для кастомизации select.

Может быть так, что в вашем js-коде option-ы у select имеют data-атрибуты, и поведение завязано на этом.
Для минимизации изменений в коде имеет смысл пробросить эти data-атрибуты в Selectize. Сделать это можно следующим образом:
1. В js-коде выставим кастомную функцию по отрисовке элементам списка примерно следующего вида:
```javascript
$('#select').selectize({
  //..
  render: {
    option: function(data) {
        if (data.code) {
            return '<div class="option" data-code="' + data.code +'">' + data.text +'</div>'
        }
        else {
            return '<div class="option">' + data.text +'</div>'
        }
    }
  }
  //..
});
```
2. Для нужных элементов списка выставить атрибут data:
```html
<option data-data="{&quot;code&quot;:&quot;code&quot;}">option</option>
```
Обратим внимание, что в качестве значения выступает объект json, с обязательным экранированием кавычек.

3. После выполнения $('#select').selectize() c нужными настройками (включая настройки отрисовки из п.2) у нас получится пробросить в selectize data-атрибуты.
