# Mongo

Mongo DB Compass



REsumen clase pasada, notas borradas

Restful&#x20;

1. Read Method = "GET"
   1. List
   2. By ID
   3. filter
2. Update
3. Create
4. Delete.





Libros tipo json.&#x20;



PAra mongo es 27017



Colección tablas: van a contener un objeto completo, esto es similar a como vemos el mundo a traves de objetos y eventos.

Documento -> registro



Cosas que programamos:

1. Logger
2. Modelo
3. Servicios -> funcionalidades o lógica
4. Rutas





Códigos de error

500 -> errores del servidor

400 -> errores del cliente

200 -> OK

201 -> Create

204 ->Delete

404-> Not found&#x20;

403 -> Forbidden







\-----------------

Se recomienda primero realizar READ porque Update y DELETE lo usan.









Metodo, capacidad que tiene una clase.&#x20;



Variable conector tienen la conxion activa a MongoDB, esto permite que se realicen los cambios, esto es inserciones, eliminicaciones, actualizaciones y demás.

Find() suele traer una lista entera de elmentos, con find\_one solo te trae un elemento. Este metodo usado garantiza que el primer elemento lo traiga&#x20;



```python
def get_book_by_id(self, book_id):
    try:
        self.book = self.db_connector.db.books.find_one({'_id':book_id})
        return self.book
   except Exception as e:
        log.critical(f'Error fetching the book id from the database: {e}')
        return jsonify({'error': 'Book not found'}), 404
```

Normalmente se busca usando diccionarios, por eso para buscar se usan llaves: `{'_id':book_id}`

La ruta recordemos es nuestra capa de presentación, para proveer el json.&#x20;





En rutas modificamos agregando linea 14 donde se especifica&#x20;

````
```python
self.route('api/books/<int:book_id>', 
methods=['GET']

````

Se modifica metodo get\_book\_by\_id en linea 27  en Routes

Si existe el libro se manda el json y manda codigo 200, en caso contrario manda como si fuera un error.&#x20;



Para comprobar funcionamiento.



python3 app.py



export MONGODB\_USER=admin

export MONGODB\_PASS=pass123

export MONGODB\_HOST=localhost



curl -X GET http://localhost:5000/api/books/1



docker ps&#x20;

docker start mongodb



\----------------

Para el filtrado se debe realizar con mongo db por nosotros.



\----------------

PARA UPDATE:



Realizar la actualizacion para ello ocupamos id libro, sabe que si existe y validar los datos y luego actualizar.

'$set: updated\_data'



En el in updated al else: return None va la validación





curl -X GET http://localhost:5000/api/books/1 -H "Content-Type: application/json" -d '{"title": "Book 4", "author": "Author 4"}'







PARA DELETE



curl -X DELETE http://localhost:5000/book/1







PARA CREATE



Para conocer el ultimo inidice de la lista se usa -1 en python y se crea el nuevo elemento







