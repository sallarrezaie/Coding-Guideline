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

### Notes about Docker 

* Since we are using Docker in our deployments, we must use Docker on our local machines too. 
* Don't run your own environments outside of docker when developing code as the results may be unpredictable once deployed.
* If you are having trouble running Docker locally, projects generated by Crowdbotics have a ReadME file that explains the step by step process for starting up your local environment with only a few commands
* Make sure that you are using PostGres on your local machine. Do not alter any settings to use a database system other than PostGres as that is what we are using in staging and production

## Help

Any advise for common problems or issues.
```
command to run if program contains helper info
```

## Authors

Contributors names and contact info

ex. Dominique Pizzie  
ex. [@DomPizzie](https://twitter.com/dompizzie)

## Version History

* 0.2
    * Various bug fixes and optimizations
    * See [commit change]() or See [release history]()
* 0.1
    * Initial Release

## License

This project is licensed under the [NAME HERE] License - see the LICENSE.md file for details

## Acknowledgments

Inspiration, code snippets, etc.
* [awesome-readme](https://github.com/matiassingers/awesome-readme)
* [PurpleBooth](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)
* [dbader](https://github.com/dbader/readme-template)
* [zenorocha](https://gist.github.com/zenorocha/4526327)
* [fvcproductions](https://gist.github.com/fvcproductions/1bfc2d4aecb01a834b46)
