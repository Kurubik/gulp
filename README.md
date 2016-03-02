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
