## React
`React` - точка входа в React-библиотеку. Если вы используете один из уже собранных пакетов, то он доступен вам глобально; Если вы используете CommonJS-модули, подключите его через `require()`.


### React.Component

```javascript
class Component
```

Это базовый класс компонентов React, если они объявлены с помощью ES6 классов. Смотрите [Reusable Components](/react/docs/reusable-components.html#es6-classes) для того, чтобы понять как использовать ES6 классы в React. Для просмотра всех предусмотренных базовым классом методов, смотрите [Component API](/react/docs/component-api.html).


### React.createClass

```javascript
ReactClass createClass(object specification)
```

Компонент реализует метод `render`, который возвращает **один единственный** дочерний элемент. Этот дочерний элемент в своей структуре может иметь произвольную глубину дочерних элементов. Единственное, что делает компоненты отличными от стандартных прототипных классов это то что вам не нужно вызывать(писать) new перед ними. TОни являются удобными обертками, которые возвращают сконструированные экземпляры (через new).

Подробную информацию смотрите тут [Component Specs and Lifecycle](/react/docs/component-specs.html).


### React.createElement

```javascript
ReactElement createElement(
  string/ReactClass type,
  [object props],
  [children ...]
)
```

Создает и Возвращает новый `ReactElement` заданного типа. Аргументом типа может быть либо строка "имя тега HTML" (например, "div", "span", и т.д.), либо `ReactClass` класс (созданый с помощью `React.createClass`).


### React.cloneElement

```
ReactElement cloneElement(
  ReactElement element,
  [object props],
  [children ...]
)
```

Копирует и возвращает новый `ReactElement` используя `element` в качестве стартовой точки. В результате элемент будет иметь собственные свойства `props` и новые неглубоко объединенные свойства. Новые дети заменят старых детей. Используйте `React.addons.cloneWithProps`, чтобы `key` и `ref` из оригинального элемента были сохранены. Это не специальное поведение объединения различный свойств (в отличнии от `cloneWithProps`). Смотрите [v0.13 RC2 blog post](/react/blog/2015/03/03/react-v0.13-rc2.html) для дополнительных деталей.


### React.createFactory

```javascript
factoryFunction createFactory(
  string/ReactClass type
)
```

Возвращает функцию, которая создает ReactElement-ы заданного типа. Как и в случае с `React.createElement`,
аргументом типа может быть либо строка "имя тега HTML" (например, "div", "span", и т.д.), либо `ReactClass`


### React.isValidElement

```javascript
boolean isValidElement(* object)
```

Проверяет, является ли объект ReactElement-ом.


### React.DOM

`React.DOM` обеспечивает удобную обертку вокруг `React.createElement` для DOM-компонентов. Она должна использоваться только в том случае, если вы не используете JSX. Пример использования: `React.DOM.div(null, 'Hello World!')`


### React.PropTypes

`React.PropTypes` используются для проверки свойств, которые передаются в компоненты. Для получения более подробной информации о `propTypes` см [Многоразовые компоненты](/react/docs/reusable-components.html).


### React.Children

`React.Children` предоставляет утилиты для работы с `this.props.children` непрозрачной структуры данных.


#### React.Children.map

```javascript
array React.Children.map(object children, function fn [, object thisArg])
```

Вызов `fn` для каждого дочернего элемента содержащегося в `children` установить `thisArg`. Если `children` - это вложенный объект или массив, то он тоже будет пройден: `fn` никогда не будут передаваться объекты контейнеров. Если дочерний элемент равен `null` или `undefined`, вернется `null` или `undefined` а не массив.


#### React.Children.forEach

```javascript
React.Children.forEach(object children, function fn [, object thisArg])
```

Работает как `React.Children.map()` только не возвращает массив.


#### React.Children.count

```javascript
number React.Children.count(object children)
```

Возвращает количество дочерних элементов `children`, это количество равно числу вызываемых `map` или `forEach` колбеков.


#### React.Children.only

```javascript
object React.Children.only(object children)
```

Возвращает одного ребенка `children` (если он один). В противном случае выбрасывает исключение.


#### React.Children.toArray

```javascript
array React.Children.toArray(object children)
```

Возвращает `children` непрозрачной структуры данных в виде плоского массива с ключами, назначенными каждому ребенку. Это полезно, если вы хотите, манипулировать коллекциями детей в ваших `render()`-методах, а особенно если вы хотите, изменить порядок или взять часть `this.props.children` перед передачей куда-нибудь еще.


## ReactDOM

Модуль `react-dom` предоставляет DOM-методы, которые могут быть использованы на верхнем уровне вашего приложения. Большинство ваших компонентов не должны использовать этот модуль.


### ReactDOM.render

```javascript
ReactComponent render(
  ReactElement element,
  DOMElement container,
  [function callback]
)
```

Отрисовывает ReactElement в DOM в контейнере `container` и возвращает [reference](/react/docs/more-about-refs.html) в компонент (или возвращает `null` для [компонентов не имеющих состояния](/react/docs/reusable-components.html#stateless-functions)).

Если ReactElement уже был отрисован в контейнере `container`, то выполнится обновление только изменившейся части React-компонента.

Если указан необязательный колбек, то он вызовется, когда компонент будет отрисован.

> Примечания:
>
> `ReactDOM.render()` управляет содержимым контейнера, который вы в него передаете. Любые DOM-элементы, котороые находились внутри этого контейнера, заменяются при первом вызове `ReactDOM.render()`. Последующие вызовы вызывают эффективный алгоритм Реакта определения и обновления изменений DOM.
>
> `ReactDOM.render()` не меняет ветку контейнера (изменят только его дочерние элементы). В дальнейшем, скорее всего появится возможность вставить компонент в существующий DOM-узел без перезаписи существующих в нем дочерних элементов.


### ReactDOM.unmountComponentAtNode

```javascript
boolean unmountComponentAtNode(DOMElement container)
```

Убирает отрисованный React-компонент из DOM и очищает его обработчики событий и состояние. Если компонента в контейнере нет, вызов этой функции ничего не сделает. Вернет `true` если компонент был убран и `false` если `unmountComponentAtNode` не нашел, что убрать.


### ReactDOM.findDOMNode

```javascript
DOMElement findDOMNode(ReactComponent component)
```

Если этот компонент был отрисован в DOM, то будет возвращен соответствующий нативный DOM-элемент. Этот метод полезен для чтения значений из DOM, некоторых полей форм и выполнения измерений DOM. **В большинстве случаев, вы можете прикрепить поля к `ref` и не использовать ` findDOMNode` вообще.**

Когда `render` возвращает `null` или `false`, `findDOMNode` возвращает `null`.


> Примечания:
>
> `findDOMNode()` - это своеобразный аварийный люк для доступа к DOM узлу. В большинстве случаев его использование не рекомендуется.
>
> `findDOMNode()` работает только с примонтированными компонентами (то есть компонентами, которые были помещены в DOM). Если вы попробуете вызвать его на компоненте, который еще не был примонтирован (как и вызов `findDOMNode()` в методе `render()` на компоненте, который еще не создан) вам выдаст исключение.
>
> `findDOMNode()` не может быть использован в stateless-компонентах.


## ReactDOMServer

Модуль `react-dom/server` позволяет вам рендерить ваши компоненты на сервере.


### ReactDOMServer.renderToString

```javascript
string renderToString(ReactElement element)
```

Отрисовывает ReactElement в HTML. Этот метод должен быть использован только на сервере. Вы можете использовать этот метод для генерации HTML на сервере и отправки готовой разметки для более быстрой загрузки страницы, а также для SEO-оптимизации.

Если вывызываете `ReactDOM.render()` на узле, в котором уже есть этот отрендеренная разметка, React оставит его, и добавит отбработчики событий, получая высокопроизводительную first-load загрузку.


### ReactDOMServer.renderToStaticMarkup

```javascript
string renderToStaticMarkup(ReactElement element)
```

Подобно `renderToString` метод не создает дополнительные DOM аттрибуты, такие как `data-react-id`, которые использует React. Это полезно если вы хотите использовать React как простой генератор статичных страниц, а без дополнительных аттрибутов страница может сэкономить много байт.