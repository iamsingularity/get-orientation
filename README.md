# get-orientation

[![Build Status](https://travis-ci.org/mooyoul/get-image-orientation.svg?branch=master)](https://travis-ci.org/mooyoul/get-image-orientation)
![npm bundle size (minified)](https://img.shields.io/bundlephobia/min/get-image-orientation.svg)
[![MIT license](http://img.shields.io/badge/license-MIT-blue.svg)](http://mooyoul.mit-license.org/)

Read Orientation tag value from Image. Supports both Browser and Server (Node.js) environment.

## Sponsor

- [Vingle](https://www.vingle.net) - Vingle, Very Community. Love the things that you love. - [We're hiring!](https://careers.vingle.net/#/engineering/backend)

## Demo

## Install

#### from NPM

```bash
$ npm install get-orientation
```


## Supported Image Format

- JPEG/JFIF
- JPEG/EXIF
- TIFF/EXIF
    
 
## Usage

#### Node.js

```typescript

import * as fs from "fs";
import { getOrientation } from "get-orientation";

// using Readable File Stream as input
const stream = fs.createReadStream(imageFilePath);
const orientation = await getOrientation(stream);

// using Buffer as input
const bufFile = fs.readFileSync(imageFilePath);
const orientation = await getOrientation(bufFile);

// using HTTP Response body as input
import * as axios from "axios";
const response = await axios({ url, responseType: "stream" });
const orientation = await getOrientation(response.data);


// using Stream interface directly
import { EXIFOrientationParser } from "get-orientation";

const parser = new EXIFOrientationParser();
parser.on("orientation", console.log);

fs.createReadStream(imageFilePath).pipe(parser);
```
 
## API (Node.js)

### `getOrientation(input: Buffer | ReadableStream)` => `Promise<Orientation>`

returns Orientation of given image.

If image is non-jpeg image, or non-image, `getOrientation` will return Orientation.  

### `new EXIFOrientationParser(input: ArrayBuffer | File)` => `WritableStram`

returns a parser stream instance that implements WritableStream interface. 

## Types

### Orientation

```typescript
enum Orientation {
  TOP_LEFT = 1,         // Horizontal (Default)
  TOP_RIGHT = 2,        // Mirror Horizontal
  BOTTOM_RIGHT  = 3,    // Rotate 180
  BOTTOM_LEFT = 4,      // Mirror vertical
  LEFT_TOP = 5,         // Mirror horizontal and rotate 270 CW
  RIGHT_TOP = 6,        // Rotate 90 CW
  RIGHT_BOTTOM = 7,     // Mirror horizontal and rotate 90 CW
  LEFT_BOTTOM = 8,      // Rotate 270 CW
}
```


## Changelog

#### 0.1.0

- Initial Release


## Testing

```bash
$ npm run test
```


## Build

```bash
$ npm run build
```

## Related

- [mooyoul/node-webpinfo](https://github.com/mooyoul/node-webpinfo) - Strongly typed, Stream based WebP Container Parser

## License
[MIT](LICENSE)

See full license on [mooyoul.mit-license.org](http://mooyoul.mit-license.org/)