# C++ Packager
Unix only library for packaging files.

## Package structure
Every package starts with block of 256 entries that have position of every file in this package.
Last entry of the block is a position (block offset) of the next block in the package. Files are identified
by hash of their names.
```
--------------- BLOCK BEGINS ------------------
0x0000 | FN hash (32 bytes) | F pos (4 bytes) |
0x....
0x00F0 | FN hash (32 bytes) | F pos (4 bytes) |
0x0100 |         empty      | B pos (4 bytes) |
---------------  BLOCK ENDS -------------------
0x0101 |              file content            |
0x.... |                                      |
```
Where:
 * `FN hash` - is SHA-256 hash of the file name. 
 * `F pos` -  position of that file in package starting from the begging of the current block.
 * `B pos` - position of the next block in this package.

## Utility
Simple executable which allows to quickly create a package from collection of files:
```bash
packager create <resource directory path>
```

You can also scan existing packages to get information on block and entries:
```bash
packager scan <path to the package>
```
