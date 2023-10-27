# Recipes_Django
Для создания сайта рецептов на Django, вам потребуется выполнить следующие шаги:

1. Установите Django, если у вас его еще нет. Вы можете установить его с помощью pip:

pip install django


2. Создайте новый проект Django с помощью команды:

django-admin startproject recipesite


3. Перейдите в директорию проекта:

cd recipesite


4. Создайте новое приложение Django для рецептов:

python manage.py startapp recipes


5. Откройте файл settings.py в директории recipesite и добавьте 'recipes' в список INSTALLED_APPS.

6. Определите модели для рецептов в файле models.py внутри приложения recipes. Например, вы можете создать модель Recipe со следующими полями:
python
from django.db import models

class Recipe(models.Model):
    title = models.CharField(max_length=100)
    ingredients = models.TextField()
    instructions = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title


7. Создайте миграции для моделей, чтобы создать соответствующие таблицы в базе данных:

python manage.py makemigrations
python manage.py migrate


8. Откройте файл urls.py в директории recipesite и добавьте следующий код:
python
from django.urls import path
from recipes import views

urlpatterns = [
    path('', views.recipe_list, name='recipe_list'),
    path('recipe/<int:pk>/', views.recipe_detail, name='recipe_detail'),
]


9. Создайте файл views.py внутри приложения recipes и добавьте следующий код:
python
from django.shortcuts import render, get_object_or_404
from .models import Recipe

def recipe_list(request):
    recipes = Recipe.objects.all()
    return render(request, 'recipes/recipe_list.html', {'recipes': recipes})

def recipe_detail(request, pk):
    recipe = get_object_or_404(Recipe, pk=pk)
    return render(request, 'recipes/recipe_detail.html', {'recipe': recipe})


10. Создайте директорию templates внутри приложения recipes и в ней создайте файлы recipe_list.html и recipe_detail.html. В этих файлах вы можете определить шаблоны для отображения списка рецептов и отдельного рецепта соответственно.

11. Запустите сервер разработки Django:

python manage.py runserver


Теперь вы можете открыть браузер и перейти по адресу http://localhost:8000/, чтобы увидеть список рецептов. Вы также можете перейти по адресу http://localhost:8000/recipe/<id>, чтобы увидеть отдельный рецепт с указанным идентификатором.
