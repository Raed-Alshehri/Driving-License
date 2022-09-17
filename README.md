
# Driving License

 This project is a program written in Python that does the following:
 -	Stores the data of citizens who want to issue a driving license

-	Adding/changing/removing/displaying/sorting data from files

-	Handling errors


 
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

## Code
```python
# a function to get the name from the user
def getName():
    firstName = input("Your First Name: ")
    lastName = input("Your Last Name: ")
    while firstName.isalpha()== False or firstName.isspace()== True or lastName.isalpha()== False or lastName.isspace()== True:
        print("Please enter a vaild name")
        firstName = input("Your First Name: ")
        lastName = input("Your Last Name: ")
    return firstName + ";" + lastName
# a function to get the gender from the user     
def getGender():    
    gender = input("Your gender (Male/Female): ")
    gender = gender.upper()
    while not gender in ("FEMALE", "MALE"):
        print("Please enter your gender (Male/Female)")
        gender = input("Your gender (Male/Female): ")
        gender = gender.upper()
    return gender

# a function to get the id from the user 
def getIdNumber(n):
    number = input("Your id number: ")
    while len(number) != n or number.isdigit() == False:
        print("Please enter a vaild number")
        number = input("Your id number: ")
    return number
# a function to get the phoneNumber from the user 
def getPhoneNumber(n):
    number = input("Your phone number: ")
    while len(number) != n or number.isdigit() == False:
        print("Please enter a vaild number")
        number = input("Your phone number: ")
    return number
# a function to get the country from the user 
def getCountry():
    country = input("Your nationality: ")
    while country.isalpha() == False:
        print("Please enter a vaild nationality")
        country = input("Your nationality: ")
    return country.upper()

import datetime
# a function for getting data from the user
def getDate():   
    birth = input("Enter your date of birth (M/D/Y): ")
    birth = birth.split('/')
    for i in range(len(birth)):
         
        while birth[i].isdigit() == False:
            print("Please enter your birth date in the correct format")
            birth = input("Enter your date of birth (M/D/Y): ")
            birth = birth.split('/')
        i += 1
    year = datetime.datetime.now().year
    while len(birth) != 3 or int(birth[0]) > 12  or int(birth[1]) > 31 or int(birth[2]) > year + 1:
        print("Please enter your birth date in the correct format")
        birth = input("Enter your date of birth (M/D/Y): ")
        birth = birth.split('/')
    return "/".join(birth)

# a function to get the blood from the user 
def getBlood():
    blood = input("Your blood type:")
    blood = blood.upper()
    bloodTypes = ['A-', 'A+', 'B-', 'B+', 'AB+', 'AB-', 'O+', 'O-']
        
    while blood not in bloodTypes:
        print("Please enter a vaild blood type")
        blood = input("Your blood type:")
        blood = blood.upper()
    return blood

# a function to convert the list to the string
def listToString(s):
    str1 = ""
    for string in s:
        str1 += string
    return str1

#define a display function to get the correct format
def display(all_data):
    print('|First Name',' '*3,'|Last Name',' ','|ID',' '*8,'|Phone Number',' '*3,'|Date',
          ' '*3,'|Gender',' '*3,'|Nation',' '*3,'|Blood|')
    print('-'*100)
    for i in range(len(all_data)):
        print('|',all_data[i][0],' '*5,'|',all_data[i][1],' '*5,'|',all_data[i][2],' ','|',all_data[i][3],
              ' '*5,'|',all_data[i][4],' '*5,'|',all_data[i][5],' '*5,'|',all_data[i][6],
              ' '*5,'|',all_data[i][7],'|')
def option1():
    #open a file for reading
    infile = open("data.txt", "r")
    personName=getName()
    idNumber= getIdNumber(10)
    phoneNmber = getPhoneNumber(10)
    date = getDate()
    gender=getGender()
    nation = getCountry()
    blood = getBlood()
    
    lines = infile.readlines()
    # a loop for listiong the date in a list , handling the error of repated id
    for line in lines:
        info = line.rstrip().split(";")
        while info[2] == idNumber:
            print("Error: Already exist")
            idNumber= getIdNumber(10)
     #closing the file to avoid data lose    
    infile.close()
    # open a file for writing 
    infile = open("data.txt","w")
    data = personName+";"+idNumber+";"+phoneNmber+";"+str(date)+";"+gender+";"+nation+";"+ blood
    for line in lines:
        infile.write(line)
    infile.write(str(data + "\n"))    
    infile.close()
 # define  functions to sort by id  , gender , first name  
def sortbyID(all_data):
    for i in range(0,len(all_data)):
        for j in range(i+1,len(all_data)):
            if all_data[j][2] < all_data[i][2]:
                all_data[i],all_data[j] =all_data[j],all_data[i]
    return all_data

#define a function for sorting ny first name                
def sortbyFN(all_data):
    
    for i in range(0,len(all_data)):
        for j in range(i+1,len(all_data)):
            if all_data[j][0] < all_data[i][0]:
                all_data[i],all_data[j] =all_data[j],all_data[i]
    return all_data  

# define a function for sorting by gender
def sortbyGender(all_data):
    for i in range(0,len(all_data)):
        for j in range(i+1,len(all_data)):
            if all_data[j][5] < all_data[i][5]:
                all_data[i],all_data[j] =all_data[j],all_data[i]
    return all_data

def option2():
    
    infile = open("data.txt", "r")
    lines = infile.readlines()
    count = 0
    # an empty list to store the date on it
    all_data=[]
    for line in lines:
        info = line.rstrip().split(";")
        # to append the date on the list
        all_data.append(info)
        
    for all_datai in all_data:
        print(all_datai)
      #closing the file to avoid losing data  
    infile.close()
    print('1 - Sorting by ID.\n2 - Sorting by First Name.\n3 - Sorting by Gender.')
    opt = int(input('Enter your choice : '))
    #if functions to take the option from the user , handling the error
    if opt == 1:
        all_data = sortbyID(all_data)
        display(all_data)
    elif opt == 2:
        all_data = sortbyFN(all_data)
        display(all_data)
    elif opt == 3:
        all_data = sortbyGender(all_data)
        display(all_data)
    else:
        # error if its not valid 
        print('Enter valid choice!!')
        option2()

# a function for the format
def displaySpecfic(all_data):
    print('|First Name',' '*3,'|Last Name',' ','|ID',' '*8,'|Phone Number',' '*3,'|Date',
          ' '*3,'|Gender',' '*3,'|Nation',' '*3,'|Blood|')
    print('-'*100)
    print('|',all_data[0],' '*5,'|',all_data[1],' '*5,'|',all_data[2],' ','|',all_data[3],
            ' '*5,'|',all_data[4],' '*5,'|',all_data[5],' '*5,'|',all_data[6],
            ' '*5,'|',all_data[7],'|')    

def option3():
    #open a file for reading
    infile = open("data.txt", "r")
    lines = infile.readlines()
    infoById = input("Enter an ID: ")
    option = -1
    count = 0
    for line in lines:
        info = line.rstrip().split(";")
        if info[2] == infoById:
            displaySpecfic(info)
            break
        count += 1
     # a loop for asking if the user wants to delete or update information   
    while option != '0':
        try:
            print(" ")
            print("1.Update person information")
            print("2.Delete person information")
            print("0.Back to the main menu")
            option = input("Enter option: ")   
            if int(option) > 2 or int(option) < 0:
                print("Please enter a valid option")                   
        except ValueError:
            print("Please enter a valid option")    
        if option == '1':
            #lines[count] = getName() + ';' + getIdNumber(10) + ';' + getPhoneNumber(10) + ';' + str(getDate()) + 
            #';' + getGender() + ';' + getCountry() + ';' + getBlood() + '\n'
            option1 = -1              
            # a loop for letting the user enter his choice
            while option1 != '0':
                # to handle the error
                try:
                    print(info)
                    print("Choose what you want to change:")
                    print("1. Name")
                    print("2. Mobile Number")
                    print("3. Blood Type")
                    print("4. Date of birth")
                    print("5. Gender")
                    print("6. Country")
                    print("0. Leave")
                    option1 = input("Enter an option: ")
                    # if its a not vaild option but its a number , we print the message
                    if int(option1) > 6 or int(option1) < 0:
                        print("Please enter a valid option")
                        # if the user didnt enter a value , error message.
                except ValueError:
                    print("Please enter a valid option")
                data = info[0]+';'+info[1]+';'+info[2]+';'+info[3]+';'+info[4]+';'+info[5]+';'+info[6]+';'+info[7]+'\n'
                newData = data
                # depending in which the user want to change 
                if option1 == '1':
                    newName = getName()
                    newName = newName.rstrip().split(';')
                    info[0] = newName[0]
                    info[1] = newName[1]
                    lines[count] = newData
                    infile = open('data.txt', 'w')
                    infile.write((listToString(lines) + '\n'))
                    infile.close()
                elif option1 == '2':
                    newPhone = getPhoneNumber(10)
                    info[3] = newPhone
                    lines[count] = newData
                    infile = open('data.txt', 'w')
                    infile.write((listToString(lines) + '\n'))
                    infile.close()
                elif option1 == '3':
                    newBlood = getBlood()
                    info[7] = newBlood
                    lines[count] = newData
                    infile = open('data.txt', 'w')
                    infile.write((listToString(lines)))
                    infile.close()
                elif option1 == '4':
                    newDate = getDate()
                    info[4] = str(newDate)
                    lines[count] = newData
                    infile = open('data.txt', 'w')
                    infile.write((listToString(lines)))
                    infile.close()
                elif option1 == '5':
                    newGender = getGender()
                    info[5] = newGender
                    lines[count] = newData
                    infile = open('data.txt', 'w')
                    infile.write((listToString(lines)))
                    infile.close()
                elif option1 == '6':
                    newCountry = getCountry()
                    info[6] = newCountry
                    lines[count] = newData
                    infile = open('data.txt', 'w')
                    infile.write((listToString(lines)))
                    infile.close()
            #infile = open('data.txt', 'w')
            #infile.write(listToString(lines)+ '\n')
            print("Information is updated successfully.")
            infile.close()
        # if the user want to remove a person            
        elif option == '2':
            lines[count] = ''
            print("Data after the remove:")
            print(listToString(lines).replace(';','|'))
            infile = open('data.txt', 'w')
            infile.write((listToString(lines)))
            infile.close()
    infile.close()                    
option = -1
# a loop to take the option from the user
while option !=4:
    try:
        print(" ")
        print("Enter 1 to add a new person: ")
        print("Enter 2 to Display information for All persons: ")
        print("Enter 3 to Display information for a specific person ( update – delete): ")
        print("Enter 4 to exit: ")
        print(" ")
        option = int(input("Enter option: "))
        if option > 4 or option < 1:
            #error if it is >4 or < 1
            print("Please enter a valid option")
            #error if its not a number
    except ValueError:
        print("Please enter a valid option")
    #call the functions
    if option == 1:
        option1()
    elif option == 2:
        option2()
    elif option == 3:
        option3()
```

     
    Enter 1 to add a new person: 
    Enter 2 to Display information for All persons: 
    Enter 3 to Display information for a specific person ( update – delete): 
    Enter 4 to exit: 
     
    Enter option: 1
    Your First Name: Raed
    Your Last Name: Alshehri
    Your id number: 201937930
    Please enter a vaild number
    Your id number: 1105695116
    Your phone number: 055443019
    Please enter a vaild number
    Your phone number: 0554430197
    Enter your date of birth (M/D/Y): 11/12/1999
    Your gender (Male/Female): Male
    Your nationality: Saudi
    Your blood type:A-
     
    Enter 1 to add a new person: 
    Enter 2 to Display information for All persons: 
    Enter 3 to Display information for a specific person ( update – delete): 
    Enter 4 to exit: 
     
    Enter option: 2
    ['Ahmed', 'Alghamdi', '1020304010', '0534342615', '4/10/1978', 'MALE', 'KSA', 'A+']
    ['Nora', 'Alqahtani', '1020304020', '0563437811', '3/20/2000', 'FEMALE', 'UAE', 'A-']
    ['Ziad', 'Alshaikh', '1020304030', '0557636431', '12/12/1995', 'MALE', 'KWT', 'A+']
    ['Aymen', 'Qasim', '1020304040', '0546988888', '1/30/2000', 'MALE', 'KSA', 'O+']
    ['Mohammad', 'Alotabie', '1020304050', '0552190134', '6/6/2001', 'MALE', 'UAE', 'O+']
    ['apdallah', 'alyoupi', '2019383500', '0546997759', '12/24/2001', 'MALE', 'KSA', 'A+']
    ['Raed', 'Alshehri', '1100000000', '0554430197', '11/12/1999', 'MALE', 'SAUDI', 'A-']
    ['Raed', 'Alshehri', '1105695116', '0554430197', '11/12/1999', 'MALE', 'SAUDI', 'A-']
    1 - Sorting by ID.
    2 - Sorting by First Name.
    3 - Sorting by Gender.
    Enter your choice : 3
    |First Name     |Last Name   |ID          |Phone Number     |Date     |Gender     |Nation     |Blood|
    ----------------------------------------------------------------------------------------------------
    | Nora       | Alqahtani       | 1020304020   | 0563437811       | 3/20/2000       | FEMALE       | UAE       | A- |
    | Ahmed       | Alghamdi       | 1020304010   | 0534342615       | 4/10/1978       | MALE       | KSA       | A+ |
    | Ziad       | Alshaikh       | 1020304030   | 0557636431       | 12/12/1995       | MALE       | KWT       | A+ |
    | Aymen       | Qasim       | 1020304040   | 0546988888       | 1/30/2000       | MALE       | KSA       | O+ |
    | Mohammad       | Alotabie       | 1020304050   | 0552190134       | 6/6/2001       | MALE       | UAE       | O+ |
    | apdallah       | alyoupi       | 2019383500   | 0546997759       | 12/24/2001       | MALE       | KSA       | A+ |
    | Raed       | Alshehri       | 1100000000   | 0554430197       | 11/12/1999       | MALE       | SAUDI       | A- |
    | Raed       | Alshehri       | 1105695116   | 0554430197       | 11/12/1999       | MALE       | SAUDI       | A- |
     
    Enter 1 to add a new person: 
    Enter 2 to Display information for All persons: 
    Enter 3 to Display information for a specific person ( update – delete): 
    Enter 4 to exit: 
     
    Enter option: 4
    


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

