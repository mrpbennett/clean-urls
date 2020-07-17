# Clean Urls

[![Netlify Status](https://api.netlify.com/api/v1/badges/b4d0fe06-782c-47ef-8bce-8758b862f8dc/deploy-status)](https://app.netlify.com/sites/clean-urls/deploys)

![img for read me](https://github.com/mrpbennett/beautify-url/blob/master/src/assets/img.png?raw=true)

Are you tired of using excel to use find and replace https:// or http:// or even www. and sometimes anything from the trailing / at the end of the url?

Thats more than a few steps just to clean up a list of urls. What if you could paste a list of urls into a box, click a button and bingo! All the urls have been stripped down to their bear esstentials? Being an account manager in AdTech I have to sometimes clean up a list of domains for various reasons. It's a mega painful task as its rather repitive and sometimes excel or a human can make an error turning a albeit repitive but simple task into a nightmare.

Therefor I created Beautify URL.

A nice little tool to take the pain out of making domains beautiful again. This tool will take a url such as:

```
http://www.cultofmac.com/464645/apple-spaceship-campus-flyover/
```

And strip it back to its bare esstentials outputing it as `cultofmac.com` pretty cool eh?

The main tool of this site is a function that uses ReGex to strip back the url to what we need. This app is built in Vue.js with Vanilla Js for the functionality.

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
