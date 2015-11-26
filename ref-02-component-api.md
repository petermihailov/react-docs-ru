---
id: component-api
title: Component API
permalink: component-api.html
prev: top-level-api.html
next: component-specs.html
---

## React.Component

Экземпляры React компонента создаются внутри React при рендере. Эти экземпляры повторно используются в последующих рендерах, и могут быть доступны в методах ваших компонентов как `this`. Единственный способ получить обработчик экземпляра React-компонента за пределами React - это сохранять возвращаеме значение в `ReactDOM.render`. Внутри других компонентов вы можете использовать [refs](/react/docs/more-about-refs.html) чтобы достичь тогоже результата.


### setState

```javascript
void setState(
  function|object nextState,
  [function callback]
)
```

Объединяет nextState с текущим состоянием. Это основной метод который вы используете, чтобы вызвать обновления пользовательского интерфейса из обработчиков событий и обратных вызовов из запросов к серверу.

Первым аргументом может быть объект (содержащий ноль или более ключей для обновления) или функция (состояния `state` и свойства `props`) которая возвращает объект, содержащий ключи для обновления.

Простой пример использования объекта:

```javascript
setState({mykey: 'my new value'});
```

Также возможно передать функцию с сигнатурой `function(state, props)`. Это может быть полезным в некоторых случаях, когда вы хотите обновить предыдущее значение state+props до того, как будет установлено какое-либо значение state:

```javascript
setState(function(previousState, currentProps) {
  return {myInteger: previousState.myInteger + 1};
});
```

Второй (необязательный) параметр - это колбек, который будет вызван по окончании `setState` и компонент будет перерендерен.

> Примечанияs:
>
> *НИКОГДА* не изменяйте `this.state` непосредственно вызовом `setState()`, который может заменить изменения которые вы сделали. Обрабатывайте `this.state`, как будто оно было неизменным.
>
> `setState()` не сразу изменяет `this.state`, но создает состояние отложенного перехода. Доступ `this.state` после вызова этого метода потенциально может вернуть существующее значение.
>
> Нет никакой гарантии, синхронной работы операций вызова `setState`, вызовы могут группироваться в целях повышения производительности.
>
> `setState()` всегда будет вызывать повторный рендеринг, пока условная логика рендеринга не реализуется в `shouldComponentUpdate()`. Если изменяемые объекты используются и логика не может быть реализована в `shouldComponentUpdate()`, вызывается `setState()` только тогда, когда новое состояние отличается от предыдущего состояния чтобы избежать ненужного ререндеринга.


### replaceState

```javascript
void replaceState(
  object nextState,
  [function callback]
)
```

Как `setState()`, но удаляет любые ранее существующие ключи состояния, которые не находятся в nextState.

> Примечания:
>
> Этот метод не поддерживается в ES6 `React.Component` и возможно будет удален в последующих версиях React


### forceUpdate

```javascript
void forceUpdate(
  [function callback]
)
```

По умолчанию, когда `state` или `props` вашего компонента меняется, ваш компонент перерисовывается. Однако, если это не явные изменения (например, данные глубоко внутри объекта меняются без изменения самого объекта) или если ваш метод `render()` зависит от каких-либо других данных, вы можете сказать React, что хотите перезапустить метод `render()` вызовом `forceUpdate()`.

Вызов `forceUpdate()` будет причиной `render()` вызванный у компонента, опустить `shouldComponentUpdate()`. This will trigger the normal lifecycle methods for child components, including the `shouldComponentUpdate()` method of each child. React will still only update the DOM if the markup changes.

Normally you should try to avoid all uses of `forceUpdate()` and only read from `this.props` and `this.state` in `render()`. This makes your component "pure" and your application much simpler and more efficient.


### getDOMNode

```javascript
DOMElement getDOMNode()
```

Если этот компонент был монтирован в DOM, то этот метод вернет соответствующий нативный DOM-элемент. Этот метод полезен для чтения значений из DOM, такие как значение поля формы и выполнение измерений DOM. Когда `render` возвращает `null` или `false`, `this.getDOMNode()` возвращает `null`.

> Примечания:
>
> getDOMNode устарела и была заменена [ReactDOM.findDOMNode()](/react/docs/top-level-api.html#reactdom.finddomnode).
>
> Этот метод не поддерживается в ES6 `React.Component` и возможно будет удален в последующих версиях React


### isMounted

```javascript
boolean isMounted()
```

`isMounted()` возвращает `true`, если компонент смонтирован в DOM, в противном случае `false`. Вы можете использовать этот метод, чтобы защитить асинхронные вызовы `setState()` или `forceUpdate()`.

> Примечания:
>
> Этот метод не поддерживается в ES6 `React.Component` и возможно будет удален в последующих версиях React


### setProps

```javascript
void setProps(
  object nextProps,
  [function callback]
)
```

Когда вы интегрируетесь с внешним приложением JavaScript вы можете желать получать сигналы изменения в React компонентах, отрендеренного `ReactDOM.render()`.

Вызов `setProps()` может быть вызван только на компоненте корневого уровня. (root-level) и может изменять его свойства, а затем перерисовыть. Кроме того, вы можете поставить дополнительный коллбек, который выполняется когда `setProps` завершит свою работу, а затем компонент перерисуется.

> Примечания:
>
>Когда это возможно, вызывайте `ReactDOM.render()` на том же узле, это производительнее.
>
> Этот метод может быть вызван только на компоненте корневого уровня. Поэтому, он доступен только на компоненте переданном непосредственно в `ReactDOM.render()` и ни на одном из его дочерних элементов. Если вы склонны к использованию `setProps()` на дочернем компоненте, вместо использования реактивных обновлений, то передайте новое свойство в дочерний компонент при его создании в `render()`.
>
> Этот метод не поддерживается в ES6 `React.Component` и возможно будет удален в последующих версиях React

### replaceProps

```javascript
void replaceProps(
  object nextProps,
  [function callback]
)
```

Как `setProps()` но удаляет любые ранее существующие свойства, вместо объединения двух объектов.

> Примечания:
>
> Этот метод не поддерживается в ES6 `React.Component` и возможно будет удален в последующих версиях React
