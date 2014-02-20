*This repository is a mirror of the [component](http://component.io) module [component/s3](http://github.com/component/s3). It has been modified to work with NPM+Browserify. You can install it using the command `npm install npmcomponent/component-s3`. Please do not open issues or send pull requests against this repo. If you have issues with this repo, report it to [npmcomponent](https://github.com/airportyh/npmcomponent).*

# s3

  S3 client upload library.

## Installation

    $ component install component/s3

## Config

  An `S3` global must be initialized with some configuration:

  - `policy` - the base64 json policy
  - `signature` - the policy signature
  - `bucket` the bucket name
  - `acl` ACL such as "public-read"
  - `key` access key

## Example

```js
var Upload = require('s3');
var drop = require('drop-anywhere');

drop(function(err, drop){
  if ('upload' != drop.type) return;
  var file = drop.item.file;
  console.log('upload %s', file.name);
  var uid = Math.random() * 1e10 | 0;
  var upload = Upload(file, { name: uid })

  var prog = document.querySelector('#progress');
  upload.on('progress', function(e){
    prog.textContent = (e.percent | 0) + '%';
  });

  upload.end(function(err){
    if (err) throw err;
    console.log('upload complete %s', upload.name);
    console.log(upload.url);
  });
});
```

## API

### Upload(options)

  - `name` remote filename or `file.name`
  - `type` content-type or `file.type`

Events:

  - `abort` upload was aborted
  - `progress` upload in progress (`e.percent` etc)
  - `end` upload is complete

## Testing

  First populate `./config.json` with your credentials:

```json
{
  "key": "asdfasdfasdfasdf",
  "secret": "asdfasdfasdfasdfasdfadsfasfdsfdasdf+fHgg",
  "bucket": "files.example.com"
}
```

  Boot the test server:

```
$ node test
```

## License

  MIT
