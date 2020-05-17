# Deno Reference Notes

Useage notes for deno.

## Events

Deno uses the same API as in the web browser, events are managed using `Event` and `EventTarget`.

* [MDN: EventTarget](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget)
* [MDN: Event](https://developer.mozilla.org/en-US/docs/Web/API/Event)

```js
const et = new EventTarget()
et.addEventListener('this-event', (e) => {
  console.log('Event raised.', e)
})
et.dispatchEvent(new Event('this-event'))

```

```js
class Car extends EventTarget {
  startEngine() {
    this.dispatchEvent(new Event('start-engine'));
  }
}

const car = new Car();
car.addEventListener('start-engine', (e) => {
  console.log('Engine started and running...', e);
});
car.startEngine();
```
