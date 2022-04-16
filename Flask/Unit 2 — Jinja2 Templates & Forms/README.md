# Jinja2 Templates and Forms
Codecademy Notes (https://www.codecademy.com/learn/learn-flask)

Inject Python into HTML with templates
Collect user data with forms

----

## Flask Templates (Lesson)

### Intro
Pages of a website usually have the same look/feel. This can be achieved using **templates**. A template refers to an HTML file that represents multiple web pages with the same structure and functionality.

Flask uses **Jinja2 template engine** to render HTML. It also includes variables/app structures. Jinja2 supports organization for growth.

We'll be organizing our site file structure, use templates, use control structures in our templates, and share elements across templates.

We'll build a cookbook site!
Codecademy starts us off with 2 routes. Codecademy also provides `helper.py` to store recipe data (`recipes, descriptions, ingredients, instructions
`)

```
from  flask  import  Flask
from  helper  import  recipes, descriptions, ingredients, instructions

app = Flask(__name__)

@app.route('/')
def index():
    return  '''
      <!DOCTYPE html>
      <html>
        <body>
          <h1>Cooking By Myself</h1>
          <p>Welcome to my cookbook. These are recipes I like.</p>
          <a href="/recipe/1">Fried Egg</a>
        </body>
      </html>
    '''
    
#### Add the variable `id` to the route URL
#### and make it the sole function parameter
@app.route("/recipe/<int:id>")
def recipe(id):
    return  f'''
      <!DOCTYPE html>
      <html>
        <body>
          <a href="/">Back To Recipe List</a>
          <p>names[id] = ''' + recipes[id] + '''</p>
          <p>descriptions[id] = ''' + descriptions[id] + '''</p>
          <p>ingredients[id] = ''' + str(ingredients[id]) + '''</p>
          <p>instructions[id] = ''' + str(instructions[id]) + '''</p>
        </body>
      </html>
    '''
```
---
### Rendering Templates
Instead of returning HTML in-line, it's more typical to have HTML files. To work with these files/templates, use the Flask function `render_template()` in the return statement. This takes in the html file name and returns the content to send to the client. This uses the Jinja2 template engine. 

```
from  flask  import  Flask, render_template  
  
app = Flask(__name__)  
  
@app.route("/")  
def index():  
    return  render_template("index.html")
```

This for a `templates` directory in the app directory. This is where all templates should be stored. `index.html` is in `templates/`

```
from  flask  import  Flask, render_template
from  helper  import  recipes, descriptions, ingredients, instructions

app = Flask(__name__)

@app.route('/')
def index():
    #### Return a rendered index.html file
    return  render_template("index.html")

@app.route("/recipe/<int:id>")
def recipe(id):
    #### Return a rendered fried_egg.html file
    return  render_template("fried_egg.html")
```

Codecademy provided the html files

---
### Template Variables
It would be much easier to have one html file for many recipes instead of tons of individual files. Let's pass data to our template files. After the html file name in `render_template`, pass in variables and their assignment. To add more variables just separate with a comma. We can pass strings, ints. lists, dicts, or objects into templates. Yes, the arg and assignment can have the same name. Codecademy naming convention is to have vars start with 'flask' or 'template' respectively.

To access the variables in our templates use `{{ template_variable }}`, which is called an expression delimiter. Certain operations, like addition, can be done within the delimiters.

Here's an example of accessing a list element individually inside the expression delimiters. Pretend `template_list = ["a", "b", "c"]`

`<p>Element at index 1: {{ template_list[1] }}</p>`
  
This outputs `Element at index 1: b`

app.py
```
from  flask  import  Flask, render_template
from  helper  import  recipes, descriptions, ingredients

app = Flask(__name__)

@app.route('/')
def index():
    return  render_template("index.html")

@app.route("/recipe/<int:id>")
def recipe(id):
    #### Add template variables as
    #### variable assignment arguments
    return  render_template("recipe.html",
      template_recipe=recipes[id],
      template_description=descriptions[id],
      template_ingredients=ingredients[id])
```

recipe.html
```
<!DOCTYPE html>
<html>
  <body>
    <a href="/">Back To Recipe List</a>
    <h1>{{ template_recipe }}</h1>
    <p>{{ template_description }}</p>
    <h3>Ingredients</h3>
    
    <ul>
      <!-- Ingredients list elements should fill the <li> tags -->
      <li>{{ template_ingredients[0] }}</li>
      <li>{{ template_ingredients[1] }}</li>
      <li>{{ template_ingredients[2] }}</li>
    </ul>
  </body>
</html>
```
---
### Variable Filters
Let's play with how we can use these vars

**Filters** are used by the template engine to act on template vars. Use them by putting the `|` char (pipe) and then the `filter_name`.

The filter `title` capitalizes the first letter of each word in a string.

```
template_heading = "my very interesting website"
{{ template_heading | title }}
``` 
... produces `My Very Interesting Website`

Filters can take args. The `default` filter will output the text in its arg when a var isn't passed to the template. The default filter doesn't work on empty strings or the None value.

`captialize`, `lower`, `uppercase`, `int`, `float`, `length`, `dictsort`

recipe.html
```
<!DOCTYPE html>
<html>
  <body>
    <a href="/">Back To Recipe List</a>
    
    <!-- Make template_recipe title case -->
    <h1>{{ template_recipe | title }}</h1>
    
    <!-- Ensure a default description -->
    <p>{{ template_description | default("A " + template_recipe + " recipe.")}}</p>

    <!-- Output number of ingredients -->
    <h3>Ingredients - {{ template_ingredients | length }}</h3>

    <ul>
      <li>{{ template_ingredients[0] }}</li>
      <li>{{ template_ingredients[1] }}</li>
      <li>{{ template_ingredients[2] }}</li>
    </ul>

    <h3>Instructions</h3>

    <ol>
      <!-- Ensure sorted instruction dictionary -->
      <li>{{ template_instructions | dictsort }}</li>
    </ol>
  </body>
</html>
```
---
### If Statements

Control our data with if/else statements.
Remember how the `default` filter doesn't work on empty strings or `None`? An if conditional allows us to check for that.

Use this statement delimiter block syntax in the template
```
{% if condition %}  
  <p>This text will output if condition is True</p>  
{% endif %}
```

Comparison operators are `<`, `>`, `<=`, `>=`, `==`, `!=`

We can access variables within this delimiter block without any additional syntax

`None`, `False`, `0`, `""`, `[]` are falsey

```
template_number = 20 ...

{% if template_number < 20 %}  
  <p>{{ template_number }} is less than 20.</p>  
{% elif template_number > 20 %}  
  <p>{{ template_number }} is greater than 20.</p>  
{% else %}  
  <p>{{ template_number }} is equal to 20.</p>  
{% endif %}  
```
... produces `20 is equal to 20.`


Handle a given description vs default description
```
<!-- Insert description if statement here -->
{% if template_description %}
  <p>{{ template_description }}</p>
  
<!-- Include else here -->
{% else %}
  <p>A {{ template_recipe }} recipe.</p>

<!-- Be sure to close with an endif block -->
{% endif %}
```

Display correct number of bullets under ingredients when there's 2 vs 3 ingredients
```
{% if template_ingredients | length == 3 %}
  <li>{{ template_ingredients[2] }}</li>
{% endif %}
```

### For Loops
This is the syntax
```
{% for x in range(3) %}  
  <p>{{ x }}</p>  
{% endfor%}
```

To iterate through keys and values
```
{% for key, value in template_dict.items() %}
```

Display the correct number of bullets under ingredients no matter the number of ingredients
```
<!-- Implement a for loop to iterate through
`template_ingredients`-->
{% for ingredient in template_ingredients %}
  <li>{{ ingredient }}</li>
{% endfor %}
```

When using **dictsort** inside a for loop, dictsort will give us access to both the key and value of the dict.

```
{% for key, instruction in template_instructions|dictsort %}
  <!-- Add the correct dictionary element to list
the instructions -->
  <p>{{ key }}: {{ instruction }}</p>
{% endfor %}
```

Add correct list and links to homepage
```
{% for id, name in template_recipes.items() %}
  <p><a  href="/recipe/{{ id }}">{{ name }}</a></p>
{% endfor %}
```

### Inheritance


----

## Flask Templates (Quiz)

Sample Text

----

## Flask Forms (Lesson)

Sample text

----

## Flask Forms (Quiz)

Sample Text

----

## Tourist Attraction (Project)

Sample text

---- 

## Flask Environment Setup

Video
