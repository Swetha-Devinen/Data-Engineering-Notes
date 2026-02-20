Module: A module is simply a .py file that contains functions, variables, or classes.

#create a file 
# math_utils.py
def add(a, b):
    return a + b

---and that can be used in another file
import math_utils

print(math_utils.add(5, 3))

Library:
A library is a collection of many modules.

Example libraries:

math

os

pandas

numpy

matplotlib

Eg:
import math

print(math.sqrt(25))


Errors and Exception Handling
Errors stop the program

eg:
print(10 / 0)

We handle errors using:
try:
    risky_code
except:
    handle_error

Eg:
try:
    num = int(input("Enter number: "))
    print(10 / num)
except ZeroDivisionError:
    print("You cannot divide by zero!")
except ValueError:
    print("Invalid input!")

try – except – finally
try:
    # Code that might cause error
except:
    # Code that runs if error occurs
finally:
    # Code that ALWAYS runs
Eg-
try:
    num1 = int(input("Enter numerator: "))
    num2 = int(input("Enter denominator: "))
    result = num1 / num2
    print("Result:", result)

except ZeroDivisionError:
    print("You cannot divide by zero!")

except ValueError:
    print("Please enter valid numbers!")

finally:
    print("Execution completed.")

Note: except- runs only if error occurs

finally- runs always

File Operations in Python
Opening a file:
file = open("sample.txt", "r")

r- read
w- write
a- append
r+- read + write

with open("sample.txt", "r") as file:
    content = file.read()
    print(content)

with open("sample.txt", "w") as file:
    file.write("Hello World")

CSV-Comma Separated Values
import csv

with open("data.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)

Pandas Library

Pandas is used for:

Data Analysis

Data Cleaning

Working with CSV/Excel

import pandas as pd

Database Connectivity 

SQLite is a lightweight database built into Python.