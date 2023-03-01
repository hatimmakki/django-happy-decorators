# Django Happy Decorators

[![Build Status](https://travis-ci.org/rodrigobdz/django-happy-decorators.svg?branch=master)](https://travis-ci.org/rodrigobdz/django-happy-decorators)
[![Coverage Status](https://coveralls.io/repos/github/rodrigobdz/django-happy-decorators/badge.svg?branch=master)](https://coveralls.io/github/rodrigobdz/django-happy-decorators?branch=master)
[![PyPI version](https://badge.fury.io/py/django-happy-decorators.svg)](https://badge.fury.io/py/django-happy-decorators)
[![Documentation Status](https://readthedocs.org/projects/django-happy-decorators/badge/?version=latest)](https://django-happy-decorators.readthedocs.io/en/latest/?badge=latest)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)


# Overview

Happy decorators for Django is a set of decorators for Django apps and views to make your life easier.


# Decorators

- `rate_limit`: Rate limit a view function based on IP address, user or all requests.


# Installation

You can install Django Rate Limit using pip:

`pip install django_happy_decorators`


# Rate Limit
## Usage

To use the rate_limit decorator, import it from the package and apply it to a view function. The decorator accepts three parameters: num_requests, time_frame and redirect_url.

```python
from django_happy_decorators.decorators.rate_limit import rate_limit

# Only add this line 👇 to limit the number of requests to the view
@rate_limit(num_requests=100, time_frame=60, redirect_url='/rate_limit_exceeded', mode='ip')
def my_view(request):
    # View logic goes here

```

The previous example will limit the number of requests to the view to 100 per hour. If the limit is reached, the user will be redirected to '/rate_limit_exceeded'.

Other Example: 

```python
from django_happy_decorators.decorators.rate_limit import rate_limit


@rate_limit(num_requests=10000, time_frame=1, redirect_url='/rate_limit_exceeded', mode='all')
def my_view(request):
    # View logic goes here

```

The previous example will limit the number of requests to the view to 10k/min (10000 requests per minute). If the limit is reached, the user will be redirected to '/rate_limit_exceeded'. This could be useful if you know your server limits and want to prevent it from crashing."


## Parameters

- num_requests: the number of requests allowed per time_frame
- time_minutes: the time frame in which the number of requests is allowed
- redirect_url: the url to redirect the user to when the limit is reached
- mode: the mode to use to limit the number of requests. It can be one of the following values: ip, user or all. Default is 'all'.
- error_message: the error message to return with the response when the limit is reached. Default is 'You have exceeded the maximum number of requests allowed.' Note that this apply only if redirect_url is not set.


## Modes:

- ip: limits the number of requests per IP address
- user: limits the number of requests per user
- all: limits the number of requests

In the example above, the view will only allow 100 requests per hour and when the limit is reached it will redirect the user to '/rate_limit_exceeded'

# "If Not" Decorator

## Usage

To use the if_not decorator, import it from the package and apply it to a view function. The decorator accepts three parameters: condition, redirect_url and error_message.

Example:

```python
from django_happy_decorators.decorators.if_not import if_not

@if_not(parameter_name="mobile", raise_error_code=400, error_message="Mobile number is required")
def send_sms_view(request):
    # View logic goes here

```

The previous example will check if the request has a parameter called 'mobile'. If it doesn't, it will raise an error with the message 'Mobile number is required' and the status code 400.

## Parameters

- parameter_name: the name of the parameter to check
- raise_error_code: the status code to return with the response when the condition is not met. Default is 400.
- error_message: the error message to return with the response when the condition is not met. Default is 'The parameter {parameter_name} is required.'

## Request Types:

The decorator can be used with these types of requests (GET, POST, PUT, DELETE). It will check the request data based on the request type.

- GET: it will check the query parameters (request.GET)
- POST: it will check the form data (request.POST)
- PUT: it will check the form data (request.POST)
- DELETE: it will check the query parameters (request.GET)


# Contributing

We welcome contributions to Django Rate Limit. If you want to contribute, please read our contributing guidelines for more information.


# License

Django Rate Limit is released under the MIT License.

This is just a sample and you can adjust the content as per your package and also add more details like screenshots, sample code etc.

