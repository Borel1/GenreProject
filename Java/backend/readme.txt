6/5/13 - mikeb
NEW: Added a very basic ARFF class
DerbyDB: Fixed exception handling so errors will be thrown to GUI.
DerbyDB: Added indexing by author/title for faster retrieval.
DerbyDB: Added a return record method in anticipation of GUI.

6/3/13 - mikeb
For the time being, I'm going to store all of the classes I write to handle the data sources available to users of the browser tool in this folder.  Right now there is just the DerbyDB interface (and its dependency).  I will eventually setup Eclipse to handle git commits, so this folder will eventually be assimilated into the organization it prefers.

Class information:

--DerbyDB--
Dependencies: derby.jar
Possible exceptions thrown: SQLException, IOException

This is a class written using the Derby API to handle basic operations with the large metadata table that was generated during an earlier phase of the project.  Currently, it is capable of:
- connecting to an existing, local database
- creating a new database and populating it using metatable.txt (or a similar structured table)
- filtering metatable.txt entries with ranges or fuzzy dates into separate tables within the Derby database so that queries can be made based on publication date and/or results ordered by date
- issuing SQL queries and returning the results as a String[][] matrix

Databases are connected to (or created) using the constructors.  In addition to specifying a local database or a seed metatable.txt file, a framework must be also be specified.  For now, this should always be "embedded".  Changes to the constructors to setup a networked connection shouldn't affect the rest of the methods.

To use an instance of DerbyDB to perform a search, the object will need to be passed into the object that deals with user input.  The user input object will then need to parse search fields into an SQL string for DerbyDB.  I left the query method open-ended, accepting just an SQL command as a String so that there wouldn't be any limitations on searches in DerbyDB.


--ARFF--
This class has no dependencies and throws no exceptions.

This is a very simple class that can read/write ARFF files as String[]'s (where each line is a line from an ARFF file).  File reading and writing should be handled by the application itself.  Currently also uses a very basic "add" function which assumes all pages and page parts are part of a prediction with a probability of 100%.

TODO: 
- Interface methods that return particular entries from the csv or specific values for particular entries in the csv.
- More flexible add method
- Use a sparse matrix to store the data?
