# Introduction #

The code file g\_fileops.c contains within it several functions useful for reading/writing integers and strings to and from an external file.  The write functions "write" to the external file in plain text. The read functions require that the external file is in plain human readable text.

Most of these functions do not have return values, they are "voids". As a result, to successfully "read" from a file, the output destination of the "read" must be specified as a parameter when calling the function.

While these functions were added for the use in a feature currently being written, they were added as an additional file in order to provide modularity to the source, and accessibility for creating other features. (It also makes navigating the higher levels of code much easier!)

This file is currently, and will always be a work in progress.

# List of Functions #

  * readFile\_int
  * readFile\_string
  * writeFile\_int
  * writeFile\_string