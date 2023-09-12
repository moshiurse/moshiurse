**First, install Vite and all React related libraries (here: Vite's React Plugin) as development dependencies:**

> npm install vite @vitejs/plugin-react --save-dev

**Create a vite.config.ts onn root path**

``` import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig(() => {
  return {
  // If issue arrises related cra use define
   define: {
      'process.env': {},
    },
    server: {
      open: true, //if you want browser open immediately
    },
    build: {
      outDir: 'build',
    },
    plugins: [react()],
  };
});
```

**Moving and updating your index.html**

Move public/index.html to root path.<br>
Remove all %PUBLIC_URL% occurrences in the index.html file.

``` 
mv public/index.html .
```

```
<link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
<link rel="icon" href="/favicon.ico" />
```

**Add script Tag in index.html**

```
<div id="root"></div>
<script type="module" src="/src/index.tsx"></script> // jsx if you use JS
```

**Uninstall CRA**

```
npm uninstall react-scripts
```

**update package.json**

```
"scripts": {
  "start": "vite",
  "build": "tsc && vite build",
  "serve": "vite preview"
},
```

**Update Typescript configs(update only following if you use ts)**
```
"target": "ESNext",
"lib": [
  "dom",
  "dom.iterable",
  "esnext"
],
"types": ["vite/client", "vite-plugin-svgr/client"]
 ```
