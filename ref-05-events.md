## SyntheticEvent

Ваши обработчики событий будут передавать экземпляры `SyntheticEvent`. Это кросс-браузерная обертка вокруг нативных браузерных событий. Она имеет такой же интерфейс как у нативных браузерных событий, включая `stopPropagation()` и `preventDefault()`, за исключением событий, работающих одинаково во всех браузерах.

Если вы обнаружите, что вам нужно событие, лежащее в основе браузера по какой-то причине, просто используйте атрибут `nativeEvent`, чтобы получить его. Каждый объект `SyntheticEvent` имеет следующие атрибуты:

```javascript
boolean bubbles
boolean cancelable
DOMEventTarget currentTarget
boolean defaultPrevented
number eventPhase
boolean isTrusted
DOMEvent nativeEvent
void preventDefault()
boolean isDefaultPrevented()
void stopPropagation()
boolean isPropagationStopped()
DOMEventTarget target
number timeStamp
string type
```

> Примечания:
>
> На момент выхода v0.14, возвращение `false` из обработчика событий не будет останавливать событие. При необходимости вызывайте `e.stopPropagation()` или `e.preventDefault()` чтобы остановить событие.

## Объединение событий

`SyntheticEvent` объединяет. Это означает, что объекты `SyntheticEvent` будут переиспользоваться и все свойства будут аннулированы после вызова колбека события.
Это сделано из-за соображений производительности.
Таким образом, вы не можете получить доступ к событию в асинхронном режиме.

```javascript
function onClick(event) {
  console.log(event); // => nullified object.
  console.log(event.type); // => "click"
  var eventType = event.type; // => "click"

  setTimeout(function() {
    console.log(event.type); // => null
    console.log(eventType); // => "click"
  }, 0);

  this.setState({clickEvent: event}); // Won't work. this.state.clickEvent will only contain null values.
  this.setState({eventType: event.type}); // You can still export event properties.
}
```

> Примечания:
>
> Если вы хотите получить доступ к свойствам события асинхронно, то вы должны вызвать у события метод `event.persist()`, который может убрать искусственное событие (synthetic event) из пула и позволит событиям храниться в коде пользователя.

## Поддерживаемые События

React нормализует события так, что они имеют стабильные характеристики в различных браузерах.

Обработчики событий ниже срабатывают по событию во всплывающей фазе (bubbling phase). Для регистрации обработчика событий в фазе захвата (capture phase), добавьте `Capture` с именем события; Например, вместо того, чтобы использовать `onClick`, вы можете использовать `onClickCapture`, чтобы обработать событие клика в фазе захвата.


### Буфер обмена событий

Наименование события:

```
onCopy onCut onPaste
```

Свойства:

```javascript
DOMDataTransfer clipboardData
```


### Составные события

Наименование события:

```
onCompositionEnd onCompositionStart onCompositionUpdate
```

Свойства:

```javascript
string data

```


### События клавиатуры

Наименование события:

```
onKeyDown onKeyPress onKeyUp
```

Свойства:

```javascript
boolean altKey
number charCode
boolean ctrlKey
boolean getModifierState(key)
string key
number keyCode
string locale
number location
boolean metaKey
boolean repeat
boolean shiftKey
number which
```


### События фокуса

Наименование события:

```
onFocus onBlur
```

Свойства:

```javascript
DOMEventTarget relatedTarget
```

Эти события фокуса работают на всех элементах в React DOM, не только на элементах формы.

### События формы

Наименование события:

```
onChange onInput onSubmit
```

Для подробной информации по событию onChange, смотрите [Forms](/react/docs/forms.html).


### События мыши

Наименование события:

```
onClick onContextMenu onDoubleClick onDrag onDragEnd onDragEnter onDragExit
onDragLeave onDragOver onDragStart onDrop onMouseDown onMouseEnter onMouseLeave
onMouseMove onMouseOut onMouseOver onMouseUp
```

Свойства:

```javascript
boolean altKey
number button
number buttons
number clientX
number clientY
boolean ctrlKey
boolean getModifierState(key)
boolean metaKey
number pageX
number pageY
DOMEventTarget relatedTarget
number screenX
number screenY
boolean shiftKey
```


### Selection events

Наименование события:

```
onSelect
```


### Touch events

Наименование события:

```
onTouchCancel onTouchEnd onTouchMove onTouchStart
```

Свойства:

```javascript
boolean altKey
DOMTouchList changedTouches
boolean ctrlKey
boolean getModifierState(key)
boolean metaKey
boolean shiftKey
DOMTouchList targetTouches
DOMTouchList touches
```


### UI Events

Наименование события:

```
onScroll
```

Свойства:

```javascript
number detail
DOMAbstractView view
```


### Wheel Events

Наименование события:

```
onWheel
```

Свойства:

```javascript
number deltaMode
number deltaX
number deltaY
number deltaZ
```

### Media Events

Наименование события:

```
onAbort onCanPlay onCanPlayThrough onDurationChange onEmptied onEncrypted onEnded onError onLoadedData onLoadedMetadata onLoadStart onPause onPlay onPlaying onProgress onRateChange onSeeked onSeeking onStalled onSuspend onTimeUpdate onVolumeChange onWaiting
```

### Image Events

Наименование события:

```
onLoad onError
```
