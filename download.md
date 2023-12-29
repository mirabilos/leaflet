---
layout: v2
title: Download
bodyclass: download-page
---

## Download Leaflet

(removed, since this repository only documents the v0.7.x used by MirKarte)

### Using a Downloaded Version of Leaflet

Inside the archives downloaded from the above links, you will see four things:

- `leaflet.js` - This is the minified Leaflet JavaScript code.
- `leaflet-src.js` - This is the readable, unminified Leaflet JavaScript, which is sometimes helpful for debugging.
- `leaflet.css` - This is the stylesheet for Leaflet.
- `images` - This is a folder that contains images referenced by `leaflet.css`. It must be in the same directory as `leaflet.css`.

Unzip the downloaded archive to your website's directory and add this to the `head` of your HTML code:

    <link rel="stylesheet" href="/path/to/leaflet.css" />
    <script src="/path/to/leaflet.js"></script> <!-- or use leaflet-src.js --!>

### Leaflet Source Code

These download packages above only contain the library itself.
If you want to download the full source code, including unit tests, files for debugging, build scripts, etc.,
you can <a href="https://github.com/Leaflet/Leaflet/releases">download it</a>
from the <a href="https://github.com/Leaflet/Leaflet">GitHub repository</a>.

### Building Leaflet from the Source

Leaflet build system is powered by the [Node.js](http://nodejs.org) platform,
which installs easily and works well across all major platforms.
Here are the steps to set it up:

 1. [Download and install Node](http://nodejs.org)
 2. Run the following commands in the command line:

 <pre><code>npm install -g jake
npm install</code></pre>

Now that you have everything installed, run `jake build` inside the Leaflet directory.
This will combine and compress the Leaflet source files, saving the build to the `dist` folder.

### Building a Custom Version of Leaflet

To make a custom build of the library with only the things you need,
open `build/build.html` page of the Leaflet source code contents, choose the components
(it figures out dependencies for you) and then run the command generated with it.
