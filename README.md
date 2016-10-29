# vue-file-field

> File field Vue style

## Install
``` bash
npm install @lassehaslev/vue-file-field --save-dev
```

## Use
Javascript

``` js
    Vue.component( 'file-field', require( '@lassehaslev/vue-file-field' ) );
```

HTML
``` html
    <file-field :multiple="true" accept="image/*" name="file"></file-field>
```

Styles can be found under src/styles/VueFileField.styl

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
