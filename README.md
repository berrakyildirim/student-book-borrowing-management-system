# Student Borrowing Management System

A hash table–based library borrowing system implemented in C

## Overview

This project implements a Student Borrowing Management System using a hash table with multiple collision–resolution techniques.
The program reads borrowing records from a file, stores students and their borrowed books efficiently, and provides functionality for searching, printing, and returning books.

The system supports:

- Linear probing

- Quadratic probing

- Double hashing

- It also includes rehashing, dynamic resizing, and linked list management for each student's borrowed books.

## Features

### Hash Table Operations

Insert students and update existing records

Handle collisions with linear, quadratic, or double hashing

Automatic rehashing when load factor > 0.5

Prime-number table resizing

### Student Operations

Search students by ID

Print all students in the hash table

Return (delete) a borrowed book entry

Track number of borrowed books

### File Input

Reads from a semicolon-separated file borrowed_books.txt with the format:

StudentID;StudentName;BorrowID;BookTitle;Author;BorrowDate


Header is skipped automatically.

### Data Structures 

BorrowRecord (Linked List Node)

Each borrowed book is stored in a linked list node:

typedef struct BorrowRecord {
    char borrowID[20];
    char bookTitle[200];
    char author[300];
    char borrowDate[20];
    struct BorrowRecord* next;
} BorrowRecord;


**Each student has:**

- ID

- Name

- Borrowed book linked list

- Borrow count


typedef struct {
    int studentID;
    char studentName[50];
    BorrowRecord* borrowList;
    int borrowCount;
} Student;


**One entry in the hash table:**


typedef struct {
    int isOccupied;
    Student student;
} HashEntry;

## Available Menu Options

When the program starts, users select the collision resolution method.
Then the menu offers:

1. Print Hash Table
2. Search Student
3. Return Book
0. Exit

## Key Algorithms

**Key Computation:**

- Product of digits (0 treated as 1):

- key = product of all digits of studentID

**Hash Functions:**

- hash1 = key % size

- hash2 = 7 - (key % 7) (for double hashing)

**Collision Handling:**

- Linear probing → h1 + i

- Quadratic probing → h1 + i²

- Double hashing → h1 + i * h2

**Rehashing:**

Triggered when:

- Load factor > 0.5


New table size:

- next_prime(old_size * 2)

## How to Run

Compile the program:

gcc main.c -o borrowing_system


Make sure the file borrowed_books.txt exists in the same directory.

**Run:**

./borrowing_system

📁 Example borrowed_books.txt
StudentID;StudentName;BorrowID;BookTitle;Author;BorrowDate
245646;Burak;B104;Algorithms;CLRS;12/03/2024
269739;Ahmet;B208;Data Structures;Weiss;15/04/2024

## Notes

Memory is dynamically allocated for each borrow record.

Returned books are properly freed from memory.

Rehashing maintains the integrity of all linked lists.

## Author

Developed as part of a data structures and hashing coursework project, focusing on:

- Hash tables

- Collision resolution

- Dynamic rehashing

- Linked lists

- File parsing

- Efficient data lookup systems
