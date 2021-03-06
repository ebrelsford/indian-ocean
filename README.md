Indian Ocean
============

A library for reading in and writing out data in Node.js, part of [The TK Toolkit](https://github.com/mhkeller/tktk).

# Installation

````
npm install indian-ocean
````

# Usage

````js
var io = require('indian-ocean');

var json_data = io.readDataSync('path/to/data.csv');

console.log(json_data);

/*
[
  {
    "name": "Gerald",
    "occupation": "Teacher",
    "city": "Philadelphia"
  },
  {
    "name": "Marcy",
    "occupation": "Venture Capitalist",
    "city": "New York"
  }
]
*/

io.writeDataSync('path/to/save/output.json', json_data)
````

# Methods

* [Reading data](#reading-data)
    * [.readData(filepath, [delimiter], callback)](#readdatafilepath-delimiter-callback)
    * [.readDataSync(filepath, [delimiter])](#readdatasyncfilepath-delimiter)
    * [.readJson(filepath, callback)](#readjsonfilepath-callback)
    * [.readJsonSync(filepath)](#readjsonsyncfilepath)
    * [.readCsv(filepath, callback)](#readcsvfilepath-callback)
    * [.readCsvSync(filepath)](#readcsvsyncfilepath)
    * [.readTsv(filepath, callback)](#readtsvfilepath-callback)
    * [.readTsvSync(filepath)](#readtsvsyncfilepath)
    * [.readPsv(filepath, callback)](#readpsvfilepath-callback)
    * [.readPsvSync(filepath)](#readpsvsyncfilepath)
    * [.readDbf(filepath, callback)](#readdbffilepath-callback)
* [Writing data](#writing-data)
    * [.writeData(filepath, data, callback)](#writedatafilepath-data-callback)
    * [.writeDataSync(filepath, data)](#writedatasyncfilepath-data)
    * [.writeDbfToData(inFilepath, outFilepath, data)](#writedbftodatainfilepath-outfilepath-callback)
* [Reading directories](#reading-directories)
    * [.readdirInclude(directorypath, filetypes, callback)](#readdirincludedirectorypath-filetypes-callback)
    * [.readdirIncludeSync(filepath, filetypes)](#readdirincludesyncdirectorypath-filetypes-callback)
    * [.readdirExclude(filepath, filetypes, callback)](#readdirexcludedirectorypath-filetypes-callback)
    * [.readdirExcludeSync(filepath, filetypes)](#readdirexcludesyncdirectorypath-filetypes-callback)
* [Helpers](#helpers)
    * [.discernFormat(filepath)](#discernformatfilepath)
    * [.discernParser(filepath, [delimiter]](#discernparserfilepath-delimiter)
    * [.discernFileFormatter(filepath)](#discernfileformatterfilepath)
    * [fs](#fs)


## Reading data

These functions read in a data file as json (a list of objects).

### .readData(filepath, [delimiter], callback)

Reads in a data file given a path ending in the file format. Callback structure is `function(err, data)`.

Supported formats:

* `.json` Array of objects
* `.csv` Comma-separated
* `.tsv` Tab-separated
* `.psv` Pipe-separated

Pass in a delimiter as the second argument to read in another format.

*Note: Does not currently support .dbf files.*

### .readDataSync(filepath, [delimiter])

Syncronous version of `.readData()`.

### .readJson(filepath, callback)

Read in a json file. Callback structure is `function(err, data)`.

### .readJsonSync(filepath)

Read json syncronously.

### .readCsv(filepath, callback)

Read in a comma-separated value file. Callback structure is `function(err, data)`.

### .readCsvSync(filepath)

Read csv syncronously.

### .readTsv(filepath, callback)

Read in a tab-separated value file. Callback structure is `function(err, data)`.

### .readTsvSync(filepath)

Read tsv syncronously.

### .readPsv(filepath, callback)

Read in a pipe-separated value file. Callback structure is `function(err, data)`.

### .readPsvSync(filepath)

Read psv syncronously.

### .readDbf(filepath, callback)

Read in a .dbf file. Callback structure is `function(err, data)`.

## Writing data

Writes json objects to the specified format.

### .writeData(filepath, data, callback)

Write out the data object, inferring the file format from the file ending specified in `filepath`. Callback structure is `function(err)`.

Supported formats:

* `.json` Array of objects
* `.csv` Comma-separated
* `.tsv` Tab-separated
* `.psv` Pipe-separated

*Note: Does not currently support .dbf files.*

### .writeDataSync(filepath, data)

Syncronous version of `.writeData`.

### .writeDbfToData(inFilepath, outFilepath, callback)

Reads in a dbf file with `.readDbf` and write to file using `.writeData`. Callback structure is `function(err)`.

## Reading directories

### .readdirInclude(path, includes, callback)

Makes a list of the files in a directory when they match the string set as *includes*. *includes* can also be an array of strings.  Callback structure is `function(err, files)`.

### .readdirIncludeSync(path, includes)

Returns a list of the files in a directory when they match the string set as *includes*. *includes* can also be an array of strings. Synchronous version of `readdirInclude`.

### .readdirExclude(path, excludes, callback)

Makes a list of the files in a directory when they **do not match** the string set as *excludes*. *excludes* can also be an array of strings.  Callback structure is `function(err, files)`.

### .readdirExcludeSync(path, excludes)

Returns a list of the files in a directory when they **do not match** match the string set as *excludes*. *excludes* can also be an array of strings. Synchronous version of `readdirExclude`.

## Helpers

### .discernFormat(filepath)

Given a `filepath` return its file extension. Used internally by `.discernPaser` and `.discernFileFormatter`.

E.g. `tk.discernFormat('path/to/data.csv')` returns `'csv'`

### .discernParser(filepath, [delimiter])

Given a `filepath`, optionally a delimiter, return a parser that can read that file as json. Used internally by `.readData` and `.readDataSync`.

E.g. 

````js
var csvParser = tk.discernParser('path/to/data.csv');

var json = parser('path/to/data.csv');
````

### .discernFileFormatter(filepath)

Returns a formatter that will format json data to file type specified by the extension in `filepath`. Used internally by `.writeData` and `.writeDataSync`.

E.g.

````js
var formatter = tk.discernFileFormatter('path/to/data.tsv');
var csv = formatter(json);
````

### fs

Exposes the native [File System](http://nodejs.org/api/fs.html) module for convenience.

# License

MIT 
