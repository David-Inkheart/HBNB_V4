# Simple AirBnB Clone

This repo holds the culmination of **HBNB** - a Fullstack Project I did at [Alx-Software Engineering Programme](https://www.alxafrica.com/software-engineering/) that collectively covers fundamental concepts of higher level programming. It is built in stages(versions) and involves collaborating with peers at several stages as was advised in the programme. The goal of AirBnB Clone project is to eventually deploy on a server, a simple copy([HBnB](http://web-01.david-inkheart.tech/)) of the [AirBnB Website](https://www.airbnb.com/). 

It is a complete web application composed by:

- A command interpreter to manipulate data without a visual interface, like in a Shell (perfect for development and debugging)
- A website (the front-end) that shows the final product to everybody: static and dynamic
- A database or files that store data (data = objects)
- An API that provides a communication interface between the front-end and the data (retrieve, create, delete, update them)

See a snapshot of the success below. 

[![js-semistandard-style](https://img.shields.io/badge/code%20style-semistandard-brightgreen.svg?style=flat-square)](https://github.com/standard/semistandard)

![Hosted-AirBnB-Clone 2023-03-08 163931](https://user-images.githubusercontent.com/106752187/232021210-813cf56b-8462-4c29-a475-9bb74d52a332.jpg)

### This is a unique overview and not an exhaustive documentation of different processes and aspects of the project that lead to this final repo.

## Table of Content
* [THE CONSOLE](#the-console)
* [Environment](#environment)
* [Installation](#installation)
* [File Descriptions](#file-descriptions)
* [Examples of Console use](#examples-of-use)
* [VERSION 2](#version-2)
* [Console improvements](#console-improvements)
* [Dataflow and Relationship diagram](#sample-dataflow-relationship-diagram-for-implementations)
* [Additional updates 1: Web framework and Templating](#additional-updates-1)
* [VERSION 3](#version-3)
* [Bugs](#bugs)
* [Authors](#authors)
* [License](#license)

## THE CONSOLE
The console is the first segment of the AirBnB project. A command line interpreter is created in this segment to manage objects for the AirBnB(HBnB) website.

This aspect of the clone was co-built with [Lateef](https://github.com/Wireless-XZ) and the original repo resides [here](https://github.com/David-Inkheart/AirBnB_clone)

Concepts learned by building this command interpreter include:

- Creating a Python [package](https://docs.python.org/3.4/tutorial/modules.html#packages) and creating a command interpreter in Python using the [cmd module](https://docs.python.org/3.8/library/cmd.html)
- [Unit testing](https://docs.python.org/3.8/library/unittest.html#module-unittest) and how to implement it in a large project
- Serializing and deserializing a Class, How to write and read a JSON file.
- Mananaging [datetime](https://docs.python.org/3.8/library/datetime.html) and making use of an [UUID](https://docs.python.org/3.8/library/uuid.html) for unique IDs
- ['*args' and '**kwargs'](https://yasoob.me/2013/08/04/args-and-kwargs-in-python-explained/) and handling named arguments in a function

#### Functionalities of this command interpreter:
* Create a new object (ex: a new User or a new Place)
* Retrieve an object from a file, a database etc...
* Do operations on objects (count, compute stats, etc...)
* Update attributes of an object
* Destroy an object


## Environment
This project is interpreted/tested on Ubuntu 14.04 LTS using python3 (version 3.4.3)

## Installation
* Clone this repository: `git clone "https://github.com/David-Inkheart/HBNB_V4.git"`
* Access HBNB directory: `cd HBNB_V4`
* Run hbnb(interactively): `./console` and enter command
* Run hbnb(non-interactively): `echo "<command>" | ./console.py`

## File Descriptions
[console.py](console.py) - the console contains the entry point of the command interpreter.
List of commands this console current supports:
* `EOF` - exits console 
* `quit` - exits console
* `<emptyline>` - overwrites default emptyline method and does nothing
* `create` - Creates a new instance of`BaseModel`, saves it (to the JSON file) and prints the id
* `destroy` - Deletes an instance based on the class name and id (save the change into the JSON file). 
* `show` - Prints the string representation of an instance based on the class name and id.
* `all` - Prints all string representation of all instances based or not on the class name. 
* `update` - Updates an instance based on the class name and id by adding or updating attribute (save the change into the JSON file).

![Console](https://user-images.githubusercontent.com/106752187/232034599-89a62f38-994e-431b-97ec-b3fb000229bf.jpg)

#### `models/` directory contains classes used for this project:
[base_model.py](/models/base_model.py) - The BaseModel class from which future classes was be derived
* `def __init__(self, *args, **kwargs)` - Initialization of the base model
* `def __str__(self)` - String representation of the BaseModel class
* `def save(self)` - Updates the attribute `updated_at` with the current datetime
* `def to_dict(self)` - returns a dictionary containing all keys/values of the instance

Classes inherited from Base Model:
* [amenity.py](/models/amenity.py)
* [city.py](/models/city.py)
* [place.py](/models/place.py)
* [review.py](/models/review.py)
* [state.py](/models/state.py)
* [user.py](/models/user.py)

#### `/models/engine` directory contains File Storage class that handles JASON serialization and deserialization :
[file_storage.py](/models/engine/file_storage.py) - serializes instances to a JSON file & deserializes back to instances
* `def all(self)` - returns the dictionary __objects
* `def new(self, obj)` - sets in __objects the obj with key <obj class name>.id
* `def save(self)` - serializes __objects to the JSON file (path: __file_path)
* ` def reload(self)` -  deserializes the JSON file to __objects

#### `/tests` directory contains all [unit test](https://docs.python.org/3.4/library/unittest.html#module-unittest) cases for this project:
[/test_models/test_base_model.py](/tests/test_models/test_base_model.py) - Contains the TestBaseModel and TestBaseModelDocs classes
TestBaseModelDocs class:
* `def setUpClass(cls)`- Set up for the doc tests
* `def test_pep8_conformance_base_model(self)` - Test that models/base_model.py conforms to PEP8
* `def test_pep8_conformance_test_base_model(self)` - Test that tests/test_models/test_base_model.py conforms to PEP8
* `def test_bm_module_docstring(self)` - Test for the base_model.py module docstring
* `def test_bm_class_docstring(self)` - Test for the BaseModel class docstring
* `def test_bm_func_docstrings(self)` - Test for the presence of docstrings in BaseModel methods

TestBaseModel class:
* `def test_is_base_model(self)` - Test that the instatiation of a BaseModel works
* `def test_created_at_instantiation(self)` - Test created_at is a pub. instance attribute of type datetime
* `def test_updated_at_instantiation(self)` - Test updated_at is a pub. instance attribute of type datetime
* `def test_diff_datetime_objs(self)` - Test that two BaseModel instances have different datetime objects

[/test_models/test_amenity.py](/tests/test_models/test_amenity.py) - Contains the TestAmenityDocs class:
* `def setUpClass(cls)` - Set up for the doc tests
* `def test_pep8_conformance_amenity(self)` - Test that models/amenity.py conforms to PEP8
* `def test_pep8_conformance_test_amenity(self)` - Test that tests/test_models/test_amenity.py conforms to PEP8
* `def test_amenity_module_docstring(self)` - Test for the amenity.py module docstring
* `def test_amenity_class_docstring(self)` - Test for the Amenity class docstring

[/test_models/test_city.py](/tests/test_models/test_city.py) - Contains the TestCityDocs class:
* `def setUpClass(cls)` - Set up for the doc tests
* `def test_pep8_conformance_city(self)` - Test that models/city.py conforms to PEP8
* `def test_pep8_conformance_test_city(self)` - Test that tests/test_models/test_city.py conforms to PEP8
* `def test_city_module_docstring(self)` - Test for the city.py module docstring
* `def test_city_class_docstring(self)` - Test for the City class docstring

[/test_models/test_file_storage.py](/tests/test_models/test_file_storage.py) - Contains the TestFileStorageDocs class:
* `def setUpClass(cls)` - Set up for the doc tests
* `def test_pep8_conformance_file_storage(self)` - Test that models/file_storage.py conforms to PEP8
* `def test_pep8_conformance_test_file_storage(self)` - Test that tests/test_models/test_file_storage.py conforms to PEP8
* `def test_file_storage_module_docstring(self)` - Test for the file_storage.py module docstring
* `def test_file_storage_class_docstring(self)` - Test for the FileStorage class docstring

[/test_models/test_place.py](/tests/test_models/test_place.py) - Contains the TestPlaceDoc class:
* `def setUpClass(cls)` - Set up for the doc tests
* `def test_pep8_conformance_place(self)` - Test that models/place.py conforms to PEP8.
* `def test_pep8_conformance_test_place(self)` - Test that tests/test_models/test_place.py conforms to PEP8.
* `def test_place_module_docstring(self)` - Test for the place.py module docstring
* `def test_place_class_docstring(self)` - Test for the Place class docstring

[/test_models/test_review.py](/tests/test_models/test_review.py) - Contains the TestReviewDocs class:
* `def setUpClass(cls)` - Set up for the doc tests
* `def test_pep8_conformance_review(self)` - Test that models/review.py conforms to PEP8
* `def test_pep8_conformance_test_review(self)` - Test that tests/test_models/test_review.py conforms to PEP8
* `def test_review_module_docstring(self)` - Test for the review.py module docstring
* `def test_review_class_docstring(self)` - Test for the Review class docstring

[/test_models/state.py](/tests/test_models/test_state.py) - Contains the TestStateDocs class:
* `def setUpClass(cls)` - Set up for the doc tests
* `def test_pep8_conformance_state(self)` - Test that models/state.py conforms to PEP8
* `def test_pep8_conformance_test_state(self)` - Test that tests/test_models/test_state.py conforms to PEP8
* `def test_state_module_docstring(self)` - Test for the state.py module docstring
* `def test_state_class_docstring(self)` - Test for the State class docstring

[/test_models/user.py](/tests/test_models/test_user.py) - Contains the TestUserDocs class:
* `def setUpClass(cls)` - Set up for the doc tests
* `def test_pep8_conformance_user(self)` - Test that models/user.py conforms to PEP8
* `def test_pep8_conformance_test_user(self)` - Test that tests/test_models/test_user.py conforms to PEP8
* `def test_user_module_docstring(self)` - Test for the user.py module docstring
* `def test_user_class_docstring(self)` - Test for the User class docstring


## Examples of use
```
...web-01:~/HBNB_V4$ ./console.py
(hbnb) help

Documented commands (type help <topic>):
========================================
EOF  all  create  destroy  help  quit  show  update

(hbnb) all MyModel
** class doesn't exist **
(hbnb) create BaseModel
7da56403-cc45-4f1c-ad32-bfafeb2bb050
(hbnb) all BaseModel
[[BaseModel] (7da56403-cc45-4f1c-ad32-bfafeb2bb050) {'updated_at': datetime.datetime(2017, 9, 28, 9, 50, 46, 772167), 'id': '7da56403-cc45-4f1c-ad32-bfafeb2bb050', 'created_at': datetime.datetime(2017, 9, 28, 9, 50, 46, 772123)}]
(hbnb) show BaseModel 7da56403-cc45-4f1c-ad32-bfafeb2bb050
[BaseModel] (7da56403-cc45-4f1c-ad32-bfafeb2bb050) {'updated_at': datetime.datetime(2017, 9, 28, 9, 50, 46, 772167), 'id': '7da56403-cc45-4f1c-ad32-bfafeb2bb050', 'created_at': datetime.datetime(2017, 9, 28, 9, 50, 46, 772123)}
(hbnb) destroy BaseModel 7da56403-cc45-4f1c-ad32-bfafeb2bb050
(hbnb) show BaseModel 7da56403-cc45-4f1c-ad32-bfafeb2bb050
** no instance found **
(hbnb) quit
```

<br/>
  
## VERSION 2
  
![image](https://user-images.githubusercontent.com/106752187/232076687-5c311cf7-b494-413e-8f97-4015f2ae8b71.png)

For this aspect, I collaborated with [Davidson](https://github.com/rotex5). One of the goals of this aspect was to simulate what is obtainable in the industry, where we will work on an existing codebase majority of the time. Our first thoughts upon looking at it might include:

“Who did this code?”, 
“How it works?”, 
“Where are unittests?”, 
“Where is this?”, 
“Why did they do that like this?”, 
“I don’t understand anything.”, 
“… I will refactor everything…”

But the worst thing we could possibly do is to redo everything. The existing codebase might be perfect, or it might have errors. We were taught not to always trust the existing codebase!

First, we were to fork an existing [codebase](https://github.com/justinmajetich/AirBnB_clone) where the console had already been built, run our checks, available tests. Then build on the existing, adding more test where necessary. 

The major additions we did on this Iteration includes: Console improvement and using an ORM to map our objects to a database. The goals we were able to accomplish include: 

* Implementation of Unit testing in a large project
* Using `*args` and `**kwargs` and handling named arguments in a function
* Creating a MySQL database and creating a MySQL user with granted privileges
* Using an ORM(SqlAlchemy) to map a Python Class to MySQL table
* Handling 2 different storage engines with the same codebase (jsonified File storage and MySQL db)
* Using environment variables
* Managing both storage engines and performing CRUD on both seamlessly

Our original repo lives [here](https://github.com/David-Inkheart/AirBnB_clone_v2)

## Console improvements

- Updated the def do_create(self, arg): function of the command interpreter (console.py) to allow for object creation with given parameters:

```
Command syntax: create <Class name> <param 1> <param 2> <param 3>...
Param syntax: <key name>=<value>
Value syntax:
String: "<value>" => starts with a double quote
```

- any double quote inside the value must be escaped with a backslash \
- all underscores '_' must be replaced by spaces ' '.
  Example: I want to set the string `My little house` to the attribute name, the command line must be name="My_little_house"

```
Float: <unit>.<decimal> => contains a dot .
Integer: <number> => default case
```

If any parameter doesn’t fit with these requirements or can’t be recognized correctly by the program, it will be skipped

## Sample dataflow-relationship diagram for implementations

![image](https://user-images.githubusercontent.com/106752187/232045286-eeb2ecd3-b64e-4fa1-9ff4-511a923fd303.png)

<br/>
  
## Additional updates 1

#### Additional updates were added by me as part of my learning journey with ALX. 

![image](https://user-images.githubusercontent.com/106752187/232049489-51aa72e9-46a9-4ce7-ab4a-904fd3250717.png)

The goal of this includes:

- learning about [Web Frameworks](https://intelegain-technologies.medium.com/what-are-web-frameworks-and-why-you-need-them-c4e8806bd0fb) and how to build a web framework with [Flask](https://flask.palletsprojects.com/en/1.0.x/quickstart/#a-minimal-application)
- defining [routes](https://flask.palletsprojects.com/en/1.0.x/quickstart/#routing) in [Flask](https://palletsprojects.com/p/flask/) and handling variables in a route
- creating a [HTML response](https://flask.palletsprojects.com/en/1.0.x/quickstart/#rendering-templates) in Flask by using a template ([Jinja](https://jinja.palletsprojects.com/en/2.9.x/templates/))
- creating [dynamic templates](https://jinja.palletsprojects.com/en/2.9.x/templates/#list-of-control-structures) (using loops, conditions…) and displaying data from a MySQL database in HTML

At the end of this,  HBNB came alive!

![popover1](https://user-images.githubusercontent.com/106752187/232054802-d33c93b5-afdb-4b57-8307-8481a118b17a.jpg)

![popover2](https://user-images.githubusercontent.com/106752187/232055573-1112923c-f358-421f-a749-e6706a5bbdd1.jpg)

 <br/>

## VERSION 3



## Bugs
No known bugs at this time. 

## Authors
Alexa Orrico - [Github](https://github.com/alexaorrico) / [Twitter](https://twitter.com/alexa_orrico)  
Jennifer Huang - [Github](https://github.com/jhuang10123) / [Twitter](https://twitter.com/earthtojhuang)  
Jhoan Zamora - [Github](https://github.com/jzamora5) / [Twitter](https://twitter.com/JhoanZamora10)  
David Ovalle - [Github](https://github.com/Nukemenonai) / [Twitter](https://twitter.com/disartDave)  
Ukanwoke Philip - [Github](https://github.com/Kaditcuy) / [Twitter](https://twitter.com/_Ukanwoke)  
David Okolie - [Github](http://github.com/David-Inkheart) / [Twitter](https://twitter.com/David_Inkheart)  
Second part of Airbnb: Joann Vuong
## License
Public Domain. No copy write protection. 
