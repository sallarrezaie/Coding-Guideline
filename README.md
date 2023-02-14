# Coding Guideline
# Arootah

## Description

An in-depth approach to best practices for GitHub and Django Rest Framework

## Django Rest Framework (DRF)

### Basic Guideline

*	Use class-based views instead of function-based views.
*	Follow the PEP 8 style guide for code formatting and style conventions.
*	Use serializers to handle the serialization and deserialization of data.
*	Use ViewSets and Routers to map URLs to views and reduce boilerplate code.
*	Use pagination to handle large datasets and improve performance.
*	Use permissions and authentication to control access to your API endpoints.
*	Use filters, ordering, and searching to provide flexible querying of your data.
*	Use testing to verify the functionality of your API and catch bugs early.
*	Use HTTP status codes appropriately to communicate the status of requests and responses.
*	Use versioning to handle changes to your API over time.
*	Use third-party packages when appropriate, such as Django-filter for advanced filtering options or DRF-extensions for additional functionality.
*	Use serializers with custom validation to ensure that data received by your API is valid and meets your requirements.
*	Use class-based authentication and permission classes to handle complex access control scenarios.
*	Use custom exceptions to handle errors and provide meaningful error messages to API clients.
*	Use caching to improve the performance of your API by reducing the number of database queries.
*	Use middleware to handle cross-cutting concerns, such as request logging or rate limiting.
*	Use Django signals to trigger actions based on changes to your models, such as sending notifications or performing background tasks.
*	Use Docker to create isolated development and production environments.
*	Use performance profiling tools to identify and optimize slow code.

### Performance Guideline

*	Use the select_related() method to retrieve related objects in a single query, instead of making separate queries for each related object.
*	Use the prefetch_related() method to retrieve related objects in a separate query, which can be more efficient for ManyToMany or reverse ForeignKey relationships.
*	Use the values() or values_list() methods to retrieve only the specific fields you need, instead of retrieving the entire object.
*	Use indexes to speed up database queries for commonly used fields, especially if they are used for filtering or ordering.
*	Use Django's built-in caching framework or third-party caching solutions to reduce the number of database queries.
*	Use the annotate() method to perform aggregate calculations on your data, instead of performing them in Python code.
*	Use the SerializerMethodField to perform complex calculations or retrieve related objects in a more efficient manner than using nested serializers.
*	Use the count() method to retrieve the number of objects that match a certain filter, instead of retrieving the entire queryset and counting in Python code.
*	Use the QuerySet.defer() or QuerySet.only() methods to retrieve only the required fields for a query, which can reduce the amount of data transferred between the database and application.
*	Use a performance profiling tool, such as Django Debug Toolbar, to identify and optimize slow queries in your code.

### Testing Guideline
*	Use the Django test framework to write unit tests for your API endpoints.
*	Use the APIClient provided by DRF to simulate API requests in your tests.
*	Write test cases for each API endpoint, including tests for different HTTP methods and different input parameters.
*	Use fixtures or factories to create test data for your tests.
*	Use assert statements to verify that the expected response is returned for each test case.
*	Test error cases, such as invalid input parameters or unauthorized access, to ensure that your API behaves as expected.
*	Use test coverage tools, such as coverage.py, to identify areas of your code that are not covered by your tests.
*	Use test-driven development (TDD) practices to ensure that new features or changes are tested before they are added to your codebase.

#### Example of a Complete Unit Test for a REST Endpoint
```
from rest_framework.test import APITestCase
from rest_framework import status
from django.urls import reverse

class MyAPIEndpointTestCase(APITestCase):
    def test_get_all_objects(self):
        url = reverse('my-api-endpoint')
        response = self.client.get(url, format='json')
        self.assertEqual(response.status_code, status.HTTP_200_OK)
        self.assertEqual(len(response.data), 3)

    def test_create_object(self):
        url = reverse('my-api-endpoint')
        data = {'name': 'New object', 'description': 'Test object'}
        response = self.client.post(url, data, format='json')
        self.assertEqual(response.status_code, status.HTTP_201_CREATED)
        self.assertEqual(response.data['name'], 'New object')

    def test_update_object(self):
        url = reverse('my-api-endpoint', kwargs={'pk': 1})
        data = {'name': 'Updated object', 'description': 'Test object'}
        response = self.client.put(url, data, format='json')
        self.assertEqual(response.status_code, status.HTTP_200_OK)
        self.assertEqual(response.data['name'], 'Updated object')

    def test_delete_object(self):
        url = reverse('my-api-endpoint', kwargs={'pk': 1})
        response = self.client.delete(url, format='json')
        self.assertEqual(response.status_code, status.HTTP_204_NO_CONTENT)
```

### Notes on Coverage Testing

* Install the coverage package using pip: ``` pip install coverage ```

* Create a .coveragerc file in the root directory of your project. This file allows you to configure the behavior of coverage, such as which files to include and exclude from coverage, and how to generate reports. Here's an example .coveragerc file:

```
[run]
source = myapp/
omit =
    */migrations/*
    */tests/*
    */admin.py
    */apps.py
branch = True

[report]
show_missing = True
precision = 2
```

* This configuration tells coverage to only consider the myapp/ directory for coverage, exclude migrations, tests, admin.py, and apps.py files from coverage, and enable branch coverage. It also tells coverage to show missing lines in the coverage report, and to display coverage percentages with two decimal places.
* Run your test suite with coverage. To do this, use the coverage command-line tool in conjunction with the manage.py command to run your test suite. This will run your test suite with coverage enabled, and generate a coverage report. For example:

```
coverage run manage.py test
```

* Generate a coverage report. After running your test suite with coverage, you can generate a coverage report using the coverage report command. This will display a detailed report of your coverage, including which lines of code were executed and which were not, as well as branch coverage information. For example:

```
coverage report
```

* This will display a report similar to the following:

```
Name            Stmts   Miss Branch BrPart  Cover
---------------------------------------------------
myapp/models.py    10      2      2      1    75%
myapp/views.py     50      5      6      2    87%
---------------------------------------------------
TOTAL              60      7      8      3    85%

```

* This report tells you that you have 85% code coverage across your myapp directory, with 7 lines of code missing coverage. You can use this information to identify areas of your code that need additional testing.

### Notes on Docker 

* Since we are using Docker in our deployments, we must use Docker on our local machines too. 
* Don't run your own environments outside of docker when developing code as the results may be unpredictable once deployed.
* If you are having trouble running Docker locally, projects generated by Crowdbotics have a ReadME file that explains the step by step process for starting up your local environment with only a few commands
* Make sure that you are using PostGres on your local machine. Do not alter any settings to use a database system other than PostGres as that is what we are using in staging and production

### Notes on performance testing using Django Debug Toolbar
* Django Debug Toolbar is a powerful tool that can help you debug performance issues and identify potential security vulnerabilities in your Django application. Here's a guideline for using Django Debug Toolbar:

* Install the django-debug-toolbar package using ``` pip: pip install django-debug-toolbar ```
Add 'debug_toolbar' to your INSTALLED_APPS setting in settings.py:

```
INSTALLED_APPS = [
    # ...
    'debug_toolbar',
    # ...
]
```

* Add the following middleware to your MIDDLEWARE setting in settings.py:

```
MIDDLEWARE = [
    # ...
    'debug_toolbar.middleware.DebugToolbarMiddleware',
    # ...
]
```

* Start your Django development server, and the Debug Toolbar will automatically appear in the upper-right corner of your web pages.
The Debug Toolbar provides detailed information about the time and resources used by each component of your web page, including SQL queries, HTTP requests, and template rendering. You can also use the Debug Toolbar to inspect the contents of your request and response objects, view the cache and logging status, and more.

* Additionally, you can customize the Debug Toolbar to meet your specific needs, such as adding custom panels or excluding specific IP addresses from accessing the toolbar. Be sure to consult the official Django Debug Toolbar documentation for more information on customization options and best practices.

* Make sure that the toolbar is not running on production as Django Debug Toolbar will increase the latency of your API calls

## GitHub

### Basic Guideline

* The development branch is where new features and changes are added and tested before they are deployed to production. All changes should be made in a feature branch and then merged into the development branch for testing.

* Use feature branches: For each new feature or bug fix, create a new feature branch from the development branch. This keeps the development branch clean and allows multiple developers to work on different features simultaneously. When the feature is complete, the branch should be merged back into the development branch.

* Review code changes: Before merging a feature branch into the development branch, the code should be reviewed by another team member. This helps catch any potential issues and ensures that the changes meet the project's coding standards.

* Test changes in the development environment: Once the code changes have been merged into the development branch, they should be tested in a development environment. This ensures that the changes work as expected and do not introduce any new issues.

* Review changes again: Before merging the development branch into the master branch, the code changes should be reviewed again to ensure that they are ready for deployment.

* Deploy changes to production: Once the changes have been reviewed and approved, merge into the master branch and deploy the changes to the production environment.

* Monitor changes in production: After changes have been deployed to production, monitor the system to ensure that everything is working as expected. If any issues are found, they should be addressed as quickly as possible to minimize any negative impact on the end-users.
