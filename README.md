# Deno Reference Notes

Useage notes for deno.

## Events

Deno uses the same API as in the web browser, events are managed using `Event` or `CustomEvent` and `EventTarget`.

* [MDN: EventTarget](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget)
* [MDN: Event](https://developer.mozilla.org/en-US/docs/Web/API/Event)
* [MDN: CustomEvent (Supports Passing Data)](https://developer.mozilla.org/en-US/docs/Web/API/CustomEvent/CustomEvent)

_Note:_ The CustomEvent constructor requires an object with a detail attirbute as you can see below. Read more on the Mozilla documentation. 

Using `EventTarget` as a separate object:

```js
const et = new EventTarget()
et.addEventListener('this-event', (e) => {
  console.log('Event raised.', e)
})
et.dispatchEvent(new Event('this-event'))

```

Inheriting from `EventTarget`:

```js
class Car extends EventTarget {
  startEngine() {
    this.dispatchEvent(new Event('start-engine'));
  }
  revEngine() {
    const evt = new CustomEvent('rev-engine', { detail: { rpm: 2000 } });
    this.dispatchEvent(evt);
  }
}

const car = new Car();
car.addEventListener('start-engine', (e) => {
  console.log('Engine started and running...', e);
});
car.addEventListener('rev-engine', (e) => {
  console.dir(e)
  console.log('Engine revved - RPM:', e.detail.rpm);
});

car.startEngine();
car.revEngine();
```
## Reading JSON Files

Because `deno` can't import json files, you need to use the full path to the file and the `readJsonSync` and `path` standard modules.

```js
import { readJsonSync } from "https://deno.land/std/fs/mod.ts";
import * as path from "https://deno.land/std/path/mod.ts";
const pwd = path.fromFileUrl(path.dirname(import.meta.url));
const join = (p) => path.join(pwd, p);
const jsonSchema = readJsonSync(join("./schema.json"));
```
