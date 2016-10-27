npm i babel-loader babel-core --save-dev

It matches against both .js and .jsx using a regular expression (/\.jsx?$/).

```
const common = { 
  entry: { app: PATHS.app },
  // Add resolve.extensions. 
  // '' is needed to allow imports without an extension. 
  // Note the .'s before extensions as it will fail to match without!!! 
  resolve: { extensions: ['', '.js', '.jsx'] },
  output: { path: PATHS.build, filename: 'bundle.js' }, 
  module: {
    loaders: [ 
    {
      test: /\.css$/, 
      loaders: ['style', 'css'], 
      include: PATHS.app 
    }, 
    // Set up jsx. This accepts js too thanks to RegExp 
    {
    test: /\.jsx?$/, 
    // Enable caching for improved performance during development 
    // It uses default OS directory by default. If you need something 
    // more custom, pass a path to it. I.e., babel?cacheDirectory=<path> 
    loaders: ['babel?cacheDirectory'], 
    // Parse only app files! Without this it will go through entire project. 
    // In addition to being slow, that will most likely result in an error. 
    include: PATHS.app  
    }
] }
}; 
```