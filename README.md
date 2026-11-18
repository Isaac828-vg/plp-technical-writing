SOFTWARE ENGINEERING ESSENTIALS

DAY 4: TECHNICAL WRITING ASSIGNMENT

Student Name: Isaac Ladu James


EXERCISE A: USER MANUAL

Creating and Activating a Python Virtual Environment Using Termux on Android

1. Introduction

This exercise explains how to create and activate a Python virtual environment using Termux on an Android phone. It also demonstrates how to install a Python package, verify the installation, and deactivate the virtual environment.

A Python virtual environment allows programmers to manage packages separately for different projects. This helps prevent conflicts between packages used in different projects.

2. Prerequisites

Before starting this exercise, the following requirements are needed:

- An Android smartphone.
- Termux installed on the phone.
- Python installed in Termux.
- An active internet connection.
- Basic knowledge of typing commands in a terminal.

3. Step-by-Step Procedure

Step 1: Open Termux

Action: Open the Termux application on the Android phone.

Expected result: The Termux terminal opens and displays a command prompt.

Step 2: Check the Python version

Action: Enter the following command:

python --version

Expected result: The installed Python version appears.

Actual result:

Python 3.13.13

Step 3: Confirm the project directory

Action: Enter the following command:

pwd

Expected result: The terminal displays the current working directory.

Actual result:

/data/data/com.termux/files/home/my_python_project

This confirms that I was already inside my project folder.

Step 4: Create the virtual environment

Action: Enter the following command:

python -m venv venv

Expected result: A virtual environment named "venv" is created inside the project folder without an error.

Step 5: Activate the virtual environment

Action: Enter the following command:

source venv/bin/activate

Expected result: The terminal prompt displays "(venv)", showing that the virtual environment is active.

Step 6: Install the Requests package

Action: Enter the following command:

python -m pip install requests

Expected result: The Requests package and its required dependencies are installed successfully.

Step 7: Verify the package installation

Action: Enter the following command:

python -m pip show requests

Expected result: The terminal displays information about the installed package.

Actual result:

Name: requests
Version: 2.34.2
Location: /data/data/com.termux/files/home/my_python_project/venv/lib/python3.13/site-packages

This confirms that the package was installed inside the virtual environment.

Step 8: Test the Requests package

Action: Enter the following command:

python -c "import requests; print(requests.__version__)"

Expected result: The terminal displays the installed package version.

Actual result:

2.34.2

This confirms that Python can successfully import the Requests package.

Step 9: Deactivate the virtual environment

Action: Enter the following command:

deactivate

Expected result: The "(venv)" prefix disappears from the terminal prompt.

Actual result:

~/my_python_project $

This confirms that the virtual environment has been deactivated successfully.

4. Screenshot Descriptions

Screenshot 1: Checking Python and the project directory



Screenshot 2: Activating the virtual environment




Shows the Termux terminal displaying "(venv)" after successful activation.

Screenshot 3: Installing and verifying the Requests package


Screenshot 4: Testing and deactivating the environment



5. Troubleshooting

Problem: Unable to install the Requests package.


During the exercise, my first installation attempt displayed this error:

ERROR: Could not find a version that satisfies the requirement requests

ERROR: No matching distribution found for requests

Possible causes:

- Unstable internet connection.
- Temporary connection problems with the Python Package Index (PyPI).
- Incorrect pip package index configuration.

Solution:

First, I checked whether the PyPI website was reachable by running:

curl -I https://pypi.org

The terminal returned an HTTP 200 response, confirming that the website was reachable.

I then retried the installation using:

python -m pip install requests

The package was installed successfully.

This taught me to check the internet connection and retry package installation when an error occurs.

6. Conclusion

I successfully created and activated a Python virtual environment using Termux on Android. I installed the Requests package, verified its installation, tested that Python could import it, and deactivated the environment.

Through this exercise, I learned how virtual environments help organise Python projects and manage their dependencies independently.



EXERCISE B: API REFERENCE DOCUMENTATION

Project Management API – Create a Task Endpoint

1. Introduction

This section provides API reference documentation for a hypothetical project management application.

The API allows an authenticated user to create a new task within an existing project. The documentation explains the endpoint, parameters, authentication requirements, HTTP response codes, and examples of requests and responses.

2. HTTP Method and Endpoint

API Name: Project Management API

Endpoint: Create a Task

HTTP Method: POST

URL Path:

/api/v1/projects/{project_id}/tasks

Description:

This endpoint allows an authenticated user to create a new task within an existing project.

3. API Parameters

3.1 Path Parameters

Parameter| Data Type| Required| Description
project_id| Integer| Yes| The unique ID of the project where the task will be created.

3.2 Query Parameters

This endpoint does not require any query parameters.

3.3 Request Body Parameters

The request body must be provided in JSON format.

Parameter| Data Type| Required| Description
title| String| Yes| Name of the task.
description| String| No| Additional information about the task.
assignee_id| Integer| Yes| ID of the person assigned to the task.
due_date| String| Yes| Task deadline in YYYY-MM-DD format.
priority| String| Yes| Priority level. Accepted values are low, medium, and high.

4. Required Headers and Authentication

The API requires the following HTTP headers:

Header| Required| Description
Content-Type| Yes| Specifies that the request body is in JSON format.
Authorization| Yes| Contains the Bearer access token used to authenticate the user.
Accept| Yes| Specifies that the client expects a JSON response.

Authentication Method:

Bearer Token Authentication is required. The user must provide a valid access token in the Authorization header.

Example:

Authorization: Bearer YOUR_ACCESS_TOKEN

5. HTTP Response Codes

The API may return the following HTTP status codes:

Status Code| Name| Explanation
201| Created| The task was successfully created.
400| Bad Request| The request contains invalid or improperly formatted data.
401| Unauthorized| The user has not provided a valid authentication token.
403| Forbidden| The user does not have permission to create tasks in the project.
404| Not Found| The specified project does not exist.
409| Conflict| The request conflicts with the current state of the project.
415| Unsupported Media Type| The request uses an unsupported content type.
422| Unprocessable Entity| The submitted data has validation errors, such as an invalid date or priority.
500| Internal Server Error| An unexpected error occurred on the server.

6. Example API Request

The following example shows how a client sends a request to create a task in project 101.

HTTP Request:

POST /api/v1/projects/101/tasks HTTP/1.1
Host: api.example.com
Content-Type: application/json
Authorization: Bearer YOUR_ACCESS_TOKEN
Accept: application/json

Request Body (JSON):

{
  "title": "Prepare project documentation",
  "description": "Write and review the technical documentation for the project.",
  "assignee_id": 25,
  "due_date": "2026-12-15",
  "priority": "high"
}

Explanation:

- "title": The name of the task.
- "description": Details about the work to be completed.
- "assignee_id": Identifies the person responsible for the task.
- "due_date": Specifies the task deadline.
- "priority": Indicates the importance of the task.

7. Example Successful API Response

When the server successfully creates the task, it returns the HTTP status code "201 Created".

HTTP Response:

HTTP/1.1 201 Created
Content-Type: application/json

Response Body (JSON):

{
  "success": true,
  "message": "Task created successfully",
  "data": {
    "task_id": 501,
    "project_id": 101,
    "title": "Prepare project documentation",
    "description": "Write and review the technical documentation for the project.",
    "assignee_id": 25,
    "due_date": "2026-12-15",
    "priority": "high",
    "status": "pending",
    "created_at": "2026-11-18T09:30:00Z"
  }
}

Explanation:

- "success": Indicates that the request was successful.
- "message": Confirms that the task was created.
- "task_id": Unique identification number assigned to the new task.
- "project_id": Identifies the project containing the task.
- "title": Name of the created task.
- "assignee_id": Identifies the person responsible for the task.
- "due_date": Shows the task deadline.
- "priority": Indicates the task priority.
- "status": Shows the current task status.
- "created_at": Records when the task was created.

8. Conclusion

This API reference documentation explains how an authenticated user can create a task in a project management application.

It describes the HTTP method, endpoint path, parameters, authentication requirements, possible response codes, and examples of request and response formats.

This documentation helps developers understand how to use the API and communicate with the project management application correctly.


GENERAL CONCLUSION

Through these two exercises, I developed practical skills in technical writing and software documentation.

In Exercise A, I learned how to create and manage a Python virtual environment using Termux on Android, install a package, and verify that it works.

In Exercise B, I learned how to document an API endpoint, explain its parameters and authentication requirements, and provide examples of JSON requests and responses.

These activities improved my understanding of software development procedures and the importance of clear technical documentation.
