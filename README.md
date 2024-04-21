# Introduction

This reposistory describes:
- What are `mouseenter` versus `mouseover`, `mouseleave` versus `mouseout`?
- The differences between `mouseenter` and `mouseover`
- The differences between `mouseleave` and `mouseout`
- Best practice

## What are mouseenter and mouseover?
From MDN:
> [mouseenter](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseenter_event) event is fired at an Element when a pointing device is initially moved so that its hotspot is within the element at which the event was fired.

> [mouseover](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseover_event) event is fired at an Element when a pointing device is used to move the cursor onto the element or one of its child elements

## The differences between `mouseenter` and `mouseover`
From [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseenter_event#usage_notes):
> Though similar to `mouseover`, `mouseenter` differs in that it doesn't bubble and it isn't sent to any descendants when the pointer is moved from one of its descendants' physical space to its own physical space.

From this quote, there are two main points:
- `mouseenter` does not bubble
- `mouseenter` is not sent when the pointer is moved from one of its descendants' physical space to its own physical space

## What are mouseleave and mouseout?
From MDN:
> [mouseleave](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseleave_event) is fired at an Element when the cursor of a pointing device (usually a mouse) is moved out of it.

> [mouseout](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseout_event) event is fired at an Element when a pointing device (usually a mouse) is used to move the cursor so that it is no longer contained within the element or one of its children.

> `mouseout` is also delivered to an element if the cursor enters a child element, because the child element obscures the visible area of the element.

## The differences between `mouseleave` and `mouseout`
From [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseleave_event):
> `mouseleave` and `mouseout` are similar but differ in that `mouseleave` does not **bubble** and mouseout does. This means that `mouseleave` is fired when the pointer has exited the element and all of its descendants, whereas mouseout is fired when the pointer leaves the element or leaves one of the element's descendants (even if the pointer is still within the element).

There is one main point: `mouseleave` does not bubble.

### Example
This example shows the different from MDN's points. 
The app contains four blocks, each block registers with 4 mouse events: `mouseenter`, `mouseover`, `mouseleave`, and `mouseout`.

Each block has three layers:
- The outer layer with the title such as `Mouse enter block`
- The `level 1` element is the parent element of the `level 2` element. Two these elements both register the same mouse event.

![The mouse example structure](/src/assets/mouse-example.png)

#### mouseenter does not bubble
Try moving the mouse from `level 1` into `level 2` block. The console looks like this:
```
level 1
level 2
```

While in the `mouseover` case:
```
level 1
level 2
level 1
```
**Explanation**:
- `mouseenter`:
  - The mouse enters the block `level 1`, it triggers `mouseenter` event and logs `level 1` on the console
  - The mouse enters the block `level 2`, it triggers `mouseenter` event and logs `level 2` on the console
- `mouseover`
  - The mouse enters the block `level 1`, it triggers `mouseover` event and logs `level 1` on the console
  - The mouse enters the block `level 2`, it triggers `mouseover` event and logs `level 2` on the console
  - The `mouseover` event does the bubble up, it triggers `mouseover` event on `level 1` block and logs the `level 1` on the console

#### mouseenter is not sent when moving from descendants to own space
Start from `level 1`, and move the mouse to `level 2` for each block, you can see:
The `mouseenter` console looks like this:
```
<empty console>
```

While `mouseover` console looks like this:
```
level 1
```
**Explanation**:
- `mouseenter`:
  - The `mouseenter` event is not sent
- `mouseover`:
  - The `mouseover` event is sent when moving from the descendant's physical space to its own physical space

#### mouseleave does not bubble
1. Move the pointer from the `level 1` block into the `level 2` block
2. Move the pointer from the `level 2` block out to the `level 1` block

The `mouseleave` console looks like this:
```
level 2
level 1
```
While the `mouseout` console looks like this:
```
level 1
level 2
level 1
level 1
```
**Explanation**:
- `mouseleave`:
  - The pointer leaves the `level 2` block then leaves the `level 1` block
- `mouseover`:
  - The pointer enters the `level 2` block, it triggers `mouseout` for `level 1` block (since `level 2` block obscures the `level 1` block) -> log `level 1`
  - The pointer leaves the `level 2` block, it triggers `mouseout` for `level 2` block -> log `level 2`
  - The `mouseout` event bubbles up to the `level 1` block -> log `level 1`
  - The pointer leaves the `level 1` block -> log `level 1`

### Best practice
From MDN:
> With deep hierarchies, the number of mouseover events sent can be quite huge and cause significant performance problems. In such cases, it is better to listen for mouseenter events.

You can use `mouseenter` combined with `mouseleave` events. The `mouseover` event and `mouseout` have bubble behavior which can
- Affect the performance if the DOM structure is deep
- Cause the unexpected behaviors

