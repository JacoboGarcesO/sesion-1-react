# SESIÓN 1: Fundamentos y Primer Componente (4 horas)

---

## HORA 1: Introducción, Setup y Conceptos Básicos (60 min)

### 1.1 ¿Qué es React? (10 min)

**Explicar a los estudiantes:**

React es una **biblioteca de JavaScript** para construir interfaces de usuario, creada por Facebook (Meta).

**Características principales:**
- **Componentes**: Divide la UI en piezas reutilizables
- **Declarativo**: Describes CÓMO debe verse la UI, no paso a paso cómo construirla
- **Virtual DOM**: React actualiza solo lo necesario, haciendo las apps rápidas

**Ejemplo del mundo real:**
"Imaginen Netflix: el header, el carrusel de películas, cada tarjeta de película... son componentes que se reutilizan"

**¿Por qué React?**
- Muy demandado en el mercado laboral
- Gran comunidad y ecosistema
- Permite crear SPAs (Single Page Applications) modernas
- Facilita mantener y escalar proyectos

---

### 1.2 Prerequisitos y Verificación de Entorno (10 min)

**Verificar que todos tengan instalado:**

**Node.js (versión 18 o superior):**
```bash
node --version
# Debe mostrar v18.x.x o superior
```

Si no lo tienen: descargar de https://nodejs.org (versión LTS)

**npm (viene con Node.js):**
```bash
npm --version
# Debe mostrar 9.x.x o superior
```

**Editor de código recomendado: VS Code**
- Descargar de https://code.visualstudio.com

**Extensiones recomendadas para VS Code:**
1. **ES7+ React/Redux/React-Native snippets** (dsznajder)
2. **Simple React Snippets** (Burke Holland)
3. **Prettier - Code formatter**

*Mostrar cómo instalar extensiones en VS Code*

---

### 1.3 Crear Proyecto con Vite (15 min)

**¿Qué es Vite?**
- Herramienta moderna para crear proyectos frontend
- Muy rápida (usa el motor esbuild)
- Sustituto moderno de Create React App

**PASO A PASO (hacer junto con los estudiantes):**

**1. Abrir terminal/consola**

**2. Navegar a la carpeta donde quieren el proyecto:**
```bash
cd Desktop
# o la carpeta que prefieran
```

**3. Crear el proyecto:**
```bash
npm create vite@latest mi-primera-app-react
```

**4. Seleccionar opciones:**
- Framework: **React** (usar flechas y Enter)
- Variant: **JavaScript** (NO TypeScript por ahora)

**5. Entrar a la carpeta del proyecto:**
```bash
cd mi-primera-app-react
```

**6. Instalar dependencias:**
```bash
npm install
```
*Explicar: esto instala todas las bibliotecas que React necesita*

**7. Iniciar el servidor de desarrollo:**
```bash
npm run dev
```

**8. Abrir el navegador:**
- Vite mostrará una URL, generalmente: `http://localhost:5173`
- Presionar Ctrl/Cmd + Click en la URL o copiarla al navegador

**¡Deberían ver la página de bienvenida de Vite + React!**

---

### 1.4 Estructura del Proyecto (15 min)

**Abrir el proyecto en VS Code:**
```bash
code .
# o arrastrar la carpeta al VS Code
```

**Explicar la estructura de archivos:**

```
mi-primera-app-react/
├── node_modules/          # ⚠️ NO tocar - librerías instaladas
├── public/                # Archivos estáticos (imágenes, etc)
│   └── vite.svg
├── src/                   # 👈 AQUÍ trabajaremos
│   ├── assets/            # Imágenes, fonts, etc
│   ├── App.css            # Estilos del componente App
│   ├── App.jsx            # 🔴 Componente principal
│   ├── index.css          # Estilos globales
│   └── main.jsx           # 🔴 Punto de entrada
├── .gitignore
├── index.html             # 🔴 HTML principal
├── package.json           # Configuración y dependencias
└── vite.config.js         # Configuración de Vite
```

**Archivos más importantes:**

**1. `index.html` (raíz del proyecto):**
```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Vite + React</title>
  </head>
  <body>
    <div id="root"></div>  <!-- 👈 React se monta aquí -->
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

**2. `src/main.jsx` (punto de entrada):**
```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

**Explicar:**
- `ReactDOM.createRoot`: crea el punto de montaje de React
- `document.getElementById('root')`: busca el div con id "root" en index.html
- `<App />`: es nuestro componente principal
- `StrictMode`: activa advertencias útiles en desarrollo

**3. `src/App.jsx` (componente principal):**
*Lo veremos en detalle en la siguiente sección*

---

### 1.5 Limpiar el Proyecto Base (10 min)

**Vamos a eliminar el código de ejemplo para empezar desde cero.**

**PASO 1: Limpiar `src/App.jsx`**

Borrar TODO el contenido y escribir:

```jsx
function App() {
  return (
    <div>
      <h1>Mi Primera App en React</h1>
      <p>¡Hola mundo!</p>
    </div>
  )
}

export default App
```

**PASO 2: Limpiar `src/App.css`**

Borrar TODO el contenido (dejar el archivo vacío o con estilos básicos):

```css
/* App.css */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
}
```

**PASO 3: Limpiar `src/index.css`**

Borrar TODO y dejar solo:

```css
/* index.css */
body {
  margin: 0;
  padding: 20px;
  background-color: #f0f0f0;
}
```

**Guardar todos los archivos (Ctrl/Cmd + S)**

**Verificar en el navegador:**
- Debería mostrarse: "Mi Primera App en React" y "¡Hola mundo!"
- Si no se actualiza automáticamente, refrescar la página

---

## HORA 2: JSX y Reglas Fundamentales (60 min)

### 2.1 ¿Qué es JSX? (15 min)

**JSX = JavaScript XML**

Es una extensión de sintaxis que permite escribir código similar a HTML dentro de JavaScript.

**Ejemplo comparativo:**

**JavaScript puro (sin JSX):**
```javascript
const elemento = React.createElement('h1', null, 'Hola Mundo')
```

**Con JSX (mucho más legible):**
```jsx
const elemento = <h1>Hola Mundo</h1>
```

**JSX NO es HTML, es JavaScript disfrazado**

React transforma JSX en llamadas a `React.createElement()` detrás de escenas.

---

### 2.2 Reglas de JSX - MUY IMPORTANTE (25 min)

**REGLA 1: Un solo elemento raíz**

❌ **INCORRECTO:**
```jsx
function App() {
  return (
    <h1>Título</h1>
    <p>Párrafo</p>
  )
}
```

✅ **CORRECTO - Opción A: envolver en un div:**
```jsx
function App() {
  return (
    <div>
      <h1>Título</h1>
      <p>Párrafo</p>
    </div>
  )
}
```

✅ **CORRECTO - Opción B: usar Fragment:**
```jsx
function App() {
  return (
    <>
      <h1>Título</h1>
      <p>Párrafo</p>
    </>
  )
}
```

**Explicar Fragments:**
- `<> </>` es la sintaxis corta de `<React.Fragment>`
- No agrega un elemento extra al DOM
- Útil cuando no quieres un div innecesario

---

**REGLA 2: Cerrar todas las etiquetas**

❌ **INCORRECTO:**
```jsx
<img src="foto.jpg">
<input type="text">
<br>
```

✅ **CORRECTO:**
```jsx
<img src="foto.jpg" />
<input type="text" />
<br />
```

**En JSX, todas las etiquetas deben cerrarse, incluso las auto-cerradas.**

---

**REGLA 3: className en lugar de class**

❌ **INCORRECTO:**
```jsx
<div class="container">Contenido</div>
```

✅ **CORRECTO:**
```jsx
<div className="container">Contenido</div>
```

**¿Por qué?** `class` es una palabra reservada en JavaScript.

---

**REGLA 4: camelCase para atributos**

Atributos que en HTML tienen guiones, en JSX usan camelCase:

| HTML          | JSX           |
|---------------|---------------|
| `onclick`     | `onClick`     |
| `onchange`    | `onChange`    |
| `maxlength`   | `maxLength`   |
| `tabindex`    | `tabIndex`    |

❌ **INCORRECTO:**
```jsx
<button onclick={handleClick}>Click</button>
```

✅ **CORRECTO:**
```jsx
<button onClick={handleClick}>Click</button>
```

---

**REGLA 5: Interpolar JavaScript con llaves `{}`**

Puedes insertar expresiones JavaScript dentro de llaves:

```jsx
function App() {
  const nombre = "Juan"
  const edad = 25
  const esMayor = edad >= 18
  
  return (
    <div>
      <h1>Hola, {nombre}</h1>
      <p>Tienes {edad} años</p>
      <p>Resultado: {10 + 5}</p>
      <p>¿Es mayor de edad? {esMayor ? 'Sí' : 'No'}</p>
    </div>
  )
}
```

**Lo que puedes poner en `{}`:**
- Variables
- Operaciones matemáticas
- Operadores ternarios
- Llamadas a funciones
- Expresiones JavaScript válidas

**Lo que NO puedes poner:**
- Sentencias (if, for, while)
- Declaraciones de variables con let/const

---

**REGLA 6: Comentarios en JSX**

```jsx
function App() {
  return (
    <div>
      {/* Este es un comentario en JSX */}
      <h1>Título</h1>
      
      {/* 
        Comentario
        multilínea
      */}
      <p>Texto</p>
    </div>
  )
}
```

**Nota:** NO usar `<!-- -->` (comentarios HTML) en JSX.

---

### 2.3 Ejercicio Práctico: Tarjeta Personal (20 min)

**Objetivo:** Crear una tarjeta con información personal usando JSX.

**Modificar `src/App.jsx`:**

```jsx
function App() {
  // Variables con información
  const nombre = "María García"
  const profesion = "Desarrolladora Frontend"
  const edad = 28
  const ciudad = "Medellín"
  const habilidades = ["React", "JavaScript", "CSS"]
  const disponible = true
  
  return (
    <div>
      <h1>Perfil Profesional</h1>
      
      <div>
        <h2>{nombre}</h2>
        <p><strong>Profesión:</strong> {profesion}</p>
        <p><strong>Edad:</strong> {edad} años</p>
        <p><strong>Ciudad:</strong> {ciudad}</p>
        
        <p>
          <strong>Estado:</strong> {disponible ? '✅ Disponible' : '❌ No disponible'}
        </p>
        
        <h3>Habilidades:</h3>
        <p>{habilidades[0]}, {habilidades[1]}, {habilidades[2]}</p>
      </div>
    </div>
  )
}

export default App
```

**Pedir a los estudiantes:**
1. Cambiar los valores de las variables con su propia información
2. Agregar una nueva variable `email` y mostrarla
3. Agregar una expresión matemática (ej: años de experiencia = edad - 22)
4. Experimentar cambiando `disponible` a `false`

**Guardar y verificar en el navegador.**

¡Nos vemos en la Sesión 2! 🚀"
