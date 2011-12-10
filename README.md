# django-cart ![Project status](http://stillmaintained.com/ahmet/django-cart.png)

## Introduction

django-cart is an easy to setup shopping cart mechanism for [Django](http://djangoproject.com) projects.

It lets you add items to and remove items from a session based cart, using the power of the Django content type framework to enable you to have your own Product model and associate with the cart without having to change anything. 

Developed using base code from [django-cart](http://code.google.com/p/django-cart) written by [Marc Garcia](http://vaig.be) and original idea belongs to Eric Woudenberg.

## Installation

Clone from github:

    $ git clone git://github.com/ahmet/django-cart.git

Add cart to INSTALLED_APPS:

    INSTALLED_APPS = (
        ...
        'cart'
    )

**Note:** `You must have django.contrib.contenttypes in INSTALLED_APPS`

Run:

	$ python manage.py syncdb

## Usage

A basic usage of django-cart could be (example):

```python
# views.py
from cart import Cart
from myproducts.models import Product

def add_to_cart(request, product_id, quantity):
    product = Product.objects.get(id=product_id)
    cart = Cart(request)
    cart.add(product, product.unit_price, quantity)

def remove_from_cart(request, product_id):
    product = Product.objects.get(id=product_id)
    cart = Cart(request)
    cart.remove(product)

def get_cart(request):
    return render_to_response('cart.html', dict(cart=Cart(request)))
```

```python
# templates/cart.html
	{% extends 'base.html' %}

	{% block body %}
    <table>
        <tr>
            <th>Product</th>
            <th>Quantity</th>
            <th>Total Price</th>
        </tr>
        {% for item in cart %}
        <tr>
            <td>{{ item.product.name }}</td>
            <td>{{ item.quantity }}</td>
            <td>{{ item.total_price }}</td>
        </tr>
        {% endfor %}
    </table>
	{% endblock %}
```

## Issues

Maybe several, please create [issues](http://github.com/ahmet/django-cart/issues).


## Contributing

Want to contribute? It's good to hear.

1. Fork it
* Create a branch (git checkout -b my_branch)
* Commit your changes (git commit -am "Added/Modified something")
* Push to the branch (git push origin my_branch)
* Create an Issue with a link to your branch
* Enjoy a refreshing beer and wait

## To do list

* tests
* migrations
* exceptions
* example app
* purge unused carts from db