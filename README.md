# BB Matrix Shuffler - v0.8.5 beta
Re-order a two-dimensional array along a horizontal, vertical, or diagonal axis; wrap it outside in or inside out; or shuffle it randomly.

## Demo
Live demonstration at [bobbybol.com/plugins/bb-matrixshuffler](http://bobbybol.com/plugins/bb-matrixshuffler/).

## Features
- Re-order any 2D array, in the following modes:
  - linear, in either vertical or horizontal direction
  - diagonal, from any corner to the opposing corner
  - centralized, from the inside out or the outside in
  - random
- Especially good for shuffling the DOM references of a grid of images.
- Works perfectly together with the [BB Pixelify](https://github.com/bobbybol/pixelify) plugin.

## Usage
The Matrix Shuffler currently expects a jQuery object to be acting on, and will return a shuffled jQuery object when done. This means that is can turn a 1-dimensional array into a 2-dimensional array given the number of rows and columns, and eventually return a flattened 1-dimensional array or a 2-dimensional array, depending on the shuffle-algorithm chosen.  
  
We can shuffle a jQuery selection like so:
```javascript
$('.imageTile').bbShuffleMatrix({
  rows              : 14,
  columns           : 7,
  shuffleAlgorithm  : "diagonal",
  shuffleDirection  : "topleft->bottomright"
});
```
This will shuffle the order of references to each `.imageTile`, so now a staggered 'reveal' animation would reveal the full image from the top-left corner down to the bottom-right corner.

## Settings and their Defaults
There's a number of `options` you can fiddle with, to get the desired result of your specific use-case:
```javascript
{
  /* SETTING               DEFAULT             EXPLANATION
  ==================================================================================================== */
     rows                  : 10,               // number of columns
     columns               : 10,               // number of rows
     shuffleAlgorithm      : "linear",         // linear, diagonal, circular, random
     shuffleDirection      : "top->bottom"     // Direction is different for different algorithms:
                                               // ====================================================
                                               // For linear:
                                               // top->bottom, bottom->top, left->right, right->left
                                               // ====================================================
                                               // For diagonal:
                                               // topleft->bottomright, bottomright->topleft,
                                               // topright->bottomleft, bottomleft->topright
                                               // ====================================================
                                               // For circular:
                                               // inside->out, outside->in
                                               // ==================================================== 
}
```
Take note that each `shuffleAlgorithm` setting requires a specific `shuffleDirection` setting, otherwise the plugin won't work.

## Known issues in **beta**
Currently the settings `linear`, `diagonal`, and `random` will return a flattened, onedimensional array, while the `circular` setting returns a 2D array. This is because a ripple-effect animation can be better achieved with the 2D array. A future version of Matrix Shuffler will give you the choice for each option to return either a onedimensional or a twodimensional array.

## Use in combination with Pixelify
This plugin can be used on any grid of images, but was initially developed to be part of the [BB Pixelify](https://github.com/bobbybol/pixelify) plugin. Hence, Pixelify delivers a couple of settings through the use of `$.data()`. Meaning that we can chain Pixelify and the Matrix Shuffler like so:
```javascript
var tilesToAnimate = $('.imgContainer')
  .bbPixelify({columns: 35, rows: 15})        // cut an image up into a grid of images,
  .bbShuffleMatrix({                          // call Matrix Shuffler to shuffle the grid,
    shuffleAlgorithm: "diagonal",             // specify which shuffle algorithm to use ,
    shuffleDirection: "topleft->bottomright"  // and what direction the tiles should run.
  })
;
// tilesToAnimate is now the variable that you can refer to when animating the tiles
```
Note that you _do not_ have to specify columns and rows a second time - they are passed on from Pixelify to Matrix Shuffler.

## Changelog  
### 0.8.5  
#### Changed
- handle $.data object

### 0.8.0  
#### Added
- circular shuffle

### 0.7.5  
#### Changed
- functional refactoring

### 0.7.0  
#### Added
- linear shuffle
- mirror shuffle

### 0.6.5  
#### Changed
- functional refactoring

### 0.6.0  
#### Added
- diagonal shuffle

### 0.5.0  
#### Added
- random shuffle
