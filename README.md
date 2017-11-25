# node --experimental-modules

Using node --experimental-modules does not respect "jsnext:main" or "module" inside the package.json file. I understand that node expects files to have the ".mjs" extension. The issue is that even if you rename the file, it won't work unless you also change the "main" attribute of the package.json file. If node --experimental-modules supported either "jsnext:main" or "module", authors could support both in the same install.


Steps to reproduce:

    $ npm install

    $ npm start
    
    > example-node-import@1.0.0 start /Users/jason/Documents/git/example-node-import
    > node --experimental-modules example.mjs
    
    (node:91689) ExperimentalWarning: The ESM module loader is experimental.
    SyntaxError: The requested module does not provide an export named 'Matrix4'
        at ModuleJob._instantiate (internal/loader/ModuleJob.js:84:17)
        at <anonymous>
    npm ERR! code ELIFECYCLE
    npm ERR! errno 1
    npm ERR! example-node-import@1.0.0 start: `node --experimental-modules example.mjs`
    npm ERR! Exit status 1
    npm ERR! 
    npm ERR! Failed at the example-node-import@1.0.0 start script.
    npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

    npm ERR! A complete log of this run can be found in:
    npm ERR!     /Users/jason/.npm/_logs/2017-11-25T23_03_07_081Z-debug.log


Steps to fix:

    $ npm run fix

    $ npm start
    
    > example-node-import@1.0.0 start /Users/jason/Documents/git/example-node-import
    > node --experimental-modules example.mjs
    
    (node:91814) ExperimentalWarning: The ESM module loader is experimental.
    Matrix4 {
      elements: [ 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1 ] }
