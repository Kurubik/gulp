/**
 * Created by megatron on 15.2.11.
 */
 var landName = 'wp-15-03';
    
    
var gulp = require('gulp');
var stylus = require('gulp-stylus');
var watch = require('gulp-watch');
var minify = require('gulp-minify');
var autoprefixer = require('autoprefixer-stylus');
var minifyHTML = require('gulp-minify-html');
var plumber = require('gulp-plumber');
var notify = require("gulp-notify");
var browserSync = require('browser-sync').create();
var reload      = browserSync.reload;

var stylusCssDest = './' + landName + '/css/';

gulp.task('default', function() {

});

gulp.task('stuff', function () {
    gulp.src('./' + landName + '/assets/images/**/*')
        .pipe(watch('./' + landName + '/assets/images/**/*'))
        .pipe(gulp.dest('./' + landName + '/images/'))
        .pipe(reload({stream:true}));
});

gulp.task('styles', function () {
    gulp.src('./' + landName + '/assets/css/*.styl')
        .pipe(plumber({errorHandler: notify.onError("Error: <%= error.message %>")}))
        .pipe(watch('./' + landName + '/assets/css/*.styl'))
        .pipe(stylus({
            compress: true,
            url: { name: 'url', limit: false },
            use: [autoprefixer({ browsers: ['> 0%', 'IE 7', 'last 3 version', 'Firefox > 20'], cascade: false })]
        }))
        .pipe(gulp.dest(stylusCssDest))
        .pipe(reload({stream:true}));
});

gulp.task('compress', function() {
    gulp.src('./' + landName + '/assets/js/*.js')
        .pipe(plumber({errorHandler: notify.onError("Error: <%= error.message %>")}))
        .pipe(watch('./' + landName + '/assets/js/*.js'))
        .pipe(minify({
            ignoreFiles: ['.combo.js', '-min.js']
        }))
        .pipe(gulp.dest('./' + landName + '/js/'))
        .pipe(reload({stream:true}));
});

gulp.task('templates', function() {
    gulp.src('./' + landName + '/templates/*.html')
        .pipe(watch('./' + landName + '/templates/*.html'))
        .pipe(minifyHTML())
        .pipe(gulp.dest('./' + landName + '/'))
        .pipe(reload({stream:true}));
});

gulp.task('browser-sync', function() {
    browserSync.init({
        server: {
            baseDir: './' + landName + '/',
            index  : "index.html"
        }
    });
});

gulp.task('bs-reload', function () {
    browserSync.reload();
});

gulp.task('default', ['styles', 'compress', 'stuff', 'templates', 'browser-sync']);









===================================================================================================




/**
 * Created by megatron on 15.2.11.
 */


var landName = 'smart-algorithm';

//var Lands = ['smartest', 'smartest2', 'smartest3', 'smartest3', 'smartest4', 'smartest5', 'smartest-reg', 'smartest-reg2', 'smartest-reg3', 'smartest-reg4', 'smartest-reg5'];


    
var gulp = require('gulp');
var stylus = require('gulp-stylus');
var watch = require('gulp-watch');
var minify = require('gulp-minify');
var autoprefixer = require('autoprefixer-stylus');
var minifyHTML = require('gulp-minify-html');
var browserSync = require('browser-sync').create();
var reload      = browserSync.reload;

var stylusCssDest = './' + landName + '/css/';

gulp.task('default', function() {

});
gulp.task('stuff', function () {
    gulp.src('./' + landName + '/assets/images/**/*')
        .pipe(watch('./' + landName + '/assets/images/**/*'))
        .pipe(gulp.dest('./' + landName + '/images/'))
        .pipe(reload({stream:true}));
});

gulp.task('styles', function () {
    gulp.src('./' + landName + '/assets/css/*.styl')
        .pipe(watch('./' + landName + '/assets/css/*.styl'))
        .pipe(stylus({
            compress: true,
           /* url: { name: 'url', limit: false },*/
            use: [autoprefixer({ browsers: ['> 0%', 'IE 7', 'last 3 version', 'Firefox > 20'], cascade: false })]
        }))
        .on('error', swallowError)
        .pipe(gulp.dest(stylusCssDest))
        .pipe(reload({stream:true}));
});

gulp.task('compress', function() {
    gulp.src('./' + landName + '/assets/js/*.js')
        .pipe(watch('./' + landName + '/assets/js/*.js'))
        .pipe(minify({
            ignoreFiles: ['.combo.js', '-min.js']
        }))
        .pipe(gulp.dest('./' + landName + '/js/'))
        .pipe(reload({stream:true}));
});

gulp.task('templates', function() {
    gulp.src('./' + landName + '/templates/*.html')
        .pipe(watch('./' + landName + '/templates/*.html'))
        .pipe(minifyHTML())
        .pipe(gulp.dest('./' + landName + '/'))
        .pipe(reload({stream:true}));
});

gulp.task('browser-sync', function() {
    browserSync.init({
        server: {
            baseDir: './' + landName + '/',
            index  : "index.html"
        }
    });
});

gulp.task('bs-reload', function () {
    browserSync.reload();
});



    gulp.task('default', ['styles', 'compress', 'stuff', 'templates', 'browser-sync']);


function swallowError (error) {
    console.log(error.toString());
    this.emit('end');
}








====================================================================================================================



{
  "main": "gulpfile.js",
  "scripts": {
    "prepublish": "bower install",
    "start": "gulp",
    "build": "gulp build"
  },
  "dependencies": {
    "coffee-script": "~1.7.1"
  },
  "devDependencies": {
    "bower": "~1.3.3",
    "browserify": "~4.1.5",
    "browserify-shim": "~3.5.0",
    "coffeeify": "~0.6.0",
    "ecstatic": "~0.5.3",
    "gulp": "~3.8.2",
    "gulp-autoprefixer": "0.0.7",
    "gulp-minify-css": "~0.3.4",
    "gulp-plumber": "^0.6.2",
    "gulp-rename": "~1.2.0",
    "gulp-streamify": "0.0.5",
    "gulp-stylus": "1.0.1",
    "gulp-uglify": "~0.3.0",
    "gulp-util": "~2.2.14",
    "gulp-minify": "~0.0.11",
    "gulp-watch": "~4.3.5 ",
    "gulp-minify-html": "~1.0.6",
    "gulp-concat" : "~2.2.0",
    "browser-sync": "~2.12.5",
    "autoprefixer-stylus": "~0.9.2",
    "vinyl-source-stream": "~0.1.1",
    "watchify": "~0.10.1"
  },
  "browser": {},
  "browserify-shim": {},
  "browserify": {
    "transform": [
      "coffeeify",
      "browserify-shim"
    ]
  }
}



































