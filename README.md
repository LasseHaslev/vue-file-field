# vue-image-upload

> Image uploader Vue style

## Install
``` bash
npm install @lassehaslev/vue-file-upload --save-dev
```

## Use
Javascript

``` js
    Vue.component( 'image-field', require( '@lassehaslev/vue-file-upload' ) );
```

HTML
``` html
    <image-field :multiple="true" accept="image/*" name="image"></image-field>
```

Styles can be found under src/styles/VueFileUploader.styl

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
