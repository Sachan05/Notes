Django:

- To open terminal in vscode : Control + ~
- Virtual environment - source venv1/bin/activate
- To read particular function - command+click
- To see suggestions - control+space
- To open DB -> search for SQLite->open DB->check sqlite explorer



In Django, every web app you want to create is called a project; and a project is a sum of applications. An application is a set of code files relying on the MVT pattern.

* navigate to the place you want your project to be created, then use this code −
	$ django-admin startproject myproject


* This will create a "myproject" folder with the following structure −
	myproject/
   		manage.py
   		myproject/
      			__init__.py
      			settings.py
      			urls.py
      			wsgi.py

* Now that your project is created and configured make sure it's working −
	$ python manage.py runserver


* Create an Application : We assume you are in your project folder. In our main “myproject” folder, the same folder then manage.py 
	$ python manage.py startapp myapp
	
	You just created myapp application and like project, Django create a “myapp” folder with the application structure −
		myapp/
   			__init__.py
   			admin.py
   			models.py
   			tests.py
   			views.py

* At this stage we have our "myapp" application, now we need to register it with our Django project "myproject". To do so, update INSTALLED_APPS tuple in the settings.py file of your project (add your app name) 



* We will create a simple view in myapp to say "welcome to my app!" . Open "myapp\views.py" and add the following view function −                  from django.shortcuts import render                 # Create your views here.                    def index(request):                             return render(request, index.html', {})


* In this view, we use HttpResponse to render the HTML page. To see this view as a page, we just need to map it to a URL. Save the following Python script as myapp/urls.py −            from django.urls import path          from . import views          urlpatterns = [             path('', views.index, name='index'),          ]


* The next step is to point the root URLconf at the myapp.urls module.  In myproject/urls.py, add an import for django.urls.include and insert an include() in the urlpatterns list, so you have −

		from django.contrib import admin
		from django.urls import include, path

		urlpatterns = [
   			path('', include('myapp.urls')),
   			path('admin/', admin.site.urls),
		]

* Now run the Django development server −
		python manage.py runserver


* Models : A Django model is again a Python class derived from django.db.model.Models, which you place in the app's models.py file.
 			A model class can include methods that return values computed from other class properties. Models typically include a __str__ method that returns a string  			representation of the instance.  			Because you changed your data models by editing models.py, you need to update the database itself. 

			python manage.py makemigrations
			python manage.py migrate

			it will create a table ‘projectname_classname’. You can use meta class to give a different table name.



			* to insert in db, create an object in views of that table n insert it.

			class Book(models.Model):
    				title = models.CharField(max_length=100)
    				authors = models.ForeignKey(Author, on_delete=models.CASCADE)
			
			* then make migrations - creates a db schema in the migrations folder , 001_initial.py file                   		python manage.py makemigrations 			* python manage.py migrate - actually create tables in DB

			

			* To add in the DB : under the function in views.py
 				s1 = Student(name=name, age = '50', dob=datetime.date.today())
    				s1.save( )

			* To get data from DB : 				res = Student.objects.get(name=name)   			* RollBack : to rollback  the changes or to previous/another migration file (001)  				python manage.py migrate library 0001


	* Admins: python manage.py createsuperuser
			  name - Saum
			  pwd - S@123 /  S@gmail.com



* Library - REST application

*  Serializers :    converts one form of data into another.                    * activate venv, get inside project folder - Demo/Hello where manage.py file exists * create App Library :  python manage.py startapp library * add it in the settings.py - installed apps * create db structure in models.py * then make migrations - creates a db schema in the migrations folder , 001_initial.py file                   python manage.py makemigrations * python manage.py migrate - actually create tables in DB * All the REST related stuff will be in views  * create a separate serializer.py file in the same app and create a object serialised here.              class BookSerialzer(serializers.ModelSerializer):                    class Meta:                          model = Book                          fields = '__all__’  * in the views.py file, map the request data to the object        @api_view(['POST'])       def create_book(request):              book_serializer = BookSerialzer(data=request.data)  * then create urls.py to map the trigger the function created.             add url patterns:                           urlpatterns = [                                      path('createbook/',views.create_book, name='createbook')                                      ] * then add in the project urls:                 path('api/’, include('library.urls'))  * then run the application :                 python manage.py runserver   * then send a post request to create a resource :                 localhost:8000/api/createbook/                 {                     "title":"Atomic Habits",                     "authors":3                  }
*         Custom Queries  : 
* To Run via Shell : python manage.py shell  from django.db.models import Q >>> from library.models import Book >>>  >>> b = Book.objects.filter(title='Atomic Habits') >>> print(b) >>> print(b[0]) >>> print(b[0].__dict__)  >>> b = Book.objects.filter(Q(title__startswith='A') | Q(title__startswith='H')) >>> print(b)   O/P = <QuerySet [<Book: Book object (1)>, <Book: Book object (2)>]>  



* Go to the folder where you need to create a project - Service
* First, create the virtual environment
    * python3 -m venv django-env
* Then, use this environment
    * source django-env/bin/activate
* Next, install django
    * python -m pip install django
* Finally test django is working
    * django-admin startproject PaymentService
* Inside PaymentService folder, create another app called payment


*inside project settings - add razor pay id n key

* Then inside payment folder, create urls.py file, add :  * urlpatterns = [          path('',views.payment, name='payment '), ]  
* Then create views, to accept data in views here from http methods, we create serializers.py file 









