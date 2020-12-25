#useGestures

A React hook for mobile gestures handling

## Params

- [ref](https://reactjs.org/docs/hooks-reference.html#useref): A react useRef object
- handlers: An object of event handlers
- options: An object of option settings

### handlers

#### Pan events

Are equal to native touch events. All other event types will trigger an equivalent pan event

- onPanStart
- onPanMove
- onPanEnd

#### Swipe events

Are pan events with a direction distance larger than options[minDelta] value

- onSwipeLeft
- onSwipeRight
- onSwipeUp
- onSwipeDown
- onSwipeLeftEnd
- onSwipeRightEnd
- onSwipeUpEnd
- onSwipeDownEnd

#### Pinch events

Are two fingers pan events.

- onPinchStart
- onPinchChanged
- onPinchEnd

### Pan / Swipe event object

```
{
  preventDefault: function,
  stopPropagation: function,
  x: number,
  y: number
  deltaX: number,
  deltaY: number,
  delta: number,
  distance: number,
  angleDeg: number,
}
```

### Pinch event object

```
{
  preventDefault: function,
  stopPropagation: function,
  pointers: [{x: number, y: number}],
  delta: number,
  scale: number,
  distance: number,
  angleDeg: number
}
```

### Usage and Demos

Here is a full [demo site](https://giladl82.github.io/use-gestures-app/) with code examples. It is best to watch in on a mobile device

Here is a quick code example

```js
export default function App() {
  const [scale, setImageScale] = useState(1);
  const [rotation, setImageRotation] = useState(0);
  const image = useRef(null);

  useGestures(image, {
    onPinchStart: event => {},
    onPinchChanged: event => {
      setImageScale(event.scale);
      setImageRotation(event.angleDeg);
    },
    onPinchEnd: event => {
      setImageScale(1);
      setImageRotation(0);
    }
  });

  return (
    <img
      ref={image}
      src={logo}
      alt="React Logo"
      className="logo"
      style={{
        transform: 'rotate(' + rotation + 'deg) scale(' + scale + ')'
      }}
    />
  );
}
```
