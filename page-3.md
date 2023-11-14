# Page 3

API RESTFUL



* CREATE -POST / PUT
  * Generalmente la modificación para CREATE es Model, Schema, Service, Routes.
* READ - GET List, by ID, filter&#x20;
  * Para READ es Service, Routes.
* UPDATE - Patch
  * Para UPDATE es Schema, Service, Routes.
* DELETE - delete
  * Para DELETE es Service, Routes.



Queremos crear un funcion par apoder eliminar un libro por lo que debemos de modificar los servicios. Por ello agregamos a nuestra función:

{% code title="BookService.py" overflow="wrap" lineNumbers="true" %}
```python
    def delete_book(self, book_id): 
        book = self.get_book_by_id(book_id)
        if book:
            del self.book_model.books[book_id]
            return book
        else:
            return None
```
{% endcode %}



\----

Ahora que ya tenemos modificado el servicio debemos realizar cambios a la ruta

{% code title="book_routes.py" overflow="wrap" lineNumbers="true" %}
```python
   
@book_routes.route('/books/<int:book_id>', methods=['DELETE'])
def delete_book(book_id):
    deleted_book = book_service.delete_book(book_id)

    if deleted_book:
        return jsonify({'message': 'Book deleted successfully'})
    else:
        return jsonify({'error': 'Book not found'}), 404
```
{% endcode %}

Se valida que se haya encontrado un libro, si no lo encuentra como es valor nulo se manda un mensaje que no lo encontró.&#x20;



NOTAS

Se le pasa un parametro de tipo entero.

```python
<int:book_id>
```

Diferencia entre tupla y lista.

Tupla no permite el el mismo dato, o datos que no sean del mismo tipo es decir elementos de diferente tipo





cd restuful app&#x20;

souce ---

activacion de entorno virtual

python3 app.py

Petición con un libro que no existe

```
curl -X DELETE http://localhost:5000/book/10
```



POSTMAN es mas faicl verificar el codigo que se manda.&#x20;



Errores mandados con json se parsean y se usan card (diferente a snackbar)



Petición con un libro que si existe

```
curl -X DELETE http://localhost:5000/book/1
```

verificamos con

```
curl -X DELETE http://localhost:5000/books
```



Dado nuestro modelo podemos buscar nuestros books por medio de titulo y autor.&#x20;

{% code title="book-service.py" overflow="wrap" lineNumbers="true" %}
```python
    def filter_books(self, title=None, author=None):
        filtered_books = []
        for book_id, book in self.book_model.books.items():
            #key, values
            #Libros que coincidan con el titulo obtenido / libros que coincidan con el autor obtenido.
            if (title is None or book['title'] == title) and (author is None or book['author'] == author):
                filtered_books.append(book)
        return filtered_books
```
{% endcode %}



Para el filtrado se coloca un valor por defecto, y se va a recorrer el diccionario de libros

Ahora se modifica el book\_routes :

```python
@book_routes.route('/books', methods=['GET'])
def get_books(): 
#return jsonify (book_service.get_all_books() )
#Se obtienen titulo y autor.
    title = request.args.get('title')
    author = request.args.get('author')
    #Mismo orden 
    filtered_books = book_service.filter_books(title, author)
    if filtered_books:
        return jsonify(filtered_books)
    else:
        return jsonify({'message': 'No books found with the specified criteria'}), 404

```



Documentacion para API, para cada metodo GET, POST, etc. Para ello vamos a usar swagger.





```
curl -X DELETE http://localhost:5000/books
```

```
curl -X DELETE http://localhost:5000/books?title=Book1
```



? para saber que parametro le estamos preguntando si tiene



```
curl -X DELETE http://localhost:5000/books?author=auth
```

como  no existen los espacios se usa %20

```
curl -X DELETE http://localhost:5000/books?title=Book%201
```

```
curl -X DELETE http://localhost:5000/books?title=Author%201
```









Funcionalidad

Ejemplo.

Gestionar Libros debe tener las 4 funcionalidades esto es CREATE, READ, UPDATE, DELETE

Son 4 APIS para 4 de nuestras funcionalidad que tenemos.



Web UI bien, y el back end bien realizado.











