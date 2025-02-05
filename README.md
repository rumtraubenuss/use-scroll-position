# `use-scroll-position`

[![Node version](https://img.shields.io/npm/v/@n8tb1t/use-scroll-position.svg?style=flat)](https://www.npmjs.com/package/@n8tb1t/use-scroll-position)
[![Node version](https://img.shields.io/librariesio/github/n8tb1t/use-scroll-position.svg?style=flat)](https://libraries.io/npm/@n8tb1t%2Fuse-scroll-position)
[![Node version](https://img.shields.io/github/license/n8tb1t/use-scroll-position.svg?style=flat)](https://github.com/n8tb1t/use-scroll-position/blob/master/LICENSE)

![Screenshot](https://github.com/n8tb1t/use-scroll-position/raw/master/examples/screenshot.png)

`use-scroll-position` is a React [hook](https://reactjs.org/docs/hooks-reference.html) that returns the browser viewport X and Y scroll position. It is highly optimized and using the special technics to avoid unnecessary rerenders!

> It uses the default react hooks rendering lifecycle, which allows you to fully control its behavior and prevent unnecessary renders.

## Demo

- [Hide navbar on scroll](https://n8tb1t.github.io/use-scroll-position/navbar/navbar)
- [Hide/Show sidebar on scroll](https://n8tb1t.github.io/use-scroll-position/navbar/sidebar)
- [Display viewport scroll position](https://n8tb1t.github.io/use-scroll-position/navbar/position)

[![Edit use-scroll-position](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/use-scroll-position-8nfin?fontsize=14)

## Install
```
yarn add @n8tb1t/use-scroll-position
```

## Usage

```jsx
useScrollPosition(effect,deps, element, useWindow, wait)
```

| Arguments | Description |
| --------- | ----------- |
`effect`    | Effect callback.
`deps`      | For effects  to fire on selected dependencies change.
`element`      | Get scroll position for a specified element by reference.
`useWindow`      | Use `window.scroll` instead of `document.body.getBoundingClientRect()` to detect scroll position.
`wait`      | The `timeout` in ms. Good for performance.

> The `useScrollPosition` returns `prevPos` and `currPos`.

## Examples

**Log current scroll position**
```jsx
import { useScrollPosition } from '@n8tb1t/use-scroll-position'
  
useScrollPosition(({ prevPos, currPos }) => {
  console.log(currPos.x)
  console.log(currPos.y)
})
```

**Change state based on scroll position**
```jsx
import React, { useState } from 'react'
import { useScrollPosition } from '@n8tb1t/use-scroll-position'

const [hideOnScroll, setHideOnScroll] = useState(true)
  
useScrollPosition(({ prevPos, currPos }) => {
  const isShow = currPos.y > prevPos.y
  if (isShow !== hideOnScroll) setHideOnScroll(isShow)
}, [hideOnScroll])
```
**Get scroll position for custom element**
```jsx
  const [elementPosition, setElementPosition] = useState({ x: 20, y: 150 })
  const elementRef = useRef()
  
    // Element scroll position
  useScrollPosition(
    ({ currPos }) => {
      setElementPosition(currPos)
    }, [], elementRef
  )
```

## Why to use
`use-scroll-position` returns the scroll position of the browser window, using a modern, stable and performant implementation.

Most of the time scroll listeners do very expensive work, such as querying dom elements, reading height / width and so on.
`use-scroll-position` solves this by using [`throttling`](https://stackoverflow.com/a/44779316) technic to avoid too many reflows (the browser to recalculate everything).