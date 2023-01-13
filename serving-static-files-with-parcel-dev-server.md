# Serving static files with Parcel's development server

You can serve static files with [Parcel](https://parceljs.org/)'s development server with the extra package `serve-static`:
```Bash
npm install --save-dev serve-static
```

Then we can use Parcel's proxy functionality by creating a `.proxyrc.js`:

```JavaScript
const path = require("path");
const serveStatic = require("serve-static");

const assetsPath = path.join(__dirname, "static");

module.exports = function (app) {
  app.use("/static", serveStatic(assetsPath));
};
```