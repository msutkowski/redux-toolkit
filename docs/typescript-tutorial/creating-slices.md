---
id: creating-slices
title: Creating slices
sidebar_label: Creating slices
hide_title: true
---

# Creating slices

The majority of RTK users should use `createSlice` to encapsulate their logic. Under the hood, `createSlice` leverages a combination of `createAction`, `createReducer`, and adds in some special utilities.

Let's start by defining our `books` and `register` feature slices and refactoring our `store` to use them instead of the hand written reducers.

```ts
// features/books/booksSlice.ts

import { createSlice } from '@reduxjs/toolkit'

interface Book {
  id: number
  title: string
  description: string
  author: string
  status: 'available' | 'unavailable'
}

const initialState: Book[] = []

const slice = createSlice({
  name: 'books',
  initialState,
  reducers: {}
})

export default slice.reducer
```

```ts
// features/register/registerSlice.ts

import { createSlice } from '@reduxjs/toolkit'

interface Transaction {
  id: number
  created_at: string
  book_id: number
  action: 'checkout' | 'return'
}

const initialState: Transaction[] = []

const slice = createSlice({
  name: 'register',
  initialState,
  reducers: {}
})

export default slice.reducer
```

We'll update our store to use the new reducers that `createSlice` generated for us:

```diff
import { configureStore } from "@reduxjs/toolkit";
import { useDispatch, useSelector, TypedUseSelectorHook } from "react-redux";
+ import booksReducer from "./features/books/booksSlice";
+ import registerReducer from "./features/register/registerSlice";

-const store = configureStore({
-  reducer: { // RTK will call `combineReducers` on this object for us
-    books: (state: Book[] = [], action) => state,
-    register: (state: Transaction[] = [], action) => state
-  }
-});

+const store = configureStore({
+  reducer: {
+    books: booksReducer,
+    register: registerReducer
+  }
+});

// 👇 IMPORTANT: We need to get our RootState and resolved Dispatch types from the store.
export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch;

// 👇 IMPORTANT: We need to provide the types to the hooks from react-redux for use in components
export const useTypedDispatch = () => useDispatch<AppDispatch>();
export const useTypedSelector: TypedUseSelectorHook<RootState> = useSelector;

export default store;
```

## Reviewing our progress

   <iframe src="https://codesandbox.io/embed/rtk-typescript-tutorial-2-create-slices-0y0k3?fontsize=14&hidenavigation=1&theme=dark&file=/src/features/books/booksSlice.ts" style={{ width: '100%', height: '500px', border: 0, borderRadius: '4px', overflow: 'hidden' }} sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>
