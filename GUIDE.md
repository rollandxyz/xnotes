
# How to creaet library

https://blog.angularindepth.com/creating-a-library-in-angular-6-87799552e7e5


## Creating an Angular Workspace and Library

```bash
ng-mat-redux-wspace
ng generate library xluo-ng6-demo-lib --prefix=xluo
ng build --prod xluo-ng6-demo-lib
```

## Using the Library in Our Application

```js
import { XluoNg6DemoLibModule } from 'xluo-ng6-demo-lib';
```

import the module in the application using the library by name.
Add the `XluoNg6DemoLibModule` to the imports array.
when importing a library by name, the Angular CLI looks first in the `tsconfig.json` paths and then in `node_modules`.


## Expanding the Library
- Generate a new component in our library.

    ```bash
    ng generate component /Components/simple-table --project=xluo-ng6-demo-lib
    ```

- Add the component to our library module’s exports array in the `xluo-ng6-demo-lib.module.ts`

- Add the component to our entry file `public_api.ts`.
- Rebuild our library after we make changes to it.

    ```bash
    ng build --prod xluo-ng6-demo-lib
    ```
- Use the new component in our application. 
add the element <xluo-simple-table></xluo-simple-table> as the last line of your `app.component.html` file
- run app with 
    ```bash
    ng serve --open
    ```


# Best practices

ALWAYS: Create your workspace using the name of your library-app. Then rename it to the name of your library.
ALWAYS: Use a prefix when generating a library. ng-packagr dependency in package.json
ALWAYS: Use the `--prod` flag when building your library.
Using the prod flag will make sure that we catch Angular Ahead-of-Time (AOT) errors early while they are still easy to find and fix.
ALWAYS: In your test application import using your library by name and NOT the individual files.
FOR COMPONENTS:
Using export makes the element visible.
Adding it to the entry file makes the class visible.

## How to rename workspace

To create an Angular workspace named ng-mat-redux-wspace. We need to create a workspace named ng-mat-redux-wspace-app and then rename it to ng-mat-redux-wspace:

`ng new` example-ng6-lib-app
`rename` example-ng6-lib-app example-ng6-lib
`cd` example-ng6-lib
`ng serve`

```js
ng new ng-mat-redux-wspace
ng rename 
```