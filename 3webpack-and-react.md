### babel

https://babeljs.io/docs/usage/options/

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
#### Setting Up .babelrc
relying ES2015 and React presets:

`npm i babel-preset-es2015 babel-preset-react --save-dev`

babel-plugin-transform-object-assign

babel-plugin-array-includes

The former allows us to use Object.assign while the latter provides Array.includes without having to worry about shimming these for older environments.

npm i babel-preset-survivejs-kanban --save-dev

{ "presets": ["es2015", "react", "survivejs-kanban"] }

作者搞事，自定义个[preset](
https://github.com/survivejs/babel-preset-survivejs-kanban/blob/master/package.json)
教你学会如何定义自己的Presets

**两种loader申明方式**
```
{ 
  test: /\.jsx?$/, 
  loaders: ['babel?cacheDirectory,presets[]=react,presets[]=es2015,presets[]=survivejs-k\ anban'],
  include: PATHS.app 
}
```
Given passing a query string like this isn’t particularly readable, another way is to use the combination of loader and query fields:
```
{ 
  test: /\.jsx?$/, 
  loader: 'babel', 
  query: {
    cacheDirectory: true,
    presets: ['react', 'es2015', 'survivejs-kanban'] 
  },
  include: PATHS.app 
}
```
Webpack loaders are always evaluated from right to left and from bottom to top (separate definitions).

