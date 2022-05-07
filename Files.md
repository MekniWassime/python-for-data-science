    file = open('file-path', 'r')
    text = file.read() #read the entire file
    file.closed        #weather or not the file is closed
    file.close()       #close the file after using it
we ca use a different syntax so that we don't have to close files manually

    with open('file-path','r') as file:
	    file.readline()
here file is available only inside the bloc, once you get out of it the file is automatically closed 
#### pickle package

    import pickle
    open('filepath', 'rb)
to open a binary file in read-only, pickle files have the extension `.pkl` which are the result of serializing a python object

 -  to read `.xlsx` spreadsheets we use `xls =pd.ExcelFile('filepath')`  
	 - `xls.sheet_names` a list of spreadsheets contained in the file
	 - `df = xls.parse('sheet_name')` to get a single spreadsheet and save it as a *DataFrame* , could also use it's index
		 - `names` a list of strings used to set the column names manually
		 - `skiprows` a list of indexes which specify the rows to skip
		 - `usecols` a list of indexes for the columns that are included
#### sas7bdat package
used to read *SAS* files

    from sas7bdat import SAS7BDAT
    with  SAS7BDAT('file.sas7bdat')  as  file:
	    df = file.to_data_frame()

#### h5py package

    import h5py
    data = h5py.File('filename.hdf5', 'r')

hdf5 files are used to hierarchically store large datasets, data is stored in a structure similar to a dictionary
hdf5 files are composed of *groups* and *datasets* , a *group* can contain multiple *groups* and *datasets* `Group['key']` (`Group.keys()` to get the list of keys), a *dataset* contains values accessed by `DataSet.value`
#### scipy package

    import scipy.io
    mat = scipy.io.loadmat('file.mat')

mat is of type dictionary
#### sqlalchemy package

    from sqlalchemy import create_engine
    engine = create_engine('connection-string')
connect to the sql database using the connection string

 - `engine.table_names()` list of table names stored in the database

to create a connection we use `con = engine.connect()`
to execute a query `rs = con.execute('sql query')`
then we store the result in a *DataFrame* using `df = DataFrame(rs.fetchall())`, instead of `fetchall` we can use `fetchmany(size=n)` to fetch n rows
we add column names to the *DataFrame* using `df.columns = rs.keys()`
after using the connection we close it calling `con.close()`, or we can use the `with engine.connect() con:` syntax so that the connection is automatically closed after we are done using it

another way of executing queries is to use the pandas function

    pd.read_sql_query('sql query', engine)

### Reading from files with Numpy

    data = np.loadtext(filename, delimiter=',')
by default `loadtext` uses any whitespace as delimiter, `'\t'` for tab separated

 - `skiprows` an integer used to skip a number of rows, for example if the first row has labels in it we can skip it using `skiprows=1`
 - `usecols` a list or interval of column indexes that you want to include in your numpy array
 - `dtype` a type, the type that the data will be read in

we can use `np.genfromtxt` to read data where some columns are of a different type, the result is what's called a [structured array](https://numpy.org/doc/stable/user/basics.rec.html)
### Reading from files with Pandas
#### flat files

    df = pd.read_csv('filepath')
read data from a comma seperated file `csv` but can also be used with `.txt` files

 - `sep` a character used as seperator or delimiter, default is `','`
 - `comment` a character which comments occur after
 - `na_values` a string or list of strings that represent `NaN` values in the file

#### stat files

    df = pd.read_stata('file.dta')
### Reading files from the web

    df = pd.read_csv('url')
to download the file and store it in a *DataFrame*

    xls = pd.read_excel(url,sheet_name=None)
to read spreadsheets from the internet, this results in a dictionary of keys being the spreadsheet name and the values being *DataFrame*s
#### urllib package

    from  urllib.request  import  urlretrieve

 - `urlretrieve('url',  'local-path')` download file from `'url'` and save it as `'local-path'`

to perform http request we do the following

    from  urllib.request  import  urlopen, Request
    request = Request('url')
    response = urlopen(request)
    html = response.read()
    response.close()
### requests package

    import requests
    r = requests.get(url)
    text = r.text
a better way of performing http requests

we can also get the response data in different forms, `r.json()` for example to get the response as json (dict)

### BeautifulSoup package

    from  bs4  import  BeautifulSoup
    soup = BeautifulSoup(html_text)
this package makes it easy for us to extract data from a html page

 - `soup.prettify()` returns a properly indented html string
 - `soup.title` to get the title of the html page
 - `soup.text` to extract the text from the page
 - `soup.find_all('html-tag-name')` find all html tags with the selector `'html-tag-name'`
	 - this returns a list of *Tag* objects, `Tag.get('html-attribute')` returns the value of `'html-attribute'` in `Tag`

### json package

    import json
    with open('json-path.json', 'r') as json-file:
	    json_data = json.load(json_file)
intuitively json data is stored as dictionaries

### tweepy package

    import tweepy
    auth = tweepy.OAuthHandler(consumer_key,  consumer_secret)
	auth.set_access_token(access_token,  access_token_secret)

tweepy makes it easy for us to handle authentication to access the twitter api
