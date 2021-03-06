# gulp-s3-upload

Made for work + personal use for uploading assets to Amazon S3 servers.  
This helps to make it an easy gulp task.

This package uses the [aws-sdk (node)](http://aws.amazon.com/sdk-for-node-js/).


**Note**
I haven't written tests for this quite yet, since it utilizes an Amazon AWS account.
This is also my first gulp plugin and my first npm published package, so any advice/help appreciated.
Thanks, Caroline

## Install
    npm install gulp-s3-upload

## Usage
    
Put in your AWS Developer key/secret. Region is optional.

    var gulp = require('gulp');
    var s3 = require('gulp-s3-upload')({
        key:       "YOUR DEV ID",
        secret:    "YOUR SECRET",
        region:    "us-west-2"     // optional
    });

Create a task.

    gulp.task("upload", function() {
        gulp.src("./dir/to/upload/**")
            .pipe(s3({
                bucket: 'your-bucket-name', //  Required
                acl:    'public-read'       //  Optional ACL permissions, defaults to public-read.
            }))
        ;
    });


#### Options

**bucket** *(required)*

Type: `string`

The bucket that the files will be uploaded to.


**acl**

Type: `string`

See [Access Control List (ACL) Overview](http://docs.aws.amazon.com/AmazonS3/latest/dev/acl-overview.html) 
for more information.  Defaults to 'public-read'.


**name_transform**

Type: `function`

Use this to transform your file names before they're uploaded to your S3 bucket.

Example:

    gulp.task("upload_transform", function() {
        gulp.src("./dir/to/upload/**")
            .pipe(aws({
                bucket: 'example-bucket',
                name_transform: function(relative_filename) {
                    var new_name = change_file_name(relative_filename);
                    return new_name;
                }
            }))
        ;
    });

----------------------------------------------------

### License 
Copyright (c) 2014, [Caroline Amaba](mailto:caroline.amaba@gmail.com)

Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted, provided that the above copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
