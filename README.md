# v-dialog

> A simple and powful dialog, dialog type including Modal, Alert, Mask and Toast, based on Vue2.x

## Install

``` bash
# install dependencies
npm i v-dialog --save
```

Include plugin in your `main.js` file.

```js
import Vue from 'vue'
import vDialog from 'v-dialog';
...

Vue.use(vDialog);
```

## Use case

### Modal

```js
import myComponent from './myComponent';//import component you want to open in Modal dialog

new Vue({
  el: '#app',
  methods: {
    click(){
      //open component in Modal, and passing params to component
      this.$vDialog.modal(myComponent, {
        params: {
          a: 1,
          b: 2
        }
      });
    }
  }
});
```

receive params in component

```js
export default {
  name: 'myComponent',
  props: ['params']
  data(){
    console.log(this.params);//{a:1, b:2}
    return {};
  }
}
```

close dialog and return data in component

```js
export default {
  name: 'myComponent',
  props: ['params']
  data(){
    console.log(this.params);//{a:1, b:2}
    return {};
  },
  methods: {
    closeDialog(){
      let data = {
        a: 2,
        b: 4
      };
      //close current Modal dialog and return data to caller
      this.$vDialog.close(data);
    }
  }
}
```

### Alert

```js
//call a message alert dialog
this.$vDialog.alert('This is a <b>Vue</b> dialog plugin: vDialog!');

//call a message alert dialog with dialog close callback
this.$vDialog.alert('This is a <b>Vue</b> dialog plugin: vDialog!',function(){
  //your callback code
});

//call a custom type message alert dialog with dialog close callback
this.$vDialog.alert('This is a <b>Vue</b> dialog plugin: vDialog!',function(){
  //your callback code
},{
  messageType: 'error',
  closeTime: 2,// auto close alert dialog in 2 second,
  language: 'en'// i18n support 'cn', 'en', 'jp'
});
```

### Mask

```js
//open a full screen mask
this.$vDialog.mask();

//use custom message
this.$vDialog.mask('my data loading...');

//use mask with callback
this.$vDialog.mask('my data loading...', function(){
  // do something when mask close
});
```

some time, you can use mask link this:
```js
let that = this;
let dialogKey = this.$vDialog.mask();
// do some http request
axios.post(...).then(resp){
  // do your business
  that.$vDialog.close(null, dialogKey);
};
```


### Toast