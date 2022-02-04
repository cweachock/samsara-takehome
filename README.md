# Samsara Take-home assessment

## Overview 
I wanted to use the VueJS framework, which I currently use at North Face, and continuing to learn, so I set up a [vue cli hello world boiler plate](https://cli.vuejs.org/guide/creating-a-project.html#vue-create)
using [npm](https://www.npmjs.com/) locally on my computer, ingesting the data.json file and figured out how to create a specific component to handle the data, then followed a [short tutorial](https://dev.to/saigowthamr/how-to-deploy-a-vue-app-to-github-pages-1ia) on how to make it work with Github Pages. Using the [**v-for**](https://vuejs.org/v2/guide/list.html) directive we can render a list of items (in this case products and product information) from the **imported JSON** file to the project. So for each item in the data.json we specify the object key, in this case "groups", and use that to build our vue App. We can get the data using [**v-bind**](https://vuejs.org/v2/api/#v-bind) to bind the property as a DOM property for the component props in the [**productGridItem.vue**](https://github.com/cweachock/vue-practice/blob/master/src/components/productGridItem.vue) component. Also, I noticed there were some HTML encodings in the json file for things like "TM" or trade mark. For those, I used the [**v-html**](https://vuejs.org/v2/guide/syntax.html#Raw-HTML) to render the HTML encodings into the H1 product title. This component also contains it's own sass stylings to affect how the product grid item is displayed. 

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
