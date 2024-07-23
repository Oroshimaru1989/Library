import os
import platform

# Global list to store book information
global libraryBooks
libraryBooks = [
    {"id": 1, "title": "To Kill a Mockingbird", "author": "Harper Lee", "year": "1960"},
    {"id": 2, "title": "1984", "author": "George Orwell", "year": "1949"},
    {"id": 3, "title": "Pride and Prejudice", "author": "Jane Austen", "year": "1813"},
    {"id": 4, "title": "The Great Gatsby", "author": "F. Scott Fitzgerald", "year": "1925"}
]

# Function to display the menu and manage library operations
def manageLibrary():
    print("""
    ------------------------------------------------------
   |======================================================| 
   |======== Welcome To Library Management System =========|
   |======================================================|
    ------------------------------------------------------

Enter 1 : To View Library Books 
Enter 2 : To Add New Book 
Enter 3 : To Search Book 
Enter 4 : To Remove Book 
    """)

    try:
        userInput = int(input("Please select an option: "))
    except ValueError:
        exit("\nHy! That's Not A Number")
    else:
        print("\n")

    if userInput == 1:
        print("Library Books List\n")
        for book in libraryBooks:
            print("ID: {id}, Title: {title}, Author: {author}, Year: {year}".format(**book))

    elif userInput == 2:
        newId = int(input("Enter Book ID: "))
        newTitle = input("Enter Book Title: ")
        newAuthor = input("Enter Book Author: ")
        newYear = input("Enter Publication Year: ")
        newBook = {"id": newId, "title": newTitle, "author": newAuthor, "year": newYear}

        if newBook in libraryBooks:
            print("\nThis Book {} Already In The Database".format(newTitle))  # Error Message
        else:
            libraryBooks.append(newBook)
            print("\n=> New Book {} Successfully Added \n".format(newTitle))
            for book in libraryBooks:
                print("ID: {id}, Title: {title}, Author: {author}, Year: {year}".format(**book))

    elif userInput == 3:
        searchTitle = input("Enter Book Title To Search: ")
        found = False
        for book in libraryBooks:
            if searchTitle.lower() in book["title"].lower():
                print("\n=> Record Found: ID: {id}, Title: {title}, Author: {author}, Year: {year}".format(**book))
                found = True
        if not found:
            print("\n=> No Record Found For Book: {}".format(searchTitle))  # Error Message

    elif userInput == 4:
        removeId = int(input("Enter Book ID To Remove: "))
        bookFound = False
        for book in libraryBooks:
            if book["id"] == removeId:
                libraryBooks.remove(book)
                print("\n=> Book ID {} Successfully Deleted \n".format(removeId))
                bookFound = True
                break
        if not bookFound:
            print("\n=> No Record Found For Book ID: {}".format(removeId))  # Error Message

    elif userInput < 1 or userInput > 4:
        print("Please Enter Valid Option")

# Function to ask the user if they want to run the program again
def runAgain():
    runAgn = input("\nWant to continue y/n?: ")
    if runAgn.lower() == 'y':
        if platform.system() == "Windows":
            os.system('cls')
        else:
            os.system('clear')
        manageLibrary()
        runAgain()
    else:
        quit()

# Initial function call to start the program
manageLibrary()
runAgain()
