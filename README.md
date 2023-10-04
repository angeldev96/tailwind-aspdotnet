![dotnet + tailwind](https://github.com/angeldev96/tailwind-aspdotnet/blob/master/thumbnail.png)

# Steps to add Tailwind in ASP.NET 6 MVC Project:
## Video tutorial: https://youtu.be/HndP-Yh8WKc
## Requirements: 
- NodeJS
- .NET 6
- Terminal Emulator (Works with Powershell in Windows and bash or zsh in Linux)

## Step 1:
Create the project in Visual Studio or the dotnet CLI

## Step 2:
Start a node project
```sh
npm init -y
```

## Step 3:
Add Tailwind
```sh
npm install -D tailwindcss
```


## Step 4:
Add script to package.json for the css output location
```sh
"scripts": {
    "css:build": "npx tailwindcss -i ./wwwroot/css/site.css -o ./wwwroot/css/styles.css --minify"
  }
```

## Step 5:
Init the tailwind config file
```sh
npx tailwindcss init
```

## Step 6:
Add modules to tailwind.config.json, this is for tailwind to style razor pages:
```sh
module.exports = {
    content: [
       './Pages/**/*.cshtml',
       './Views/**/*.cshtml'
],
    theme: {
        extend: {},
    },
    plugins: [],
}
```

## Step 7:
Add input css to site.css in wwwroot/css
```sh
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Step 8:
Add itemgroups in the project under the .csproj file, this is for building the css before deploying:
```sh
<ItemGroup>
  <UpToDateCheckBuilt Include="wwwroot/css/site.css" Set="Css" />
  <UpToDateCheckBuilt Include="tailwind.config.js" Set="Css" />
</ItemGroup>

<Target Name="Tailwind" BeforeTargets="Build">
  <Exec Command="npm run css:build"/>
</Target>
```

## Step 9:
Include the path to the CSS file in the _Layout.cshtml file (Or the other views you need to style with tailwind)
```sh
<link rel="stylesheet" href="~/css/styles.css" asp-append-version="true" />
```

