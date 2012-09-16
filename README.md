

# LibComponentLogging-embedded

[http://0xc0.de/LibComponentLogging](http://0xc0.de/LibComponentLogging)    
[http://github.com/aharren/LibComponentLogging-embedded](http://github.com/aharren/LibComponentLogging-embedded)


## Overview

lcl\_embed is a tiny tool to create embedded variants of LibComponentLogging for usage in libraries or frameworks.

Such an embedded variant of LibComponentLogging is characterized by having your library/framework's unique prefix in each of LibComponentLogging's code symbols and file names. This way it's possible to use LibComponentLogging in your library/framework and expose it to the clients of your library/framework, while these clients can use a normal installation of LibComponentLogging for their own logging.


## Usage

1. Install and configure LibComponentLogging for your library or framework.

2. Download the lcl\_embed script or clone this repository.

3. Run lcl\_embed on your project files to transform LibComponentLogging into an embedded variant.


## Example

lcl\_embed's usage is

    lcl_embed <project-name> <symbol-prefix> <folder>

So, 

    lcl_embed MyProject MP .

will call lcl\_embed with the project name MyProject and the symbol prefix MP on the files in the current folder.

lcl\_embed will modify all files which contain LibComponentLogging symbols and add the symbol prefix as a prefix to all symbols, e.g. afterwards all log components will have the prefix MPlcl\_c instead of lcl\_c and log levels will have the prefix MPlcl\_v instead of lcl\_v.

lcl\_embed will also rename all files from LibComponentLogging and add the symbol prefix as a suffix to the file names, e.g. it will rename lcl.h to lcl\_MP.h and lcl\_config\_components.h to lcl\_config\_components\_MP.h. lcl\_embed will also adjust your Xcode project file.

In addition, lcl\_embed will delete all LibComponentLogging template files.

## Copyright and License

Copyright (c) 2012 Arne Harren <ah@0xc0.de>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

