# Design Document

## TApp


## Table of Contents
- [Design Document](#design-document)
  - [## TApp](#-tapp)
  - [Table of Contents](#table-of-contents)
    - [Document Revision History](#document-revision-history)
- [1. Introduction](#1-introduction)
- [2.	Architectural and Component-level Design](#2architectural-and-component-level-design)
  - [2.1 System Structure](#21-system-structure)
  - [2.2 Subsystem Design](#22-subsystem-design)
    - [2.2.1 Model](#221-model)
    - [2.2.2 Controller](#222-controller)
    - [2.2.3 View and User Interface Design](#223-view-and-user-interface-design)
- [3. Progress Report](#3-progress-report)
- [4. Testing Plan](#4-testing-plan)
- [5. References](#5-references)

<a name="revision-history"> </a>

### Document Revision History

| Name | Date | Changes | Version |
| ------ | ------ | --------- | --------- |
|Revision 1 |2021-10-05 |Initial draft | 1.0        |
|      |      |         |         |
|      |      |         |         |


# 1. Introduction

This document is to provide a more indepth and speciic plan for how our application will actually be designed, rquirements met, and use cases implimented. 

This document details how our application, a web app for teachers and students to assign and organize TAs for course, will be implimented. Aswell as in the future, how it has been implimented. We will include component diagrams, UI sketches, and flow charts detailing how we plan to create this app.

section 2 covers design schematics and other functional plans. Detailing classes, how they are related, how the controller operates, and other implimentation. 

section 3 covers  progress done, this lets you keep up with current development, and allows you to follow previous progress chronologically. 

section 4 will cover testing plans for future, more robust iterations of our application

section 5 will include various resources that was used in the creation of this product as either a direct aid or conceptual crutch

# 2.	Architectural and Component-level Design
## 2.1 System Structure

![UML class (2)](https://user-images.githubusercontent.com/112023644/197697077-1c97d86a-9ab7-4243-9fd1-b9e0d794570f.png)

The type of high-level archittecture we use for this prohect is, the Model-View-Controller (MVC) pattern.
The model view controller was a architect strucutre that we have all used int he past and best fit for this project as well. 
Are project code is also split up in away where we have categories for Model (model.py), Controllers (forms/routes.py), and View (html files)

Subsystems and roles:
  login: login users
  logout: logoit users
  create_student/create_facutly: create account of that type
  index: disaplays the form of user type
  create_ta_positions: create TA positions for students to apply to
 
In order to reduce coupling we used encapsultation in order to reduce dependecies between classes. In order to increase cohesion we kept aspect of subsytems with smiliar roles related and easy to understand. For example naming coneventions. We also have high reusabiltiy where we reuse classes like courses and major in different places instead of making completey new classes.  
  

## 2.2 Subsystem Design 

### 2.2.1 Model

Models:

**User**
This table stores all the user date
The user class is used for the sole purpose of storing personal information pertaining to the user

**Faculty**
This table store faculty user data 

**Student**
This table stores student user data

**TAPosition**
TAPositions is the table to stores every position created by a faculty memebr that a student can apply for

**Major**
Model for all majors. Majors are related to students (one-to-many)

**Course**
The model for all courses. Is related to TAPositions(one-to-many)

**Application**
The relationship table between students and TAPositions (one-to-one)

UML Diagram 

![UMLclassdiagram](https://user-images.githubusercontent.com/112040580/201834244-2b149a2c-c8f2-4bd2-94fa-fa28025015b1.png)

### 2.2.2 Controller

Controller contains all the subsystems located in the auth_routes.py or routes.py

|   | Methods           | URL Path   | Description  |
|:--|:------------------|:-----------|:-------------|
|1. | 'GET'| /index|  Sends the user to the index html. If the user is not logged they're redirected to a login page, if they are a student this displays open TA positions with the option to apply, otherwise for faculty this displays applications from students to TA for those positions and the status of those applications |
|2. | 'GET'|/viewprofile|    This will render the current users profile showing all the data in that users class, this is somewhat dynamic, changing information displayed depending on if the user is a faculty member or student. if no user is logged in this will redirect to the /login route.|          |
|3. |'POST'|/accept/\<appid>| This will be used to by teachers to accept students applications, this requires the user to be logged in, to have posted the course the application has a relationship to, and the course to have open TA positions remaining |
|4. |'GET', 'POST'|/create_ta_position|This will be used by teachers to create TA positions for students to the apply for, users must be logged in to a faculty account to use.|
|5. |'GET', 'POST'|/register_student|This will render the student register page template. This page will have a register form that will be used to create a new student user instance to be added to the database|
|6. |'GET', 'POST'|/register_faculty|This will render the faculty register page template. This page will have a register form that will be used to create a new faculty user instance to be added to the database|
|7. |'GET', 'POST'|/login|This will render the login page template. It will contain a login form that will be passed to the template. It will also check if the user logging in is a faculty user or student user.|
|8. |'GET'|/logout|This will log the current user out and redirect back to the /login route|
|9. |'GET'|/viewstudent/\<studentid>|renders an applicants information for a logged in faculty member, if not studentid does not respond to an applicant for the faculty, or if the user is not logged in, this will redirect with an appropriate flash message|

### 2.2.3 View and User Interface Design 

UI Sketches:

![TeamProjectSketches](https://user-images.githubusercontent.com/112023644/195495849-f1462c34-8cdc-40cd-835e-39f0f4dfee25.png)
![Untitled](https://user-images.githubusercontent.com/112023644/195495870-6b2783b4-19fb-4124-bc6c-1b8009bc6c2c.png)
Student Index View:
![image](https://user-images.githubusercontent.com/104106520/201860716-f30a4aa8-727d-4156-91cb-2ebbbd41093b.png)
Students Applications View:
![image](https://user-images.githubusercontent.com/104106520/201861083-895be50d-1a2d-4714-82a2-4cbabfef6bf3.png)
Faculty Index View:
![image](https://user-images.githubusercontent.com/104106520/201861352-08912b46-f279-4f6a-a154-33467412444c.png)
TA Position Creation:
![image](https://user-images.githubusercontent.com/104106520/201861553-5dd6ec9f-9fdf-4a24-a294-3d0e949467c8.png)
Application Creation:
![image](https://user-images.githubusercontent.com/104106520/201862247-d1cbf435-c955-4738-a8e7-ea0e59cfde13.png)


  
The view is how the page is formatted and data is is displayed on said page. As of right now in interation 1 we haven't used any external libraries/framework but plan to use Bootstrap for future iterations.

Included pages for Iteration 1:
  - base.html
    - bar with options to go to different pages
  - createtaposition.html
    - allows Faculty to create ta positions
  - login.html
    - login for both Faculty and Students
  - registerFaculty.html
    - Register as a faculty member
  - registerStudent.html
    - Register as a student member
  - index.html:
    - displays the form of the index page based on user type


Iteration 2:
  - viewprofile.html
    - displays profile of user
  - applyposition.html
    - Allows student to apply to a ta role
  - yourapps.html
    - displays all pending applications to a faculty user


Future Iterations:
  - studentlist.html
    - displays all students applied for TA positions if the faculty member's class
  - studentassign.html
    - assign students to TA roles
  - viewposition.html
    - shows all available ta positions for students


# 3. Progress Report

In iteration 1, the main difficulties our team faced was minimum communication and procrastination. Our team did not meet nearly enough to plan the development of the software. This lead to alot of confusion and problems with each member's assigned parts. The features implemented in this iteration are: User Log In, User Registration, Faculty able to create TA positions. 
In the future, we will be meeting more to plan as well as pushing eachother to complete tasks on time.
  
Iteration 1 branch:
https://github.com/WSU-CptS322-Fall2022/termproject-the-boys/tree/Iteration1.git

In iteration 2, things went better than last time. However, there is still not as much communication as we would have liked, as well as a little too much procrastination going on. All things considered, the workflow for this iteration was quite smoother. Features implemented in this iteration include:
- Viewing posts for TA positions with all the correct info.
- Applying for the TA positions
- Viewing user profile with correct info


# 4. Testing Plan

We will most likely be testing the functionality of student and faculty users separately. With each user type logged in, we check the interactions between all the routes. We'll also do this with no user logged in. For testing, we will probably use Unittest or PyTest.

Functional tests will be written specifically for each test that will pass when the use case is satisfied. These will be from the perspective of the user in the case and will go through the steps of the case until we get to the result.

Manual inspection will be done of each webpage for any visual bugs. These include poorly sized ui objects. 


# 5. References

draw.io (uml sketches)

----
