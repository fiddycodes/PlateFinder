# PlateFinder
## Outline
This Program will find any body specified body on a given telescopic plate from a choice of 3 useable plate catalogs. It achieves this through the use of python and JPL Horizons, to find out the body positions over a given amount of time.

## Requirements
* Python 3.6
* An installation of the python package manager *PIP*
* Windows or Unix Based System
* An Internet Connection

## Dependencies
This section lists all the external python package dependencies the programme has, for more information on each of them click their name to be redirected to their information page.
* [Astroquery](https://astroquery.readthedocs.io/en/latest/)
* [Astropy](http://www.astropy.org/)
* [TQDM](https://pypi.org/project/tqdm/)
* [Numpy](http://www.numpy.org/)
* [Requests](http://docs.python-requests.org/en/master/)
* [Pyephem](https://rhodesmill.org/pyephem/)
* [Matplotlib](https://matplotlib.org/)
* [RoboBrowser](https://robobrowser.readthedocs.io/en/latest/readme.html)
* [Openpyxl](https://openpyxl.readthedocs.io/)

## Installation
Install any distribution of python desired. This can be a base python installation or preferably a scientific distribution such as Anaconda. A python distribution like Anaconda is recommended as this will have many of the python libraries required for the project already installed. After this you can run the programme in a terminal or command prompt using the [Run.py](https://github.com/fiddycodes/PlateFinder/blob/master/Run.py) file. On initialisation of the programme, the running instance will check if all the dependencies are installed. If not the programme will automatically run shell commands to install the dependencies. These shell commands use the python package manager PIP to install packages with the command: 'pip install `pip install packagename`. If there are any errors in the process of installing the dependencies. Either install it through your desired manual method, or there is a problem with your pip installation. The programme will then create any empty directories it needs and it is ready to be used when the first prompt is displayed.

## Usage
### Entering Options
Many options are provided to get the desired outputs. All these options are chosen by entering a desired number into the program: `1 for Yes, 2 for no` to name an example. The programme will prompt you if anything invalid is entered as an option.
```python
list_options(list) # lists numbered options
while True:
    try:
        answer = int(input("Please enter a the 1 or 2: "))
    # 1st Check: handles errors if numbers are not entered or nothing is entered by user.
    except (ValueError, UnboundLocalError):
        print ("Please enter a valid number of 1 or 2")
    else:
    # 2nd Check: handles errors where user enters number out of range of options.
        if answer < 1 or answer > 2:
            print ("Please Enter a Number in Given Range")
        else:
            # all checks have passed the answer chosen is valid and can be used elsewhere.
            break
```
So enter only numbers into the programme not strings of text.

### Procedure
You can choose between using the graphing module, computation module or both at the start of the programme. This procedure will walk you through the steps of using the computation module first to get results on bodies and then the graphing module for generating images of parts of the sky.

#### Computation Module
1. You will first be prompted to choose what plate catalog you want to load into the programme. There are 4 to choose from but [possI.txt](https://github.com/fiddycodes/PlateFinder/blob/master/Imports/Plate%20Files/possI.txt) should be avoided (See [Known Issues](#Known-Issues) for more information).
2. Then you can choose what bodies to load into the programme this is either from a default list that the programme contains or by loading your own file into the programme (See [Customisation](#Customisation) section).
3. If you have used the programme in the last hour, you will be asked if you would like to purge cache files of the body queried from JPL Horizons. It is up to you whether you keep these files they are contained in the [Ephemeris Cache](https://github.com/fiddycodes/PlateFinder/tree/master/Ephemeris%20Cache/Container) directory.
4. The querying process will take roughly a minute for a body to query all the data required from the plate file, then the computations to find if the body is on a given plate will occur. The results will be placed in the *Exports/Plate Saves* directory and is denoted `Object Name, Date Calculated`.

#### Graphing Module
1. First you can choose how many graphs you would like to generate. One is a perfectly valid option.
2. You can then choose to if you would like to download fits files from the internet or generate existing files that have been saved in the *Exports/Fits-Files* directory. For the purposes of the procedure and what you will want 9 cases out of 10. The procedure will follow downloading the a fits files from the internet. For more information on the generation of images from existing fits files see [Customisation](#Customisation).
3. You will now be prompted to enter which file to open and what plate record to generate. The image is then downloaded and saves to the *Exports/Fits-Images* directory. This process is repeated for as many generations as were chosen. The images are denoted by `Body Taken From - Plate Generated From`
4. After generation you will be prompted if you would like to generate an Excel data spreadsheet containing the data from the graph generations to be used in practical experimentation. These excel sheet will be saved to the *Exports/Excel-Files* and are denoted by `Date Of Creation`.

### General Notes
1. If you delete any directories in the [Exports](Exports) directory, upon reinitialisation of the programme all directories will be created again.
2. The exports directory will be generated upon the first initialisation of the programme, containing all its sub directories, this will lead to a longer start up time.
3. As mentioned above (Section [Requirements](#Requirements)), the programme requires an internet connection to query data from the internet.
4. The caching process will keep cached body files as long as the last date modified on the [Ephemeris Cache](https://github.com/fiddycodes/PlateFinder/tree/master/Ephemeris%20Cache/Container) Directory does not exceed an hour.
5. If more than two bodies are loaded from a file into the programme, a sub directory will be created to hold all the results files.

## Customisation
* New plate entries can be added by modifying the [Imports/Plate File Locals.txt](https://github.com/fiddycodes/PlateFinder/blob/master/Imports/Plate%20Locals.txt) this file will be responsible for downloading new plate catalogues from the internet. Use the following format when entering new plate entries, each point is a line in the file:
  1. Description of where the plate catalog is from i.e the telescope it was taken from.
  2. The link to the plate data. It should be a link to raw text data, so this can be downloaded.
  3. The latitude, longitude and elevation of the telescope where the plate catalogue was taken for degrees and kilometres respectively.
  Take care to ensure that the formats of the plate catalogue are the same, as this can be read into the programme properly. Check catalogue file [Catalog_ukstu.txt](https://github.com/fiddycodes/PlateFinder/blob/master/Imports/Plate%20Files/catlog_ukstu.txt) for reference.
* Text files containing the name of the desired bodies to be calculated can be placed in the [Imports/Body Files](https://github.com/fiddycodes/PlateFinder/tree/master/Imports/Body%20Files) directory. Each body name should be on its own line in the file to be read one by one.
* The list of default bodies can also be edited directly, this is the best method of entering bodies that share their name with others. For example if only the word Mars was used to try and query about Mars the planet, an error would be raised because you have to specify Mars' code '499'. In [Imports/BodyList.txt](https://github.com/fiddycodes/PlateFinder/blob/master/Imports/Body%20List.txt) you can add bodies to the default list by using the form `BodyName BodyCode`.

## Known Issues
* The plate catalogue file [possI.txt](https://github.com/fiddycodes/PlateFinder/blob/master/Imports/Plate%20Files/possI.txt) can not have bodies computed for its plates. Due to its different plate catalogue format. The programme will run but after previous testing, the body will not be found on any plates.

## Things To Do
- [] Incorporate C code into computation for greater precision
- [?] Possibly colour the terminal



