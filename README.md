# Angular Template
You will need to install node (and node package manager). 

You can install node here: https://nodejs.org/en/download/

There is also a great tool called 'node version manager' that is very useful in development to switch between node versions for different projects. You can find that:
https://github.com/nvm-sh/nvm

Make sure to navigate to the root directory and run 
```npm install```
This will install all the dependencies of node modules that will be needed to run your application.
    
## Running the app in development

To run the application with webpack for local development (http://localhost:4300), run the following command 

```
ng serve app
```

# Creating library components in the application
To create a component, you will first need to navigate to the correct directory where you want the package to be located. Then you will use angular to generate the library files. The following command will create a library that you can use in the application

```
ng generate library component-name --entry-file=public-api
```
This will create a number of files.
```
CREATE libs/components/component-name/.browserslistrc (600 bytes)
CREATE libs/components/component-name/karma.conf.js (1438 bytes)
CREATE libs/components/component-name/ng-package.json (169 bytes)
CREATE libs/components/component-name/package.json (193 bytes)
CREATE libs/components/component-name/README.md (1042 bytes)
CREATE libs/components/component-name/tsconfig.lib.json (339 bytes)
CREATE libs/components/component-name/tsconfig.lib.prod.json (240 bytes)
CREATE libs/components/component-name/tsconfig.spec.json (315 bytes)
CREATE libs/components/component-name/src/test.ts (763 bytes)
CREATE libs/components/component-name/src/public-api.ts (187 bytes)
CREATE libs/components/component-name/src/lib/component-name.module.ts (278 bytes)
CREATE libs/components/component-name/src/lib/component-name.component.spec.ts (676 bytes)
CREATE libs/components/component-name/src/lib/component-name.component.ts (288 bytes)
CREATE libs/components/component-name/src/lib/component-name.service.spec.ts (393 bytes)
CREATE libs/components/component-name/src/lib/component-name.service.ts (142 bytes)
UPDATE angular.json (9800 bytes)
UPDATE tsconfig.json (1560 bytes)
```

After generating the library, you will also need to edit the package.json in your library. Set the "name" to what you want to be able to import the package as. This will allow any library or component to be able to import something from your newly created library.

```
{
  "name": "@itt-components/${component-name}",
  "version": "0.0.1",
  "peerDependencies": {
    "@angular/common": "^13.2.0",
    "@angular/core": "^13.2.0"
  },
  "dependencies": {
    "tslib": "^2.3.0"
  }
}
```
You will also need to go to the base tsconfig.json at the root of the project and add your component to the paths section.

```
"@itt-components/component-name": [
  "libs/components/component-name/src/public-api.ts"
],
```

Make all the changes and additions to the newly created component. Then to add it to the project, make the necessary changes to the routing config in app-routing.module.ts of the project you want to access it in. (In this case it will be app)

```typescript
const routes: Routes = [
  {
    path: '${DesiredPathForComponent}',
    component: ${ComponentName}
  }
];
```

Now if you go to your localhost:4300 instance, your component will be accessible at the route you specified in the app-routing.module.ts
You can also edit your main project HTML to have a link to the route you just added above.
