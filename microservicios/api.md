# API

4 funciones&#x20;

1. Create
2. Read - Filtro
3. Update
4. Delete



Dentro de app.py





\-> Modelos: contiene la estructura en donde vamos a guardar los datos.

\-> Esquemas, validación de los datos, que toda la informacion ea correcta. Al solicitar un archivo o valor de tipo numérico el esquema verficia que el dato este bien formado para que no se realice inyección de alguna otra cosa.



&#x20;\-> Rutas&#x20;

\-> Sources







Ejemplo 2.&#x20;

Recordar colocar el interpretador de python es el del entorno virtual, vnv -> python3.12&#x20;

{% code title="book_model.py" overflow="wrap" lineNumbers="true" %}
```python
class BookModel:
    def __init__(self): #definimosnuestra clase
        self.books = { #variable books, libros que vamos a colocar
            1: {'title': 'Book 1', 'author': 'Author 1'}, #
            2: {'title': 'Book 2', 'author': 'Author 2'},
            3: {'title': 'Book 3', 'author': 'Author 3'},
        }

    #este modelo sera en tipo json, el esquema sera usado despues en MongoDB, 
```
{% endcode %}



{% code title="book_schema.py" overflow="wrap" lineNumbers="true" %}
```python
class BookSchema:
    def __init__(self): #definimosnuestra clase
        self.BookSchema = { #variable books, libros que vamos a colocar
            'title': { 'type': 'string', 'required': 'True'}, #
            'title': { 'type': 'string', 'required': 'True'}, 
        }
```
{% endcode %}



{% code title="book_service.py" overflow="wrap" lineNumbers="true" %}
```python
class BookService:
    def __init__(self, book_model, book_schema):
        self.book_model = book_model
        self.book_schema = book_schema

     def get_all_books(self):
        return list(self.book_model.books.values())
```
{% endcode %}



{% code title="book_routes.py" overflow="wrap" lineNumbers="true" %}
```python
from flask import Blueprint, jsonify     #todo dato que se envie lo convierte en un objeto tipo json.
from services.book_service import BookService
from models.book_model import BookModel
from schemas.book_schema import BookSchema


book_routes = Blueprint("books_routes", __name__)
book_model = BookModel()
book_schema = BookSchema()
book_service = BookService(book_model, book_schema)
    
@book_routes.route('/books', methods=['GET'])
def get_books(): 
    return jsonify (book_service.get_all_books() )
```
{% endcode %}



{% code title="" overflow="wrap" lineNumbers="true" %}
```python
from flask import Flask
from routes.book_routes import book_routes

app = Flask(__name__)
app.register_blueprint(book_routes)

if __name__ == '__main__':
    app.run(debug=True)
```
{% endcode %}

python app.py

con estos al ejecutar curl -X GET http://localhost:3000/books

obtenemos la lista de los libros que tenemos.&#x20;







Ahorma modificamos en base a un criterio de busqueda del id del libro

PAra esto debemos modificar book service y route

{% code title="book_service.py" overflow="wrap" lineNumbers="true" %}
```python
class BookService:
    def __init__(self, book_model, book_schema):
        self.book_model = book_model
        self.book_schema = book_schema

     def get_all_books(self):
        return list(self.book_model.books.values())

    def get_book_by_id(self, book_id):
        book = self.book_model.books.get(book_id)
        return book
```
{% endcode %}

<pre class="language-python" data-title="book_route.py" data-overflow="wrap" data-line-numbers><code class="lang-python">from flask import Blueprint, jsonify #todo dato que se envie lo convierte en un objeto tipo json.
from services.book_service import BookService
from models.book_model import BookModel
from schemas.book_schema import BookSchema


book_routes = Blueprint("books_routes", __name__)
book_model = BookModel()
book_schema = BookSchema()
book_service = BookService(book_model, book_schema)
    
@book_routes.route('/books', methods=['GET'])
def get_books(): 
    return jsonify (book_service.get_all_books() )

<strong>#el entero viene del book id del libro que se va a obtener.
</strong><strong>@book_routes.route('/books/&#x3C;int:book_id>', methods=['GET'])
</strong>def get_book_by_id(book_id):
    book = book_service.get_book_by_id(book_id)
    if book:
        return jsonify(book)
    else:
        return jsonify({'error': 'Book not found'}), 404
</code></pre>

python.py app.py

curl -X GET http://localhost:3000/books/1



LECTURA

1. obtener listado completo
2. Obtener por ID
3. Filtrado



\-----------------

CREACION

Ahora modificamos





{% code title="book_schema.py" overflow="wrap" lineNumbers="true" %}
```python
from marshmallow import Schema, fields, validates, ValidationError

class BookSchema:
    title = fields.String(required=True)
    author = fields.String(required=True)

    @validates('title')
    def validate_title(self, value): #validación del titulo
        if len(value) < 5:
            raise ValidationError('Title must be at leat 5 characters long.') #lanza un error personalizado junto a un mensaje personalizado para el usuario.
        
    @validates('author')
    def validate_author(self, value): #valudacion del autor
        if len(value) < 5:
            raise ValidationError('Author must be at leat 5 characters long.')
```
{% endcode %}

Expresiones regulares

\*(Asterisco) -> de 0 a  n

. (punto) -> de 1 a n

^ ->

? ->

&#x20; &#x20;

{% code title="book_service.py" overflow="wrap" lineNumbers="true" %}
```python
class BookService:
    def __init__(self, book_model, book_schema):
        self.book_model = book_model
        self.book_schema = book_schema

     def get_all_books(self):
        return list(self.book_model.books.values())

    def get_book_by_id(self, book_id):
        book = self.book_model.books.get(book_id)
        return book

    def add_book(self, new_book):
            self.book_model.books[len(self.book_model.books) + 1] = new_book
            #como no sabemos el numero de nuestra lista actual hacemos un len 
            #para conocer cuantos tenemos y agregamos uno para no afectar.
            return new_book
```
{% endcode %}







{% code title="book_routes.py" overflow="wrap" lineNumbers="true" %}
```python
from flask import Blueprint, jsonify, request #todo dato que se envie lo convierte en un objeto tipo json.
from services.book_service import BookService
from models.book_model import BookModel
from schemas.book_schema import BookSchema
from marshmallow import ValidationError

book_routes = Blueprint("books_routes", __name__)
book_model = BookModel()
book_schema = BookSchema()
book_service = BookService(book_model, book_schema)
#localhost:3000? 
@book_routes.route('/books', methods=['GET'])
def get_books(): 

#return jsonify (book_service.get_all_books() )
    title = request.args.get('title')
    author = request.args.get('author')
    filtered_books = book_service.filter_books(title, author)
    if filtered_books:
        return jsonify(filtered_books)
    else:
        return jsonify({'message': 'No books found with the specified criteria'}), 404

@book_routes.route('/books/<int:book_id>', methods=['GET'])
def get_book_by_id(book_id):
    book = book_service.get_book_by_id(book_id)
    if book:
        return jsonify(book)
    else:
        return jsonify({'error': 'Book not found'}), 404


@book_routes.route('/books', methods=['POST'])
def create_book():
    data = reques    t.get_json() #pasamos la data de nuestro .json
    if not data: #primero verificamos que tenemos datos en nuestro .json
        return jsonify({'error': 'Invalid data'}), 400 

    #Descomponemos por partes el diccionario. 
    title = data.get('title') 
    author = data.get('author')

    try: 
        book_schema.validate_title(title)
        book_schema.validate_author(author)
    except ValidationError as e:
        return(jsonify({'error': 'Invalid data', 'details': e.messages}))

    new_book = {
        'title': title,
        'author': author
    }
    created_book = book_service.add_book(new_book)
    
    return jsonify(created_book), 201
    
    
```
{% endcode %}





curl -X GET http://localhost:3000/



curl -X POST http://localhost:3000



NEcesitamos mandarle el json por medio de un header:

/books -H "Content-Type: application/json" -d '{}'



&#x20; \#este le dice que tiipo de contenidos se esta aplicando?

\-d define el cuerpo o body de nuestra petición, en este caso el body estará vacío.





Ahora mandaremos un libro con un autor o titulo incorrecto:

curl -X POST http://localhost:3000

/books -H "Content-Type: application/json" -d '{"title": "Book", "author": "Author 4"}'

Correcto:

/books -H "Content-Type: application/json" -d '{"title": "Book 4", "author": "Author 4"}'

Validamos que sise agregó el libro:&#x20;

curl -X GET http://localhost:3000/





//PARA ACTUALIZACION Y LMINICAICON ES IMPORTANTE PARTIR DE LA LECTURA PORQUE FACILITA LOS DEMAS.

```python
def update_book(self, book_id, updated_data):
        book = self.get_book_by_id(book_id) #buscamos el libro con el metodo que creamos
        print(f'Book: {book}') 
        if book: #existe ese libro
            for key, value in updated_data.items(): #si nos regresa el libro
                if key in book: #si encuentra la llave en ese libro :D
                    book[key] = value
            return book
        else:
            return None #si no encontro el libro, no se actualizaw
```





```python
@book_routes.route('/books/<int:book_id>', methods=['PUT'])
def update_book(book_id):
    data = request.get_json()
    if not data:
        return jsonify({'error': 'Invalid data'}), 400
    
    title = data.get('title')
    author = data.get('author')

    try: 
        book_schema.validate_title(title)
        book_schema.validate_author(author)
    except ValidationError as e:
        return(jsonify({'error': 'Invalid data', 'details': e.messages}))
    
    book_updated = book_service.update_book(book_id, data)
    
    if book_updated:
        return jsonify(book_updated)
    else:
        return jsonify({'error': 'Book not found'}), 404
```



Codigo de error, todos los 400 son errores de cliente, los del server

El metodo usado es PUT -> actualización.







curl -X PUT http://localhost:3000/

/books/2 -H "Content-Type: application/json" -d '{"title": "Book n", "author": "Author n"}'



Comprobamos con que no se haya agragado ningun libro, en cambio se debe modificar solo el libro 2 por los datos que colocamos.&#x20;

curl -X GET http://localhost:3000/





