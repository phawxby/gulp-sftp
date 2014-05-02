# [gulp](http://gulpjs.com)-sftp [![Build Status](https://travis-ci.org/gtg092x/gulp-sftp.svg?branch=master)](https://travis-ci.org/gtg092x/gulp-sftp)

> Upload files via SSH

Useful for uploading and deploying things via sftp. Right now this plugin just uploads everything. Caching and hash comparison are two TODO items.  

[![NPM](https://nodei.co/npm/gulp-sftp.png?downloads=true&stars=true)](https://nodei.co/npm/gulp-sftp/)

## Install

```bash
$ npm install --save-dev gulp-sftp
```


## Usage

```js
var gulp = require('gulp');
var sftp = require('gulp-sftp');

gulp.task('default', function () {
	return gulp.src('src/*')
		.pipe(sftp({
			host: 'website.com',
			user: 'johndoe',
			pass: '1234'
		}));
});
```


## API

### sftp(options)

#### options.host

*Required*  
Type: `String`

#### options.port

Type: `Number`  
Default: `22`

#### options.user

Type: `String`  
Default: `'anonymous'`

#### options.pass

Type: `String`  
Default: `'@anonymous'`

If this option is not set, gulp-sftp assumes the user is using private key authentication and will default to using keys at the following locations:

`~/.ssh/id_dsa` and `/.ssh/id_rsa`

#### options.remotePath

Type: `String`  
Default: `'/'`

The remote path to upload too. This path should exist, though the child directories that house your files do not need to.

#### options.key

type `String` or `Object`
Default: `null`

A key file location. If an object, please use the format `{location:'/path/to/file',passphrase:'secretphrase'}`


#### options.passphrase

type `String`
Default: `null`

A passphrase for secret key authentication. Leave blank if your key does not need a passphrase.

#### options.keyContents

type `String`
Default: `null`

If you wish to pass the key directly through gulp, you can do so by setting it to options.keyContents. This isn't very secure, however, and is strongly discouraged.

#### options.auth

type `String`
Default: `null`

An identifier to access authentication information from `.ftppass` see [Authentication](#Authentication) for more information.


##Authentication

For better security, save authentication data in a json formatted file named `.ftppass`

```js
var gulp = require('gulp');
var sftp = require('gulp-sftp');

gulp.task('default', function () {
	return gulp.src('src/*')
		.pipe(sftp({
			host: 'website.com',			
			auth: 'keyMain'
		}));
});
```

`.ftppass`

```json
{
  "keyMain": {
    "user": "username1",
    "pass": "password1"
  },  
  "privateKey": {    
    "user": "username"
  },
  "privateKeyEncrypted": {    
    "user": "username",
    "passphrase": "passphrase1"
  },
  "privateKeyCustom": {    
    "user": "username",
    "passphrase": "passphrase1",
    "keyLocation": "/full/path/to/key"
  }
}
``` 


## License

[MIT](http://opensource.org/licenses/MIT)