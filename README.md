# Vue Composition API

- [Vue Composition API](#vue-composition-api)
  - [Deployment](#deployment)
  - [Description](#description)
  - [Composition API Details](#composition-api-details)

## Deployment

- Checkout deployment at <https://gagandeep39.github.io/vue-composition-api-demo/>

## Description

- There are 2 ways of writing vue components
  - Options API (Traditional)
  - Compositions API

## Composition API Details

- Alternative way of writing Vue Logic
- Used for Larger Apps
- Main problem with large apps: Too much data and UI code in large apps
- In options API, lot of similar code that should belong together is split across dofferent parts such as watcher, methods, computed etc.
- Composition API allows reusing logic
- Basically merging `data()`, `methods`, `computed`, `watch` into `setup()`
