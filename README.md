In Django, you can define functions within your models to perform specific tasks related to the model. These functions are often referred to as model methods. Here's a simple example to demonstrate how you can create a model function in Django:

Assuming you have a model named Book, you can create a method within the model class to perform a specific action. Let's say you want to get the full title of the book, combining the title and author:

python
Copy code
# models.py
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=50)
    published_date = models.DateField()

    def full_title(self):
        """Returns the full title of the book."""
        return f"{self.title} by {self.author}"
In this example, we've defined a full_title method within the Book model. This method takes the title and author fields of the book and combines them to create the full title. You can then use this method on instances of the Book model:

python
Copy code
# views.py
from django.shortcuts import render
from .models import Book

def book_detail(request, book_id):
    book = Book.objects.get(pk=book_id)
    full_title = book.full_title()

    return render(request, 'book_detail.html', {'book': book, 'full_title': full_title})
In the above view, we retrieve a Book instance from the database and then call its full_title method to get the combined title and author. You can then pass this information to a template for rendering.

Remember to run python manage.py makemigrations and python manage.py migrate after making changes to your models to apply the changes to the database schema.
