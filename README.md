# TideLit - Frontend

Frontend desarrollado en **Vue 3** con **Vite**, que consume la API desarrollada en Symfony.  
Permite listar libros y mostrar su promedio de calificaciones (`average_rating`), además de refrescar los datos manualmente.

---

## 1. Requisitos

Asegúrate de tener instaladas las siguientes herramientas:

- **Node.js** >= 18.x  
- **npm** >= 9.x o **yarn** >= 1.22  
- Backend en Symfony corriendo (ver [README Backend](../backend/README.md))

---

## 2. Instalación y configuración

### Clonar repositorio
```bash
git clone https://github.com/NicolasDevel/tidelit-front.git
cd tidelit/frontend
```

### Variables de entorno
Copia el archivo .env.example a .env:
```bash
cp .env.example .env
```
Edita el archivo .env y configura la URL de la API Symfony:
```bash
VITE_API_URL=http://localhost:8080/api
```
### Instalar dependencias
```bash
npm install
```
### Ejecutar en modo desarrollo
```bash
npm run dev
```
Por defecto, el frontend se ejecutará en:
```bash
http://localhost:5173
```
## 3. Funcionalidades
- Lista de libros obtenida desde el endpoint GET /api/books.
- Muestra:
    - title → Título del libro.
    - author → Autor.
    - published_year → Año de publicación.
    - average_rating → Promedio de calificaciones.
    - Botón para refrescar datos manualmente.
    - Manejo básico de errores si la API no responde.

## 4. Estructura del proyecto
frontend/
├── public/                # Archivos públicos
├── src/
│   ├── components/
│   │   └── BookList.vue   # Componente principal que lista libros
│   ├── services/
│   │   └── api.js         # Configuración de Axios
│   ├── App.vue            # Root component
│   └── main.js            # Punto de entrada de Vue
├── .env.example           # Variables de entorno
├── package.json
└── vite.config.js

## 5. Ejemplo de consumo
Ejemplo de respuesta del endpoint GET /api/books
```json
{
    "message": "Books retrieved successfully",
    "data": [
        {
            "id": 2,
            "title": "Clean Code",
            "author": "Robert C. Martin",
            "published_year": 2008,
            "average_rating": "4.0000000000000000"
        },
        {
            "id": 3,
            "title": "Refactoring",
            "author": "Martin Fowler",
            "published_year": 1999,
            "average_rating": "3.0000000000000000"
        },
        {
            "id": 1,
            "title": "El Arte de Programar",
            "author": "Donald Knuth",
            "published_year": 1968,
            "average_rating": "4.5000000000000000"
        }
    ]
}
```

## 6. Branch y commit final
### Branch evaluado: master
### Commit final:
```bash
commit bf39130783865599432c0dd5e1243038030d7248

```