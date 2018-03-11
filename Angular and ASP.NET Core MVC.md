
# Angular and ASP.NET Core MVC

 Use @angular/cli package in conjunction with the .NET tools for creating a new MVC project

## A. Preparing to Create a Project 
To create a project that combines Angular and ASP.NET Core MVC, I start with @angular/cli and access he underlying webpack configuration, which can then be used to integrate the Angular tools and libraries into the ASP.NET Core project.
To start this process, open a new command prompt and run the command:
```console
 npm install --global @angular/cli 
 ```

## B. Creating the Project

### Creating the Angular Part of the Project

 1. Open a new command prompt, navigate to the folder where you keep your development projects, and run the command:
    ```console 
    ng new SportsStore --skip-git --skip-commit --skip-tests --source-dir ClientApp 
    ```

 2. The ng command is provided by the @angular/cli package, and ng new creates a new Angular project. The arguments that start with ``--skip`` tell @angular/cli not to perform some of the standard setup steps that are usually included in projects, and the ``--source-dir`` argument specifies the name of the folder that will contain the source code for the Angular application. The Angular code lives in a folder called ClientApp in projects that combine Angular and ASP.NET Core MVC.

    The command creates a folder called SportsStore that contains the tools and configuration files for an Angular project, along with some placeholder code so that the tools and project structure can be tested.

The rest of the setup is performed inside the project folder, so run the command ``cd SportsStore``to change the working directory.

3. Getting the Angular tools to work with the .NET tools requires additional NPM packages. Run the command to install these packages 
    ```console
    npm install --save-dev webpack@4.1.1 aspnet-prerendering@3.0.1 aspnet-webpack@2.0.3 webpack-hot-middleware@2.21.2 
    ```
 

4. These NPM packages are used to set up and run the Angular development tools inside the ASP.NET Core runtime. These packages work directly with webpack, which is usually hidden when working with projects created using @angular/cli. Run the command ``ng eject`` in the SportsStore folder to create a webpack configuration file that can be used to build and  run the project, a process known as ejecting the project from @angular/cli. 

5. The ejection process updates the package.json file, which NPM uses to keep track of the packages used by the project. In some cases, the ejection process will add additional NPM packages to the project.json file, so run the command `` npm install `` to ensure that any new packages are downloaded and installed. 

### Creating the ASP.NET Core MVC Part of the Project 

1. Run the command in the SportsStore folder to create a basic MVC project 
    ```console
    dotnet new mvc --language C# --auth None --framework netcoreapp2.0
    ```


2. This NuGet package is the .NET counterpart to the NPM packages and is used to integrate the Angular tools into Visual Studio. run command to adding a NuGet Package to the Project 
    ```console
    dotnet add package Microsoft.AspNetCore.SpaServices --version 2.0.2
    ```

3. If the application data will be stored using Microsoft SQL Server and accessed using Entity Framework Core. Run the commands in the SportsStore folder to add the NuGet packages required to add these features to the application
    ```console
    dotnet add package Microsoft.EntityFrameworkCore --version 2.0.1 
    dotnet add package Microsoft.EntityFrameworkCore.Design --version 2.0.1 
    dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 2.0.1
    ``` 

 4. Adding NuGet Packages in the SportsStore.csproj File in the SportsStore Folder

    ```csharp
    <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools"  Version="2.0.0" /> ''
    <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet"  Version="2.0.1" />
    ```
5. To Download new packages with a command prompt, run the command `` dotnet restore `` 

## C. Configuring the Project 

Now that the project foundation is in place, it is time to configure the different parts of the application to work together

1. Creating and Editing the Configuration Files. Add a TypeScript file called boot.ts to the SportsStore/ClientApp folder, with the code below:

    ```csharp
    import { enableProdMode } from "@angular/core"; 
    import { platformBrowserDynamic } from "@angular/platform-browser-dynamic"; 
    import { AppModule } from "./app/app.module";
    const bootApplication = () => { 
        platformBrowserDynamic().bootstrapModule(AppModule); 
    };
    if (module["hot"]) {
        module["hot"].accept();
        module["hot"].dispose(() => {
            const oldRootElem = document.querySelector("app-root");
            const newRootElem = document.createElement("app-root");
            oldRootElem.parentNode.insertBefore(newRootElem, oldRootElem);
            platformBrowserDynamic().destroy();
        });
    }
    if (document.readyState === "complete") {
        bootApplication();
    } else {
        document.addEventListener("DOMContentLoaded", bootApplication); 
    }
    ```

    This file is responsible for loading the Angular application and responding to changes to the client-side code.

2. Edit the Startup.cs file to change the code in the Configure method. The additions enable the integration between the ASP.NET Core and Angular development tools.
    ```csharp
        using Microsoft.AspNetCore.SpaServices.Webpack;
        ...
        ...
        app.UseDeveloperExceptionPage();
        app.UseWebpackDevMiddleware(new WebpackDevMiddlewareOptions {
            HotModuleReplacement = true
        });
        //if (env.IsDevelopment()) {
        //  app.UseDeveloperExceptionPage();
        //  app.UseBrowserLink();
        //} else {
        //  app.UseExceptionHandler("/Home/Error");
        //}
    ```
3. Open the webpack.config.js file in the SportsStore folder, locate the module.exports statement, and make the changes in bold.  
    ```csharp
    "entry": {    "main": [        "./ClientApp\\boot.ts"    ],
    ```

4.  Open the webpack.config.js file in the SportsStore folder, locate "output" add the following:

    ```csharp
    "path": path.join(process.cwd(), "wwwroot/dist"),
    "publicPath": "/app/"
    ```
 
## D. Enabling Logging Messages 

Enabling Logging in the appsettings.json File in the SportsStore Folder
    ```csharp
    "Microsoft.EntityFrameworkCore": "Information",      "Microsoft.AspNetCore.NodeServices": "Information", 
    ```

## E. Updating the Bootstrap Package 
 If use the Bootstrap CSS package to style the HTML elements displayed by the browser.

## F. Updating the Controller, Layout, and View 

The final step in setting up the project is to update the controller and the Razor layout and view to replace the placeholder content and incorporate the Angular application. Edit the Home controller and replace the contents with the code shown in Listing 3-18.

1. Replacing Content in the HomeController.cs File in the Controllers Folder
```csharp
using Microsoft.AspNetCore.Mvc;
namespace SportsStore.Controllers {    
    public class HomeController : Controller {
    public IActionResult Index() {
        return View();
        }    
    }
}
```


2. Replacing Content in the Index.cshtml File in the Views/Home Folder
<div class="p-1">  <app-root></app-root> </div>

The script elements in this view include bundles of JavaScript files that contain the Angular framework and the client-side application code. These bundles will be created automatically by webpack when the files in the Angular part of the project change. The app-root element will be replaced with dynamic content produced by the Angular application, as you will see in the next section. The other elements are standard HTML that has been styled with Bootstrap.

## G. Running the Project 

If you are using Visual Studio Code, then use a command window to run the command `` dotnet run `` in the SportsStore folder, which will build the project and start the ASP.NET Core HTTP server.  

--

The Angular development tools and ASP.NET Core are now working together. Edit the app.component.ts file in the SportsStore/ClientApp/app folder and  make the change highlighted in Listing 3-22. (You will have to expand the app.component.html file to see the app.component.ts file in the Solution Explorer if you are using Visual Studio, which nests related files together.)
