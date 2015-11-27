## Supported Tags

React старается поддерживать все распространенные елементы. Если вам нужен элемент, которого нет в этом списке, пожалуйста, [напишите сюда](https://github.com/facebook/react/issues/new).

### HTML элементы

Поддерживаются следующие HTML элементы:

```
a abbr address area article aside audio b base bdi bdo big blockquote body br
button canvas caption cite code col colgroup data datalist dd del details dfn
dialog div dl dt em embed fieldset figcaption figure footer form h1 h2 h3 h4 h5
h6 head header hr html i iframe img input ins kbd keygen label legend li link
main map mark menu menuitem meta meter nav noscript object ol optgroup option
output p param picture pre progress q rp rt ruby s samp script section select
small source span strong style sub summary sup table tbody td textarea tfoot th
thead time title tr track u ul var video wbr
```

### SVG элементы

Поддерживаются SVG элементы:

```
circle clipPath defs ellipse g line linearGradient mask path pattern polygon polyline
radialGradient rect stop svg text tspan
```

Также вам может быть интересен [react-art](https://github.com/facebook/react-art), это библиотека React для рисования, которая может быть отрендерина в Canvas, SVG, или VML (для IE8).


## Поддерживаемые аттрибуты

React поддерживает все `data-*` и `aria-*` аттрибуты, а также каждый атрибут из списка, указанного ниже.

> Примечания:
>
> Все аттрибуты записываются в верблюжьей нотации (camel-case). Аттрибуты `class` и `for` будут называться соответственно `className` и `htmlFor`, чтобы совпадало со спецификацией DOM API.

Для просмотра списка событий смотрите [Supported Events](/react/docs/events.html).

### HTML аттрибуты

Вот такие вот стандартные аттрибуты поддерживаются:

```
accept acceptCharset accessKey action allowFullScreen allowTransparency alt
async autoComplete autoFocus autoPlay capture cellPadding cellSpacing charSet
challenge checked classID className cols colSpan content contentEditable contextMenu
controls coords crossOrigin data dateTime defer dir disabled download draggable
encType form formAction formEncType formMethod formNoValidate formTarget frameBorder
headers height hidden high href hrefLang htmlFor httpEquiv icon id inputMode
keyParams keyType label lang list loop low manifest marginHeight marginWidth max
maxLength media mediaGroup method min minlength multiple muted name noValidate open
optimum pattern placeholder poster preload radioGroup readOnly rel required role
rows rowSpan sandbox scope scoped scrolling seamless selected shape size sizes
span spellCheck src srcDoc srcSet start step style summary tabIndex target title
type useMap value width wmode wrap
```

В дополнение, поддерживаются следующие нестандартизированные аттрибуты:

- `autoCapitalize autoCorrect` для Mobile Safari.
- `property` для [Open Graph](http://ogp.me/) мета тегов.
- `itemProp itemScope itemType itemRef itemID` для [HTML5 microdata](http://schema.org/docs/gs.html).
- `unselectable` для Internet Explorer.
- `results autoSave` для WebKit/Blink полей типа `search`.

Существуют также специфичные React аттрибуты `dangerouslySetInnerHTML` ([подробнее](/react/docs/special-non-dom-attributes.html)), они используются лля непосредственной вставки HTML в компонент.

### SVG Аттрибуты

```
clipPath cx cy d dx dy fill fillOpacity fontFamily
fontSize fx fy gradientTransform gradientUnits markerEnd
markerMid markerStart offset opacity patternContentUnits
patternUnits points preserveAspectRatio r rx ry spreadMethod
stopColor stopOpacity stroke  strokeDasharray strokeLinecap
strokeOpacity strokeWidth textAnchor transform version
viewBox x1 x2 x xlinkActuate xlinkArcrole xlinkHref xlinkRole
xlinkShow xlinkTitle xlinkType xmlBase xmlLang xmlSpace y1 y2 y
```
