
# Driving License

 This project is a program written in Python that does the following:
 -	Stores the data of citizens who want to issue a driving license

-	Adding/Changing/Removing/Displaying/Sorting Data from files

-	Handling Errors


 
## Functions and Description
For changing and displaying names as well as dealing with files, I made some important key functions and other less complex functions to help my program with a total of 16 functions (No global variables were used)

The major functions are:
```
Option 1 : Adding data
-	The main goal of this function is to call for each function to write data in the file
-	Action is done by calling many functions that are written in the beginning of the program such as getName (), getGender ()()… getBlood () to write the new data in the file
-	If an ID already exists, an appropriate message is displayed.
```
```
Option 2 : Displaying data
-	The main goal of this function to display data in either (Sort by ID, Sort by Gender, Sort by First Name)
-	I created a menu that the user can select 
-	Errors of menu were handled (invalid inputs)
```
```
Option 3 : Editing data
The main reason behind this function is to adjust the data of a specific person (Editing, Removing) data or just show the data of that person
-	Reading the file line by line using loops and converting it to a list to see if a matched ID was found (by indexing) 
-	If a match was found, access the menu that consist of (Update,Remove,Leave)
-	If the user selects update, another menu pops up and it consist of what the user wants to change (Name,Phone Number.. etc)
-	If the user selects, for example Name, the program will go for the specific line that holds the matched Id and change the Name with the new data
-	If the user selects remove, the line that holds that person data will be removed
-	Value Errors were handled
``` 

## 🛠 Skills Used
Python: expressions, decision structures, looping, functions, lists, files and exceptions.
## 🚀 About Me
👋 Hi, I’m @Raed-Alshehri

👀 I’m interested in data science, machine learning, and statistics.

🌱 I’m applying my skills in the data analytics field using Python, R, and SQL


## 🔗 Links
[![portfolio](https://img.shields.io/badge/my_portfolio-000?style=for-the-badge&logo=ko-fi&logoColor=white)](https://raed-alshehri.github.io/RaedAlshehri.github.io/)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/raedalshehri/)


## Feedback

If you have any feedback, please reach out to me at alshehri.raeda@gmail.com

