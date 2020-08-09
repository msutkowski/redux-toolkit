---
id: configure-the-store
title: Configure the store
sidebar_label: Configure the store
hide_title: true
---

# Configure the store

The base of a good TypeScript integration with RTK revolves around the store configuration. When your store is typed correctly, you'll have a great experience with most additional middleware(s), and most importantly, fully typed hooks.

For this tutorial we will create a simple application consisting of two feature slices: books and a transaction register.

## Defining interfaces

Let's start by defining the interfaces we'll use for our application

```ts
interface Book {
  id: number
  title: string
  description: string
  author: string
  status: 'available' | 'unavailable'
}

interface Transaction {
  id: number
  created_at: string
  book_id: number
  action: 'checkout' | 'return'
}
```

## Creating the store

```ts
import { configureStore } from '@reduxjs/toolkit'
import { useDispatch, useSelector, TypedUseSelectorHook } from 'react-redux'

interface Book {
  id: number
  title: string
  description: string
  author: string
  status: 'available' | 'unavailable'
}

interface Transaction {
  id: number
  created_at: string
  book_id: number
  action: 'checkout' | 'return'
}

// We're going to configure the store with a `root reducer` consisting of `books` and `register`.
const store = configureStore({
  reducer: {
    // RTK will call `combineReducers` on this object for us
    books: (state: Book[] = [], action) => state,
    register: (state: Transaction[] = [], action) => state
  }
})

// 👇 IMPORTANT: We need to get our RootState and resolved Dispatch types from the store
export type RootState = ReturnType<typeof store.getState>
export type AppDispatch = typeof store.dispatch

// 👇 IMPORTANT: We need to provide the types to the hooks from react-redux for use in components
export const useTypedDispatch = () => useDispatch<AppDispatch>()
export const useTypedSelector: TypedUseSelectorHook<RootState> = useSelector

export default store
```

Now that we have the basic store configured, let's check the typings. At this point, you'll see the `store.getState` will allow us to access `books` and `register`, while `store.dispatch` will have the typings for the default thunk middleware that RTK provides.

![Code screenshot showing type resolution](/assets/tutorials/typescript/typescript-tutorial-1-getstate-resolved.png)

## Reviewing our progress

You can view the progress of our application in [CodeSandbox](https://codesandbox.io/s/rtk-typescript-tutorial-1-configure-store-43lqm?file=/src/store.ts).
