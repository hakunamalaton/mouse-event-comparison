# Introduction

This reposistory describes:
- What is `mouseenter`, what is `mouseover`?
- The differences between `mouseenter` and `mouseover`
- Which to use `mouseenter` or `mouseover`

## What is mouseenter and mouseover
From MDN:
> [mouseenter](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseenter_event) event is fired at an Element when a pointing device is initially moved so that its hotspot is within the element at which the event was fired.

> [mouseover](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseover_event) event is fired at an Element when a pointing device is used to move the cursor onto the element or one of its child elements

## The differences between `mouseenter` and `mouseover`
From [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseenter_event#usage_notes):
> Though similar to mouseover, mouseenter differs in that it doesn't bubble and it isn't sent to any descendants when the pointer is moved from one of its descendants' physical space to its own physical space.

There are two different points:
- Mouse enter does not bubble
- Mouse enter is not sent when the pointer is moved from one of its descendants' physical space to its own physical space

In this example, we are going to prove these two points above.

### Example
The app contains two blocks:
- The left block is registered with mouse enter event
- The right block is registered with mouse over event

Each block has three layers:
- The outest layer with title `Mouse enter block` or `Mouse over block`
- The `level 1` layer registers with mouse event
- The `level 2` layer registers with mouse event

![The mouse example structure](/src/assets/mouse-example.png)

#### Mouse enter does not bubble
Try moving the mouse with these step from `level 2` to `level 1` for each block, you could see:
The mouse enter block's console:
```
level 1
level 2
```
**Explanation**:
1. The mouse enters the block `level 1`, it triggers mouse enter event and logs `level 1` on the console
2. The mouse enters the block `level 2`, it triggers mouse enter event and logs `level 2` on the console

The mouse over block's console:
```
level 1
level 2
level 1
```
**Explanation**:
1. The mouse enters the block `level 1`, it triggers `mouseover` event and logs `level 1` on the console
2. The mouse enters the block `level 2`, it triggers `mouseover` event and logs `level 2` on the console
3. The `mouseover` event does the bubble up, it triggers mouse over event on `level 1` block and logs the `level 1` on the console

#### Mouse enter is not sent when moving from descendants to own space
Start from `level 1`, move the mouse to `level 2` for each block, you could see:
The mouse enter block's console:
```
<empty console>
```
**Explanation**:
1. The `mouseenter` event is not sent

The mouse over block's console:
```
level 1
```
**Explanation**:
1. The `mouseover` event is sent when moving from the descendant's physical space to its own physical space

### Which to use `mouseenter` or `mouseover`
From MDN:
> With deep hierarchies, the number of mouseover events sent can be quite huge and cause significant performance problems. In such cases, it is better to listen for mouseenter events.

