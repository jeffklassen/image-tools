# image-organizer
Sort Images by Exif Attributes

## Requirements

Requires gomfunkel's [node-exif](https://github.com/gomfunkel/node-exif) package.

## Getting started

### Installation

1. Download the project by running:

`git clone git@github.com:jeffklassen/image-organizer.git`

2. run `npm install` to download the node-exif dependency

### Configuration

Start at `index.js` and you'll notice that photoOrganizer requires an `options` object with two fields: `srcDir` and `destDir`.

`srcDir` is a string value for the directory containing the pictures you want to move.

`destDir` can be either a string or a callback function accepting the `exifData`. Using a string here will simply move all images from `srcDir` to `destDir`. To sort images based on exif data values, provide a call back as follows:

```javascript
var options = {

  srcDir: 'path/where/your/images/are/',
  destDir: function (exifData) {
        // using the first 4 characters of the exif image.CreateDate value (which turns out to be the year)
        // to sort pictures by year
        var year = exifData.image.CreateDate.substr(0, 4);
       
        return '/home/user/Pictures/' + year + '/CellPhonePics/';
    }
  }
```

**Please note**: since exif values are applied inconsistenly by different cameras, it may be necessary to check multiple exif data locations to get the value you are looking for. Check out `dateExtractor.js` for how I extract the creation date value for multiple images.

### First Run

`node index`

## TODO
1. ~~Document each module~~
2. Add validation for `srdDir` and `destDir` values.