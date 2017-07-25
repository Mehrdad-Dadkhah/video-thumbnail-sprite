# video-thumbnail-sprite

[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE)
[![Packagist Version](https://img.shields.io/packagist/v/emgag/video-thumbnail-sprite.svg?style=flat-square)](https://packagist.org/packages/emgag/video-thumbnail-sprite)
[![Project Status: Active - The project has reached a stable, usable state and is being actively developed.](http://www.repostatus.org/badges/0.1.0/active.svg)](http://www.repostatus.org/#active)

PHP library for generating video thumbnail sprites to be used for thumbnails in [JWPlayer](https://support.jwplayer.com/customer/portal/articles/1407439-adding-preview-thumbnails)'s seek bar. For a real world example used in production, see [gameswelt.de](http://www.gameswelt.de/the-witcher-3-wild-hunt/test/multipler-rollenspielorgasmus,238958).

## System requirements

Tested with >=5.6, following binaries need to be installed

* Either [ffmpeg](http://www.ffmpeg.org/download.html) (tested with >= v2.2) or [ffmpegthumbnailer](https://github.com/dirkvdb/ffmpegthumbnailer)
* [imagemagick](http://www.imagemagick.org/script/binary-releases.php) (tested with >= v6.6)

## Installation

```
composer require emgag/video-thumbnail-sprite
```

## Usage

**NOTE**: Method chaining, setting an alternative converter and keeping the individual images after generating the sprite image are only supported in the current master branch, not in the released version 0.2. 


```PHP
use Emgag\Video\ThumbnailSprite\ThumbnailSprite;


$sprite = new ThumbnailSprite();
$sprite->setSource('path-to-source-video.mp4')
       ->setOutputDirectory('dir-to-store-sprite-and-vtt')
       // filename prefix for image sprite and WebVTT file (defaults to "sprite", resulting in "sprite.jpg" and "sprite.vtt")
       ->setPrefix('sprite') 
       // absolute URL of sprite image or relative to where the WebVTT file is stored
       ->setUrlPrefix('http://example.org/sprites')
       // sampling rate in seconds 
       ->setRate(10) 
       // minimum number of images (will modify sampling rate accordingly if it would result in fewer images than this)
       ->setMinThumbs(20)
       // width of one thumbnail in px 
       ->setWidth(120) 
       ->generate();
```

There are two different converters available, [ffmpeg](http://www.ffmpeg.org/download.html) (default) or [ffmpegthumbnailer](https://github.com/dirkvdb/ffmpegthumbnailer). 

Change converter to ffmpegthumbnailer:

```PHP
$sprite->setConverter('ffmpegthumbnailer');
```

To keep individual images of sprite instead of removing it after assembling the sprite: 

```PHP
$sprite->setOutputImageDirectory('dir-to-store-images');
```

## Acknowledgments

* Inspired by [vlanard/videoscripts](https://github.com/vlanard/videoscripts) and [scaryguy/jwthumbs](https://github.com/scaryguy/jwthumbs).
* Thanks to [Mehrdad-Dadkhah](https://github.com/Mehrdad-Dadkhah) for adding ffmpegthumbnailer support and other additional features.

Uses:

* [captioning/captioning](https://github.com/captioning/captioning)
* [emgag/flysystem-tempdir](https://github.com/emgag/flysystem-tempdir)
* [intervention/image](https://github.com/Intervention/image)
* [php-ffmpeg/php-ffmpeg](https://github.com/PHP-FFMpeg/PHP-FFMpeg)
* [symfony/process](https://github.com/symfony/Process)
* [thephpleague/flysytem](https://github.com/thephpleague/flysystem)

## License

video-thumbnail-sprite is licensed under the [MIT License](http://opensource.org/licenses/MIT).
