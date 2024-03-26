# MobX base controller

MobX controller for state and/or data in your stores

## Table of contents
1. [Basic usage](#basic-usage)
2. [Use store without custom hook](#use-store-without-custom-hook)
3. [Use only one type of controller](#use-only-one-type-of-controller)
4. [License](#license)

## Basic usage

First, create your store that extends base controller class

```ts
// my-store.ts
import { BaseController } from "@kurai-io/base-controller"
import { makeObservable } from "mobx"

interface State {
  myState: string
  optional?: string
}

interface Data {
  myData: string
}

export default class MyStore extends BaseController<State, Data> {
  constructor() {
    super({
      myState: "value"
    }, {
      myData: "value"
    })

    makeObservable(this)
  }
}
```

Then use your store in some other place

```ts
import { useStore } from "@kurai-io/mobx-base-controller"
import MyStore from "./my-store"

const myStore = useStore(MyStore)

// Set multiple states at once
myStore.setState({ optional: "value" })

// Set single state
myStore.setState("optional", "value")

myStore.state.optional // Get state data

// Same methods used for working with store data

myStore.setData({ myData: "value" })
```

## Use store without custom hook

If you prefer not to use `useStore` hook, you can
make your own way to use store. As example, you can
just create instance of class and then import it where it needed

```ts
// ... my-store.ts file contents

class MyStore extends BaseController<State, Data> {
  // ...
}

const myStore = new MyStore()

export default myStore

```

## Use only one type of controller

If you prefer not to use data and state at same time, you
can just use `StateController` or `DataController`

```ts
// my-state-store.ts

import { StateController } from "@kurai-io/base-controller"
import { makeObservable } from "mobx"

interface State {
  myState: string
  optional?: string
}

// Or DataController if you prefer to use data instead of state
export default class MyStore extends StateController<State> {
  constructor() {
    super({
      myState: "value"
    })

    makeObservable(this)
  }
}
```

Usage will be the same as for `BaseController`, but you
will be able to interact only with one type of state

## License

You can copy and paste the MIT license summary from below.

```text
MIT License

Copyright (c) 2022-2024 Kurai Foundation

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```

This package was originally designed for [SafeBlock](https://safeblock.com) products
