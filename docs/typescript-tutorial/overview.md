---
id: intro
title: TypeScript Tutorial Overview
sidebar_label: Overview
hide_title: true
hide_sidebar: true
---

# TypeScript Tutorial Overview

Using TypeScript with RTK will dramatically improve your overall developer experience while making it painless to manage your global state. RTK is built with TypeScript and does a lot of heavy lifting to give you inference out of the box, and exports its types to make more advanced implementations possible.

Currently, we support TypeScript >= 3.5, however we recommend using the most recent version of TypeScript to ensure compatability with future releases.

This section will guide you through integrating and using TypeScript with RTK and showing the recommended configurations to prevent common issues that can arise. It will start with the basics, focusing on state only, and then gradually introduce each of the APIs (e.g. configureStore, createSlice, createAsyncThunk, createEntityAdapter, etc). At any point if you would like to get a deeper understanding, the API reference and [Usage with TypeScript](../usage/usage-with-typescript.md) sections go in depth over each topic and API.

We will be building a fully functional application along the way using CodeSandbox. Look out for the embedded sandbox at the end of each page.

## What this tutorial is not

This is not an in-depth guide that digs into the internals of any of the APIs, nor is it a full overview of Redux itself. You can use RTK without knowing the history and internals of Redux, but if this is your first time working with Redux or RTK, we do recommend that you read the [Redux Essentials Guide](https://redux.js.org/tutorials/essentials/part-1-overview-concepts) so that you can better understand the core concepts.
