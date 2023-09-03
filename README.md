<h1 align="center" style = "margin: 0 auto;  height: 200px; overflow: hidden;" >
  <p align="center">API FRUTAS</p>
  <a href="" ><img style=" width: 100%; text-align: center; " src="./public/image/Frutas.jpg" alt="Docusaurus"></a>
</h1>

## Tabla de contenidos
- [Tabla de contenidos](#tabla-de-contenidos)
  - [Información General](#información-general)
  - [Link URL base](#link-url-base)
  - [Objeto Frutas](#objeto-frutas)
  - [Peticiones](#peticiones)
  - [Métodos](#métodos)
    - [Método PUT](#método-put)
    - [Metodo POST](#metodo-post)
  - [Archivo .ENV](#archivo-env)
  - [Graficos](#graficos)
  - [Colaboradores](#colaboradores)

### Información General
***
<div class="warning" style='padding:0.1em; background-color:#E9D8FD; color:#69337A'>
<span>
<p style='margin-left:1em;'>
La Api Frutas, es un proyecto para <b>Visualizar,Crear, Actualizar y Eliminar</b> fácilmente frutas de una base de datos proporcionada.
</p>
</p></span>
</div>
 

### Link URL base
***
<!-- http://localhost:3000/api/v1/ -->
> http://localhost:3000/api/v1/


### Objeto Frutas
***
```javascript
// ejemplo de la estructura de frutas
{
    "id":1,
    "imagen":"🍌",
    "nombre":"Bananas",
    "importe":300,
    "stock":50
}
```

###  Peticiones 
***
| PETICION | URL                                     | DESCRIPCION                        |
| :------- | :-------------------------------------- | :--------------------------------- |
| GET      | [/frutas](http://localhost:3000/frutas) | Obtener todas las frutas           |
| POST     | [/frutas](http://localhost:3000/frutas) | Agregar una fruta                  |
| PUT      | [/frutas/:id](http://localhost:3000/frutas/:id) | Modificar una fruta pasandole el ID                 |
| DELETE   | [/frutas/:id](http://localhost:3000/frutas/:id) | Eliminar una fruta pasandole el ID |

### Métodos
#### Método PUT
***
> [!NOTE]  
> Este método va actualizar la fruta recibiendo el Id  y los campos del objeto a modificar en la base de datos
```javascript

app.put('/frutas/:id' , async (req, res) => {
    const id = parseInt(req.params.id) || 0;
    const nuevosDatos = req.body
    if (!nuevosDatos) {
     res.status(400).send('Error formato no recibido')
    }
const client = await connectToMongodb();
    if (!client) {
        res.status(500).send('Error al conectarse a MongoDB')
        return;
    }
const db = client.db('frutas') 
const collection = await db.collection('frutas').updateOne({id : id },{ $set : nuevosDatos })
.then(() => {
    console.log('Se actualizo la nueva fruta')
    let mensaje = " Se actualizo la nueva fruta id: "+ id
    res.status(200).json({descripcion : mensaje , objeto: nuevosDatos})
}).catch(err => { 
    let mensaje = 'Error al actualizar id : ' + id 
console.error(err)
res.status(500).json ({descripcion : mensaje , objeto: nuevosDatos})
}).finally(() => { client.close()})

})
```

#### Metodo POST
***
> [!NOTE]  
> Este método crear una nueva fruta en la base de datos 
```javascript
app.post('/frutas' , async (req, res) => {
    const nuevaFruta = req.body
        if (nuevaFruta === undefined ) {
            res.status(400).send('Error en el formato de los datos ingresados')
        }
        const client = await connectToMongodb();
        if (!client) {
            res.status(500).send('Error al conectarse a MongoDB')
            return;
        }
    const db = client.db('frutas') 
    const collection = await db.collection('frutas').insertOne(nuevaFruta)
    .then(() => {
        console.log('Se creó la nueva fruta')
        res.status(201).send('Se creó la nueva fruta')
    }).catch(err => { 
        console.error(err)
    }).finally(() => { client.close()})
    
})
```

### Archivo .ENV
***
```
PORT=3008
MONGODB_URLSTRING=mongodb+srv://caro:1234@nube0.ztddbrv.mongodb.net/?retryWrites=true&w=majority
# mongodb+srv://<username>:<password>@nube0.ztddbrv.mongodb.net
```

### Graficos 
```mermaid
graph TD
  A[Inicio] --> B[Crear servidor Express]
  B --> C[Agregar los require necesarios, express, dotenv ..]
  C --> D[Incluir las funciones de conectar y desconectar declaradas en src/mongodb.js]
  D --> E[Definir endpoint GET /frutas]
  D --> F[Definir endpoint PUT /frutas/:id]
  D --> G[Definir endpoint GET /frutas/nombre/:nombre]
  D --> H[Definir endpoint POST /frutas/]
  E --> K[Retornar todo el contenido]
  F --> L[Aplicar filtro por Id]
  G --> M[Aplicar filtro por nombre de fruta]
  H --> N[Crea nueva fruta a partir del objeto enviado en el body]
```
##grafico ejemplo
```mermaid
graph TD
  A[Inicio] --> B[Crear servidor Express]
  B --> C[Agregar los require necesarios]
  C --> D[Incluir las funciones deconectar y desconectar declaradas en src/mongodb.js]
  D --> E[Definir endpoint GET /frutas]
  D --> F[Definir endpoint PUT /frutas/:id]
  D --> G[Definir endpoint GET /frutas/nombre/:nombre]
  D --> H[Definir endpoint POST /frutas/]
```
### Colaboradores 
***
<a href="https://github.com/carolinamendez0/IngeniasTpIntegrador/graphs/contributors" target="_blank">
<img alt="Carolina Mendez" title="Carolina Mendez" style=" width: 60px; /* Tamaño de los avatares */
  height: 60px;
  border-radius: 50%;" src="https://avatars.githubusercontent.com/u/49485102?s=60&v=4?width=890"></a>
<!-- <img src=""> -->


