
## 🗓️ **Day 1 — Django Basics**

### 🧱 1. Setup & Project Structure

```bash
# create virtual environment
python -m venv env
source env/bin/activate   # or env\Scripts\activate (Windows)

# install django
pip install django

# create new project
django-admin startproject myproject

# move inside & run server
cd myproject
python manage.py runserver
```

**Project structure:**

```
myproject/
├── manage.py
├── myproject/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
```

---

### 🧩 2. Create & Register an App

```bash
python manage.py startapp blog
```

**Add the app to `INSTALLED_APPS` in `settings.py`:**

```python
INSTALLED_APPS = [
    'blog',
    'django.contrib.admin',
    'django.contrib.auth',
    ...
]
```

---

### ⚙️ 3. Views, URLs & Templates

**blog/views.py**

```python
from django.http import HttpResponse

def home(request):
    return HttpResponse("Hello Django!")
```

**blog/urls.py**

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home')
]
```

**Include blog URLs in main `urls.py`:**

```python
from django.urls import path, include

urlpatterns = [
    path('', include('blog.urls')),
]
```

---

### 🧱 4. Models & Database

**blog/models.py**

```python
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.title
```

**Apply migrations:**

```bash
python manage.py makemigrations
python manage.py migrate
```

**Create superuser:**

```bash
python manage.py createsuperuser
```

**Run server and check admin:**

```bash
python manage.py runserver
# visit http://127.0.0.1:8000/admin
```

---

### 🧭 5. Django ORM Basics

```python
# shell
python manage.py shell

from blog.models import Post
Post.objects.create(title="Hello", content="Django is fun!")
Post.objects.all()
Post.objects.filter(title__icontains="hello")
Post.objects.get(id=1)
```

---

### 🧩 6. Templates (Basic Example)

**blog/views.py**

```python
from django.shortcuts import render

def home(request):
    return render(request, 'blog/home.html', {'name': 'Shadman'})
```

**blog/templates/blog/home.html**

```html
<h1>Hello {{ name }}</h1>
```

---

## ✅ Summary Commands

| Task             | Command                                 |
| ---------------- | --------------------------------------- |
| Create project   | `django-admin startproject projectname` |
| Create app       | `python manage.py startapp appname`     |
| Run server       | `python manage.py runserver`            |
| Make migrations  | `python manage.py makemigrations`       |
| Apply migrations | `python manage.py migrate`              |
| Create superuser | `python manage.py createsuperuser`      |

---

## 🗓️ **Day 2 — Django REST Framework (DRF)**

### ⚙️ 1. Setup

```bash
pip install djangorestframework
```

**settings.py**

```python
INSTALLED_APPS = [
    'rest_framework',
    'blog',
]
```

---

### 🧩 2. Simple Model

**blog/models.py**

```python
from django.db import models

class Article(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    author = models.CharField(max_length=50)
```

---

### 📦 3. Serializer

**blog/serializers.py**

```python
from rest_framework import serializers
from .models import Article

class ArticleSerializer(serializers.ModelSerializer):
    class Meta:
        model = Article
        fields = '__all__'
```

---

### 🧭 4. CRUD Views (APIView)

**blog/views.py**

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status
from .models import Article
from .serializers import ArticleSerializer

class ArticleList(APIView):
    def get(self, request):
        articles = Article.objects.all()
        serializer = ArticleSerializer(articles, many=True)
        return Response(serializer.data)

    def post(self, request):
        serializer = ArticleSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
```

---

### 🔗 5. URLs

**blog/urls.py**

```python
from django.urls import path
from .views import ArticleList

urlpatterns = [
    path('articles/', ArticleList.as_view(), name='article-list'),
]
```

**main urls.py**

```python
from django.urls import path, include

urlpatterns = [
    path('api/', include('blog.urls')),
]
```

---

### 🧱 6. ModelViewSet (Shorter CRUD)

**blog/views.py**

```python
from rest_framework import viewsets
from .models import Article
from .serializers import ArticleSerializer

class ArticleViewSet(viewsets.ModelViewSet):
    queryset = Article.objects.all()
    serializer_class = ArticleSerializer
```

**blog/urls.py**

```python
from rest_framework.routers import DefaultRouter
from .views import ArticleViewSet

router = DefaultRouter()
router.register(r'articles', ArticleViewSet)

urlpatterns = router.urls
```

---

### 🧪 7. Test the API

Run:

```bash
python manage.py runserver
```

Go to:
👉 `http://127.0.0.1:8000/api/articles/`

---

### ⚡ 8. Common DRF Commands

| Task             | Command                                            |
| ---------------- | -------------------------------------------------- |
| Install DRF      | `pip install djangorestframework`                  |
| Serializer class | `serializers.ModelSerializer`                      |
| APIView          | `from rest_framework.views import APIView`         |
| ViewSet Router   | `from rest_framework.routers import DefaultRouter` |

---

### 🔥 Bonus — Use Django Shell for API data

```bash
python manage.py shell
from blog.models import Article
Article.objects.create(title="Django REST", content="Learning APIs", author="Shadman")
```
