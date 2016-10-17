# VueJS cascading address component

[![CircleCI](https://img.shields.io/circleci/project/savokiss/vue-cascading-address/master.svg)](https://circleci.com/gh/savokiss/vue-cascading-address)
[![npm version](https://img.shields.io/npm/v/vue-cascading-address.svg)](https://www.npmjs.com/package/vue-cascading-address)

## How it looks:
![](./static/demo.gif)

## Dependencies
- VueJS 2.0.1
- Bootstrap 3.3.6

## Usage

### INSTALLATION
```
npm install vue-cascading-address --save
```

### ES6
```
import cascadingAdress from 'vue-cascading-address'
export {
  components: {
    cascadingAddress
  },
  methods: {
    confirmCity(data){
      console.log(data);// { province: 'xxx' , city: 'xxx' , area: 'xxx' }
    }
  }
}
```

### HTML
```
  <cascading-address @confirm="confirmCity"></cascading-address>
```

## API

### Props
| name        | type    | required | description |
| ---------- | --------| -------- | ---------------- |
| inputClass | String  | false    | custom classes added to input like 'input-sm'|


### Events
| name       | attributes    | listen to | description |
| ---------- | --------| -------- | ---------------- |
| confirm    | (data)  | @confirm    | Emitted after `confirm` button, data structure: { province: String, city: String, area: String} |
