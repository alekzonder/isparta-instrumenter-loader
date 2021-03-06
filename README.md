## Isparta instrumenter loader for [webpack](https://webpack.github.io/)

Instrument JS files with [Isparta](https://github.com/douglasduteil/isparta) for subsequent code coverage reporting.<br/>
Forked from [deepsweet/istanbul-instrumenter-loader](https://github.com/deepsweet/istanbul-instrumenter-loader). Thank you for your work :thumbs_up:

### Install

```sh
$ npm i -S isparta-instrumenter-loader
```

### Usage

Useful to get work together [karma-webpack](https://github.com/webpack/karma-webpack) and [karma-coverage](https://github.com/karma-runner/karma-coverage). For example:

1. [karma-webpack config](https://github.com/webpack/karma-webpack#karma-webpack)
2. [karma-coverage config](https://github.com/karma-runner/karma-coverage#configuration)
3. replace `karma-coverage`'s code instrumenting with `istanbul-instrumenter-loader`'s one:

```javascript
config.set({
    ...
    files: [
      // 'src/**/*.js', << you don't need this anymore
      'test/**/*.js'
    ],
    ...
    preprocessors: {
        // 'src/**/*.js': ['coverage'], << and this too
        'test/**/*.js': [ 'webpack' ]
    },
    reporters: [ 'progress', 'coverage' ],
    coverageReporter: {
        type: 'html',
        dir: 'coverage/'
    },
    ...
    webpack: {
        ...
        module: {
            preLoaders: [ // << add subject as webpack's preloader
                {
                  test: /(\.jsx)|(\.js)$/,
                  // exclude this dirs from coverage
                  exclude: /(test|node_modules|bower_components)\//,
                  loader: 'isparta-instrumenter-loader'
                },
            ],
            // other webpack loaders ...
            loaders: [ ... ],
        },
        ...
    }
});
```

[Documentation: Using loaders](https://webpack.github.io/docs/using-loaders.html).

### License
[WTFPL](http://www.wtfpl.net/wp-content/uploads/2012/12/wtfpl-strip.jpg)
