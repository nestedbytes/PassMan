### PassMan
A simple and safe password manager
### Download
Normal <br>
[Download](https://github.com/shourgamer2/PassMan/releases/download/vr.10.0/PassMan.exe) <br>
Portable <br>
[Download](https://github.com/shourgamer2/PassMan/releases/download/port1.0.0/passmanportable.zip)
### How it works ?
This password manager stores the passwords in a file. <br>
It does not store it on any data center or server. <br>
If you want to move the passwords to another computer then open the install location copy the passman.exe and passmanager.db and  move it to a pendrive or upload it to google drive then go to your computer which you want to have the passwords make sure you have passman installed go to the install location here as well and then delete passman.exe and passmanager.db then download or move  the passman.exe and passmanger.db which is from your another computer
### Modify 
Clone <br>
``` sh 
git clone https://github.com/shourgamer2/PassMan
```
Open
``` sh 
python passman.py 
```
Open in vs code
``` sh 
code
```
Modify the code <br>
Import 
``` python
try:
    from tkinter import *
    #from ttk import *
except ImportError:  # Python 3
    from tkinter import *
    #from tkinter.ttk import *
import sqlite3
from tkinter import messagebox
```
Make the window
```python
root = Tk()
root.title("PassMan")
root.geometry("500x400")
root.minsize(600, 400)
root.maxsize(600, 400)
root.iconbitmap("appicon.ico")
root.resizable(False, False) 

frame = Frame(root, bg="#80c1ff", bd=5)
frame.place(relx=0.50, rely=0.50, relwidth=0.98, relheight=0.45, anchor = "n")
```
Make the file to store passwords
``` python
conn = sqlite3.connect("passmanager.db")
cursor = conn.cursor()
```
Make table
``` python
cursor.execute(""" CREATE TABLE IF NOT EXISTS manager (
                       app_name text,
                        url text,
                        email_id text,
                        password text
                        )
""")
```
Commit changes
``` python
conn.commit()
```
Close connection
``` python
conn.close()
```
Create submit function for database
```python
def submit():
    #connect to database
    conn = sqlite3.connect("passmanager.db")
    cursor = conn.cursor()
```
Insert Into Table
```python
if app_name.get()!="" and url.get()!="" and email_id.get()!="" and password.get()!="":
        cursor.execute("INSERT INTO manager VALUES (:app_name, :url, :email_id, :password)",
            {
                'app_name': app_name.get(),
                'url': url.get(),
                'email_id': email_id.get(),
                'password': password.get()
            }
        )
```
Message box
``` python
messagebox.showinfo("Info", "Record Added in Database!")
```
After data entry clear the text boxes
```python
app_name.delete(0, END)
        url.delete(0, END)
        email_id.delete(0, END)
        password.delete(0, END)

    else:
        messagebox.showinfo("Alert", "Please fill all details!")
        conn.close()

```
Create Query Function
```python
def query():
    #set button text
    query_btn.configure(text="Hide Records", command=hide)
    # connect to database
    conn = sqlite3.connect("passmanager.db")
    cursor = conn.cursor()

    #Query the database
    cursor.execute("SELECT *, oid FROM manager")
    records = cursor.fetchall()
    #print(records)

    p_records = ""
    for record in records:
            p_records += str(record[4])+ " " +str(record[0])+ " " + str(record[1])+ " " + str(record[2]) + " " + str(record[3])+ "\n"
        #print(record)

    query_label['text'] = p_records
    # Commit changes
    conn.commit()

    # Close connection
    conn.close()
```
Create Function to Delete A Record
```python
def delete():
    # connect to database
    conn = sqlite3.connect("passmanager.db")
    cursor = conn.cursor()

    #Query the database
    t = delete_id.get()
    if(t!=""):
        cursor.execute("DELETE FROM manager where oid = " + delete_id.get())
        delete_id.delete(0, END)
        messagebox.showinfo("Alert", "Record %s Deleted" %t)
    else:
        messagebox.showinfo("Alert", "Please enter record id to delete!")

    # Commit changes
    conn.commit()

    # Close connection
    conn.close()
```
Create Function to Update A Record
```python
def update():
    t = update_id.get()
    if(t!=""):
        global edit
        edit = Tk()
        edit.title("Update Record")
        edit.geometry("500x400")
        edit.minsize(450, 300)
        edit.maxsize(450, 300)
```
Global variables
```python
global app_name_edit, url_edit, email_id_edit, password_edit
```
create Text Boxes
```python
app_name_edit = Entry(edit, width=30)
        app_name_edit.grid(row=0, column=1, padx=20)
        url_edit = Entry(edit, width=30)
        url_edit.grid(row=1, column=1, padx=20)
        email_id_edit = Entry(edit, width=30)
        email_id_edit.grid(row=2, column=1, padx=20)
        password_edit = Entry(edit, width=30)
        password_edit.grid(row=3, column=1, padx=20)
 ```
 For the rest of the code please just visit the file and learn




