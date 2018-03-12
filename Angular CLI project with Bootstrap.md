 4.0## Add Bootstrap to an Angular CLI project

1. Creating an Angular project with Angular CLI

```console
ng new angular-bootstrap-example
```

2. Installing Bootstrap from NPM

```console
npm install bootstrap --save
```
or 4.0 release
```console
npm install bootstrap@next --save
```

3. Importing the CSS
```js
Configure .angular-cli.json:
"styles": [
  "../node_modules/bootstrap/dist/css/bootstrap.min.css",
  "styles.scss"
]
```
or src/style.css:
```js
@import './styles/bootstrap-3.3.7-dist/css/bootstrap.min.css';
```

4. Bootstrap JavaScript Components with ngx-bootstrap
```console
npm install bootstrap ngx-bootstrap --save
```

5. Adding the required Bootstrap modules in app.module.ts
