How to create a custom Apple ][ character generator ROM
-------------------------------------------------------

The chargenXXX.pbm files are raw ROM dumps prepended with a PBM bitmap header that allows the reading of the data as an image in a program such as the GIMP (http://gimp.org). The three different PBM files are the basic character generator ROM, one with //e lowercase and special characters, lastly one with the addition of MouseText characters in the area control characters would normally go. The MouseText characters are not compatible with anything and are there for those who want to program their own applications using these useful characters. For best compatibility with existing applications, just use the lower case image.

Launch the GIMP and read the PBM image. To make make editing easier, zoom to about 1000%. Enable grid view and change the grid spacing to 8 pixels. This will align on the character cells and help defining the top and bottom of the characters. Notice that the image is actually reversed: white = 0 and black = 1. To create your own ROM image, start with one of the existing images and paint the characters with a pencil tool and a 1x1 pixel brush. The leftmost column of pixels is not displayed, so whatever is there will be ignored. The effective character cell is 7x8 pixels.

When done, export the image to a PBM file using the RAW option (you will be prompted). At the command line, edit the resulting file with the vi editor as such:
```
vi -b image.pbm
```
using image.pbm for whatever file you previously saved. You will see a few lines of text followed by gibberish. Delete the text header using the 'dd' command for each line of the header. Don't delete the gibberish - that is the font data. Save the result using:
```
:w image.bin
```
using image.bin for the raw font data. This is directly programmable to a 2716 EPROM or 28C16 EEPROM.

