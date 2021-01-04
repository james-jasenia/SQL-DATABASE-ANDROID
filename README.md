# SQL Databases Prototype - Android
##### Tutorial: The Complete Android Oreo Developer Course - Section 7

## Purpose: 
The purpose of this app is to explore the data persistence using SQL and databases.


## Key Classes and Methods:
### SQLiteDatabase
The SQLiteDatabase class and the package in which it is provided, contains all of the APIs you will need to create and interact with a database in Android. You use SQL to interact with the database which can be quite string heavy. The documentation recommends creating a companion class (contract class), which explicitly specific the layout of your schema. 

<em>Note: The documentation <strong>highly recommends</strong> that you use <strong>'Room Persistence Library'</strong> as an abstraction layer for accessing information is your SQLiteDatabases. The following code base does <strong>not</strong> use Room.</em>

#### Open or Create:
As the name implies, this method will take a name parameter and either:
- Create a new database if a database with the name does not exist
- Open the database with the same name
```
SQLiteDatabase myDatabase = this.openOrCreateDatabase("Users", MODE_PRIVATE, null);
```

### .execSQL()
This method allows you to interact with the database using SQL. 

#### Create table
```
myDatabase.execSQL("CREATE TABLE IF NOT EXISTS users (name VARCHAR, age INT(3))");
```

#### Insert
```
myDatabase.execSQL("INSERT INTO users (name, age) VALUES ('James', 30)");
myDatabase.execSQL("INSERT INTO users (name, age) VALUES ('Sarah', 28)");
```

### Cursor
The cursor object is an interface which represents a table of any database. When you try to retrieve data using the .rawQuery method, the database will return a Cursor object. It is convention to name the cursor c. When the cursor is created, it will point to the 0th location. You use the .movesToFirst() method to move to the first location in the table. Some helpful methods for moving the cursors are:
.moveToFirst()
.moveToNext()
.moveToPosition(Integer index)
.moveToLast()
.moveToPrevious()

#### Accessing
You need to get the column indices you require. 
```
Cursor c = myDatabase.rawQuery("SELECT * FROM users", null);

int nameIndex = c.getColumnIndex("name");
int ageIndex = c.getColumnIndex("age");

c.moveToFirst();

while (!c.isAfterLast()) {
  Log.i("Name", c.getString(nameIndex));
  Log.i("Age", c.getString(ageIndex));
  c.moveToNext();
}
```

