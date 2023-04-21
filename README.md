# EJS_MS_Teams

ElectronJS Wrapper for MS Teams

* Note this EJS version does not work on the MS Teams site for me. Try the WebView2 version which does work.

## See Also

[WV2_MSTeamsBrowser](https://github.com/tgraupmann/WV2_MSTeamsBrowser) - WebView2 wrapper for MS Teams

## Resources

[Electron Forge - Getting Started](https://www.electronforge.io/)

## Dependencies

* Install [NodeJS](https://nodejs.org/)

Yarn

```cli
npm install --global yarn
```

## Setup

Create the EJS Forge Project.

```cli
npm init electron-app@latest EJS_MS_Teams
CD EJS_MS_Teams
```

Change the start url in [src/index.html](src/index.html)

```html
<!DOCTYPE html>
<html>
  <head>
  <script>
    window.location = 'https://teams.microsoft.com/';
  </script>
  </head>
</html>
```

Update window defaults in [src/index.js](src/index.js) to change the default window size, maximize, and disable opening the default dev tools

```js
// run full speed in background
app.commandLine.appendSwitch("disable-background-timer-throttling");

const createWindow = () => {
  // Create the browser window.
  const mainWindow = new BrowserWindow({
    width: 1280,
    height: 720,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js'),
    },
  });

  // and load the index.html of the app.
  mainWindow.loadFile(path.join(__dirname, 'index.html'));

  // Open the DevTools.
  // mainWindow.webContents.openDevTools();

  // maximize the window
  mainWindow.maximize();
  mainWindow.show();
};
```

Start the app to verify the application works

```cli
cd EJS_MS_Teams
npm start
```

Build the standalone application

```cli
npm run make
```

Application outputs to `out\ejs-ms-teams-win32-x64\ejs-ms-teams.exe`

Build the installer

```cli
npm run publish
```

Installer outputs to `out\make\squirrel.windows\x64\ejs-ms-teams-1.0.0 Setup.exe`
