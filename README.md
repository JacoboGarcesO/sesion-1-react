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

---

## HORA 3: Componentes y Props (60 min)

### 3.1 ¿Qué es un Componente? (10 min)

**Definición:**
Un componente es una pieza independiente y reutilizable de la UI.

**Analogía:**
- Tu app es como una casa
- Los componentes son como ladrillos LEGO
- Puedes reutilizar el mismo "ladrillo" en diferentes partes

**Tipos de componentes:**
- **Funcionales** (los que usaremos): funciones que retornan JSX
- ~~Clase~~ (obsoletos, no los enseñaremos)

**Anatomía de un componente funcional:**

```jsx
function NombreDelComponente() {
  // Lógica del componente (opcional)
  
  return (
    // JSX que se renderizará
  )
}

export default NombreDelComponente
```

**Reglas para nombrar componentes:**
- ✅ SIEMPRE en PascalCase: `MiComponente`, `Header`, `UserCard`
- ❌ NO en camelCase: `miComponente`
- ❌ NO en minúsculas: `header`

---

### 3.2 Crear el Primer Componente (15 min)

**Crear un componente Header:**

**PASO 1: Crear carpeta `components` dentro de `src`**

```
src/
├── components/    # 👈 Nueva carpeta
├── App.jsx
└── ...
```

**PASO 2: Crear archivo `src/components/Header.jsx`**

```jsx
// Header.jsx
function Header() {
  return (
    <header>
      <h1>🚀 Mi Aplicación React</h1>
      <p>Bienvenido a mi primera app</p>
    </header>
  )
}

export default Header
```

**Explicar:**
- `function Header()`: define el componente
- `return (...)`: retorna el JSX
- `export default Header`: permite importarlo en otros archivos

---

**PASO 3: Importar y usar en `App.jsx`**

```jsx
// App.jsx
import Header from './components/Header'

function App() {
  return (
    <div>
      <Header />
      
      <main>
        <p>Contenido principal de la aplicación</p>
      </main>
    </div>
  )
}

export default App
```

**Explicar:**
- `import Header from './components/Header'`: importa el componente
- `<Header />`: usa el componente (como si fuera una etiqueta HTML)
- `./` significa "en la misma carpeta o subcarpeta"

**Guardar y verificar en el navegador.**

---

### 3.3 Props: Pasar Datos a Componentes (20 min)

**¿Qué son las Props?**
- Props = Properties (propiedades)
- Permiten pasar datos del componente padre al hijo
- Son como los argumentos de una función

**Ejemplo básico:**

**Crear `src/components/Saludo.jsx`:**

```jsx
// Saludo.jsx
function Saludo(props) {
  return (
    <div>
      <h2>Hola, {props.nombre}!</h2>
      <p>Tienes {props.edad} años</p>
    </div>
  )
}

export default Saludo
```

**Usar en `App.jsx`:**

```jsx
import Header from './components/Header'
import Saludo from './components/Saludo'

function App() {
  return (
    <div>
      <Header />
      
      <Saludo nombre="Carlos" edad={30} />
      <Saludo nombre="Ana" edad={25} />
      <Saludo nombre="Luis" edad={35} />
    </div>
  )
}

export default App
```

**Explicar:**
- `nombre="Carlos"`: prop de tipo string (entre comillas)
- `edad={30}`: prop de tipo number (entre llaves)
- El mismo componente `Saludo` se reutiliza 3 veces con datos diferentes

---

**Destructuring de Props (sintaxis moderna):**

En lugar de escribir `props.nombre`, `props.edad`... podemos desestructurar:

```jsx
// Saludo.jsx - FORMA MEJORADA
function Saludo({ nombre, edad }) {  // 👈 Destructuring
  return (
    <div>
      <h2>Hola, {nombre}!</h2>
      <p>Tienes {edad} años</p>
    </div>
  )
}

export default Saludo
```

**Más limpio y legible. ¡Usaremos siempre esta forma!**

---

**Props de diferentes tipos:**

```jsx
// Ejemplos de props
<Componente
  texto="Hola"           // String
  numero={42}            // Number
  booleano={true}        // Boolean
  array={[1, 2, 3]}      // Array
  objeto={{ x: 10 }}     // Object
  funcion={() => {}}     // Function
/>
```

**Recuerda:** Todo menos strings va entre llaves `{}`

---

### 3.4 Ejercicio: Componente Card (15 min)

**Crear un componente reutilizable de tarjeta de producto.**

**Crear `src/components/ProductCard.jsx`:**

```jsx
// ProductCard.jsx
function ProductCard({ nombre, precio, imagen, disponible }) {
  return (
    <div style={{ 
      border: '1px solid #ddd', 
      padding: '20px', 
      margin: '10px',
      borderRadius: '8px',
      width: '250px'
    }}>
      <img 
        src={imagen} 
        alt={nombre}
        style={{ width: '100%', height: '200px', objectFit: 'cover' }}
      />
      <h3>{nombre}</h3>
      <p style={{ fontSize: '20px', color: 'green', fontWeight: 'bold' }}>
        ${precio}
      </p>
      <p style={{ color: disponible ? 'green' : 'red' }}>
        {disponible ? '✅ En stock' : '❌ Agotado'}
      </p>
    </div>
  )
}

export default ProductCard
```

**Usar en `App.jsx`:**

```jsx
import Header from './components/Header'
import ProductCard from './components/ProductCard'

function App() {
  return (
    <div>
      <Header />
      
      <div style={{ display: 'flex', flexWrap: 'wrap' }}>
        <ProductCard
          nombre="Laptop HP"
          precio={1200}
          imagen="https://via.placeholder.com/250"
          disponible={true}
        />
        
        <ProductCard
          nombre="Mouse Logitech"
          precio={25}
          imagen="https://via.placeholder.com/250"
          disponible={false}
        />
        
        <ProductCard
          nombre="Teclado Mecánico"
          precio={80}
          imagen="https://via.placeholder.com/250"
          disponible={true}
        />
      </div>
    </div>
  )
}

export default App
```

**Pedir a los estudiantes:**
1. Agregar 2 productos más
2. Cambiar las imágenes (pueden usar https://picsum.photos/250 para imágenes random)
3. Modificar los estilos inline

---

## HORA 4: Estilos en React (60 min)

### 4.1 Formas de Aplicar Estilos (10 min)

**En React hay 3 formas principales:**

1. **Estilos inline** (objetos JavaScript)
2. **CSS externo** (archivos .css separados)
3. **CSS Modules** (CSS con scope local)

**Hoy veremos las 3 formas.**

---

### 4.2 Estilos Inline (15 min)

**Sintaxis:**

```jsx
<div style={{ propiedad: 'valor' }}>
  Contenido
</div>
```

**⚠️ Notar:**
- Doble llave: `{{ }}`
- Propiedades en camelCase: `backgroundColor`, `fontSize`
- Valores string entre comillas: `'red'`, `'20px'`
- Valores numéricos sin comillas: `20` (React asume px)

**Ejemplos:**

```jsx
function Boton() {
  const estiloBoton = {
    backgroundColor: '#007bff',
    color: 'white',
    padding: '10px 20px',
    border: 'none',
    borderRadius: '5px',
    fontSize: '16px',
    cursor: 'pointer'
  }
  
  return (
    <button style={estiloBoton}>
      Click aquí
    </button>
  )
}
```

**O directamente inline:**

```jsx
<button style={{
  backgroundColor: '#007bff',
  color: 'white',
  padding: '10px 20px'
}}>
  Click aquí
</button>
```

**Ventajas:**
- Rápido para estilos dinámicos
- No hay conflictos de nombres

**Desventajas:**
- Difícil de mantener en componentes grandes
- No soporta pseudo-clases (:hover, :active)
- No soporta media queries

---

### 4.3 CSS Externo (20 min)

**La forma más común y recomendada.**

**PASO 1: Crear un archivo CSS para el componente**

**Crear `src/components/Header.css`:**

```css
/* Header.css */
.header {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 30px;
  text-align: center;
  border-radius: 10px;
  margin-bottom: 20px;
}

.header h1 {
  margin: 0;
  font-size: 2.5rem;
}

.header p {
  margin: 10px 0 0 0;
  font-size: 1.1rem;
  opacity: 0.9;
}
```

**PASO 2: Importar el CSS en el componente**

```jsx
// Header.jsx
import './Header.css'  // 👈 Importar CSS

function Header() {
  return (
    <header className="header">  {/* 👈 usar className */}
      <h1>🚀 Mi Aplicación React</h1>
      <p>Bienvenido a mi primera app</p>
    </header>
  )
}

export default Header
```

**Guardar y ver los cambios en el navegador.**

---

**Ejercicio: Estilizar ProductCard**

**Crear `src/components/ProductCard.css`:**

```css
/* ProductCard.css */
.product-card {
  border: 2px solid #e0e0e0;
  padding: 20px;
  margin: 10px;
  border-radius: 12px;
  width: 250px;
  background-color: white;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s, box-shadow 0.2s;
}

.product-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.15);
}

.product-card img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 8px;
  margin-bottom: 15px;
}

.product-card h3 {
  margin: 10px 0;
  color: #333;
  font-size: 1.3rem;
}

.product-price {
  font-size: 24px;
  color: #28a745;
  font-weight: bold;
  margin: 10px 0;
}

.product-status {
  font-weight: 600;
  margin-top: 10px;
}

.in-stock {
  color: #28a745;
}

.out-of-stock {
  color: #dc3545;
}
```

**Actualizar `ProductCard.jsx`:**

```jsx
import './ProductCard.css'

function ProductCard({ nombre, precio, imagen, disponible }) {
  return (
    <div className="product-card">
      <img src={imagen} alt={nombre} />
      <h3>{nombre}</h3>
      <p className="product-price">${precio}</p>
      <p className={disponible ? 'product-status in-stock' : 'product-status out-of-stock'}>
        {disponible ? '✅ En stock' : '❌ Agotado'}
      </p>
    </div>
  )
}

export default ProductCard
```

**Notar:**
- Clases CSS dinámicas con operador ternario
- Múltiples clases separadas por espacio
- `:hover` funciona perfectamente

---

### 4.4 CSS Modules (15 min)

**CSS Modules: CSS con scope local (evita conflictos de nombres)**

**¿Qué problema resuelven?**

Si tienes dos componentes con la clase `.titulo`, se pisarán entre sí. CSS Modules previene esto.

**PASO 1: Crear archivo con extensión `.module.css`**

**Crear `src/components/Footer.module.css`:**

```css
/* Footer.module.css */
.footer {
  background-color: #2c3e50;
  color: white;
  padding: 30px;
  text-align: center;
  margin-top: 40px;
  border-radius: 10px;
}

.titulo {
  font-size: 1.5rem;
  margin-bottom: 10px;
}

.redes {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin-top: 15px;
}

.enlace {
  color: #3498db;
  text-decoration: none;
  font-weight: 600;
  transition: color 0.3s;
}

.enlace:hover {
  color: #5dade2;
}
```

**PASO 2: Importar como objeto y usar**

**Crear `src/components/Footer.jsx`:**

```jsx
import styles from './Footer.module.css'  // 👈 Importar como 'styles'

function Footer() {
  return (
    <footer className={styles.footer}>  {/* 👈 styles.nombreClase */}
      <h3 className={styles.titulo}>Síguenos en Redes</h3>
      <div className={styles.redes}>
        <a href="#" className={styles.enlace}>Twitter</a>
        <a href="#" className={styles.enlace}>Instagram</a>
        <a href="#" className={styles.enlace}>LinkedIn</a>
      </div>
      <p>© 2025 Mi App React</p>
    </footer>
  )
}

export default Footer
```

**Usar en `App.jsx`:**

```jsx
import Header from './components/Header'
import ProductCard from './components/ProductCard'
import Footer from './components/Footer'

function App() {
  return (
    <div>
      <Header />
      
      <div style={{ display: 'flex', flexWrap: 'wrap', justifyContent: 'center' }}>
        <ProductCard
          nombre="Laptop HP"
          precio={1200}
          imagen="https://picsum.photos/250/200"
          disponible={true}
        />
        <ProductCard
          nombre="Mouse Logitech"
          precio={25}
          imagen="https://picsum.photos/250/201"
          disponible={false}
        />
        <ProductCard
          nombre="Teclado Mecánico"
          precio={80}
          imagen="https://picsum.photos/250/202"
          disponible={true}
        />
      </div>
      
      <Footer />
    </div>
  )
}

export default App
```

**Verificar en el navegador: las clases tendrán nombres únicos generados automáticamente**

Ejemplo: `.Footer_footer__a8b3c` (previene conflictos)

---

**Comparación de las 3 formas:**

| Método | Ventajas | Desventajas | Cuándo usar |
|--------|----------|-------------|-------------|
| **Inline** | Rápido, dinámico | Sin :hover, difícil de mantener | Estilos dinámicos simples |
| **CSS externo** | Familiar, completo | Posibles conflictos de nombres | Proyectos pequeños-medianos |
| **CSS Modules** | Sin conflictos, escalable | Sintaxis diferente | Proyectos medianos-grandes |

---

### 4.5 Proyecto Guiado Final: Landing Page

**Objetivo:** Crear una landing page simple integrando todo lo aprendido.

**Estructura:**
- Header (ya lo tenemos)
- Sección Hero
- Grid de productos (ya lo tenemos)
- Footer (ya lo tenemos)

**Crear `src/components/Hero.jsx`:**

```jsx
import './Hero.css'

function Hero({ titulo, subtitulo, textoBoton }) {
  return (
    <section className="hero">
      <h1>{titulo}</h1>
      <p>{subtitulo}</p>
      <button className="hero-button">{textoBoton}</button>
    </section>
  )
}

export default Hero
```

**Crear `src/components/Hero.css`:**

```css
/* Hero.css */
.hero {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 80px 20px;
  text-align: center;
  border-radius: 15px;
  margin-bottom: 40px;
}

.hero h1 {
  font-size: 3rem;
  margin: 0 0 20px 0;
  font-weight: 800;
}

.hero p {
  font-size: 1.3rem;
  margin-bottom: 30px;
  opacity: 0.95;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}

.hero-button {
  background-color: white;
  color: #667eea;
  padding: 15px 40px;
  font-size: 1.1rem;
  font-weight: 600;
  border: none;
  border-radius: 30px;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.hero-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
}

.hero-button:active {
  transform: translateY(-1px);
}
```

---

**Crear `src/App.css` (estilos del contenedor principal):**

```css
/* App.css */
.app-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f8f9fa;
  min-height: 100vh;
}

.products-section {
  margin: 40px 0;
}

.products-title {
  text-align: center;
  font-size: 2.5rem;
  color: #2c3e50;
  margin-bottom: 30px;
}

.products-grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 20px;
}
```

---

**Actualizar `src/App.jsx` (versión final integrada):**

```jsx
import './App.css'
import Header from './components/Header'
import Hero from './components/Hero'
import ProductCard from './components/ProductCard'
import Footer from './components/Footer'

function App() {
  return (
    <div className="app-container">
      <Header />
      
      <Hero 
        titulo="Bienvenido a TechStore"
        subtitulo="Los mejores productos de tecnología al mejor precio"
        textoBoton="Ver Catálogo"
      />
      
      <section className="products-section">
        <h2 className="products-title">Nuestros Productos</h2>
        
        <div className="products-grid">
          <ProductCard
            nombre="Laptop HP Pavilion"
            precio={1200}
            imagen="https://picsum.photos/250/200?random=1"
            disponible={true}
          />
          
          <ProductCard
            nombre="Mouse Logitech MX"
            precio={25}
            imagen="https://picsum.photos/250/200?random=2"
            disponible={false}
          />
          
          <ProductCard
            nombre="Teclado Mecánico"
            precio={80}
            imagen="https://picsum.photos/250/200?random=3"
            disponible={true}
          />
          
          <ProductCard
            nombre="Monitor Samsung 27"
            precio={350}
            imagen="https://picsum.photos/250/200?random=4"
            disponible={true}
          />
          
          <ProductCard
            nombre="Webcam Logitech 4K"
            precio={120}
            imagen="https://picsum.photos/250/200?random=5"
            disponible={true}
          />
          
          <ProductCard
            nombre="Auriculares Sony"
            precio={200}
            imagen="https://picsum.photos/250/200?random=6"
            disponible={false}
          />
        </div>
      </section>
      
      <Footer />
    </div>
  )
}

export default App
```

---

**Actualizar `src/index.css` (estilos globales):**

```css
/* index.css */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #ecf0f1;
  color: #2c3e50;
  line-height: 1.6;
}

h1, h2, h3, h4, h5, h6 {
  font-weight: 700;
}

button {
  font-family: inherit;
}
```

---

## EJERCICIOS PRÁCTICOS PARA LOS ESTUDIANTES

### Ejercicio 1: Crear componente InfoCard

**Instrucciones:**
1. Crear un nuevo componente llamado `InfoCard.jsx` en la carpeta `components`
2. El componente debe recibir props: `icono`, `titulo`, `descripcion`
3. Crear estilos en `InfoCard.css`
4. Mostrar 3 tarjetas en `App.jsx` con información diferente

**Ejemplo de uso:**
```jsx
<InfoCard 
  icono="🚀"
  titulo="Envío Rápido"
  descripcion="Entrega en 24-48 horas"
/>
```

**Solución (para mostrar después):**

```jsx
// InfoCard.jsx
import './InfoCard.css'

function InfoCard({ icono, titulo, descripcion }) {
  return (
    <div className="info-card">
      <div className="info-icono">{icono}</div>
      <h3 className="info-titulo">{titulo}</h3>
      <p className="info-descripcion">{descripcion}</p>
    </div>
  )
}

export default InfoCard
```

```css
/* InfoCard.css */
.info-card {
  background-color: white;
  padding: 30px;
  border-radius: 12px;
  text-align: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s;
  width: 280px;
}

.info-card:hover {
  transform: translateY(-5px);
}

.info-icono {
  font-size: 3rem;
  margin-bottom: 15px;
}

.info-titulo {
  color: #667eea;
  margin-bottom: 10px;
  font-size: 1.3rem;
}

.info-descripcion {
  color: #666;
  font-size: 0.95rem;
}
```

---

### Ejercicio 2: Personalizar la Landing Page

**Pedir a los estudiantes que:**
1. Cambien los colores del gradiente en Hero
2. Agreguen su propio texto en Hero
3. Cambien los productos con sus propios datos
4. Agreguen al menos 2 productos más
5. Modifiquen el Footer con sus redes sociales

---

### Ejercicio 3: Crear componente Button reutilizable

**Objetivo:** Crear un botón reutilizable con diferentes variantes.

**Instrucciones:**
1. Crear `Button.jsx` que reciba props: `texto`, `tipo` (puede ser 'primary', 'secondary', 'danger')
2. Aplicar diferentes estilos según el tipo
3. Usar el componente en diferentes partes de la app

**Solución:**

```jsx
// Button.jsx
import './Button.css'

function Button({ texto, tipo = 'primary' }) {
  return (
    <button className={`btn btn-${tipo}`}>
      {texto}
    </button>
  )
}

export default Button
```

```css
/* Button.css */
.btn {
  padding: 12px 30px;
  font-size: 1rem;
  font-weight: 600;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s;
}

.btn-primary {
  background-color: #667eea;
  color: white;
}

.btn-primary:hover {
  background-color: #5568d3;
}

.btn-secondary {
  background-color: #95a5a6;
  color: white;
}

.btn-secondary:hover {
  background-color: #7f8c8d;
}

.btn-danger {
  background-color: #e74c3c;
  color: white;
}

.btn-danger:hover {
  background-color: #c0392b;
}
```

**Uso:**
```jsx
<Button texto="Comprar Ahora" tipo="primary" />
<Button texto="Ver Más" tipo="secondary" />
<Button texto="Eliminar" tipo="danger" />
```

---

## RECAPITULACIÓN DE LA SESIÓN 1

### ¿Qué aprendimos hoy?

✅ **Configurar un proyecto React con Vite**
- Comando: `npm create vite@latest`
- Estructura de carpetas
- Iniciar servidor: `npm run dev`

✅ **JSX y sus reglas fundamentales**
- Un solo elemento raíz
- Cerrar todas las etiquetas
- `className` en lugar de `class`
- camelCase para atributos
- Interpolar JavaScript con `{}`
- Comentarios: `{/* */}`

✅ **Componentes**
- Son funciones que retornan JSX
- Nombres en PascalCase
- Import/Export de componentes
- Reutilización de componentes

✅ **Props**
- Pasar datos del padre al hijo
- Destructuring de props
- Props de diferentes tipos

✅ **Estilos en React**
- Inline styles (objetos JavaScript)
- CSS externo (archivos .css)
- CSS Modules (scope local)

✅ **Proyecto final: Landing Page**
- Header, Hero, ProductCard, Footer
- Composición de componentes
- Aplicación de estilos

---

## TAREA PARA CASA

**Proyecto: "Mi Portafolio Personal"**

Crear una landing page personal con:

1. **Componente Header**
   - Tu nombre
   - Subtítulo con tu profesión o aspiración

2. **Componente Hero**
   - Foto de perfil (pueden usar https://i.pravatar.cc/300 temporalmente)
   - Breve descripción sobre ti
   - Botón de "Contáctame"

3. **Componente SkillCard (crear 4-6 tarjetas)**
   - Props: `icono`, `nombreSkill`, `nivel` (Básico/Intermedio/Avanzado)
   - Mostrar diferentes habilidades

4. **Componente ProjectCard (crear 3 proyectos)**
   - Props: `titulo`, `descripcion`, `imagen`, `tecnologias`
   - Pueden ser proyectos reales o ficticios

5. **Componente Footer**
   - Links a redes sociales
   - Email de contacto

**Requisitos técnicos:**
- Usar al menos 5 componentes diferentes
- Aplicar estilos con CSS externo o CSS Modules
- Usar props correctamente
- Código limpio y organizado

**Bonus (opcional):**
- Agregar hover effects
- Usar CSS Modules en todos los componentes
- Hacer el diseño responsive (usar media queries)

---

## RECURSOS ADICIONALES

**Documentación:**
- React Docs: https://react.dev
- Vite Docs: https://vitejs.dev

**Herramientas útiles:**
- Placeholder de imágenes: https://picsum.photos
- Placeholder de avatares: https://i.pravatar.cc
- Íconos emoji: pueden usar emojis directos (🚀, 💻, 📱)

**Para la próxima sesión necesitarán:**
- El proyecto de hoy funcionando
- Node.js y npm funcionando correctamente
- Ganas de aprender sobre estado (useState) y formularios

---

## SOLUCIÓN DE PROBLEMAS COMUNES

### Error: "Module not found"
- Verificar que la ruta del import sea correcta
- Verificar que el archivo exista
- Verificar la extensión (.jsx)

### Error: "Unexpected token"
- Falta cerrar una llave `}`
- Falta cerrar un paréntesis `)`
- Falta cerrar una etiqueta JSX

### El componente no se muestra
- Verificar que se esté importando correctamente
- Verificar que tenga `export default`
- Verificar que se esté usando como `<NombreComponente />`

### Los estilos no se aplican
- Verificar que el CSS esté importado
- Verificar que las clases estén escritas correctamente
- Verificar que se use `className` y no `class`

### Hot reload no funciona
- Guardar todos los archivos (Ctrl/Cmd + S)
- Refrescar el navegador manualmente
- Reiniciar el servidor: Ctrl+C y luego `npm run dev`

---

## PREGUNTAS FRECUENTES

**P: ¿Puedo usar HTML normal en lugar de JSX?**
R: No, React usa JSX. Pero JSX es muy similar a HTML, solo con algunas diferencias (className, cerrar etiquetas, etc.)

**P: ¿Debo usar siempre CSS Modules?**
R: No es obligatorio. Puedes usar CSS normal. CSS Modules es útil en proyectos grandes para evitar conflictos.

**P: ¿Puedo nombrar mis componentes en minúscula?**
R: NO. React requiere que los componentes empiecen con mayúscula (PascalCase). Si usas minúscula, React pensará que es una etiqueta HTML.

**P: ¿Cuántos componentes debo crear?**
R: Divide la UI en piezas lógicas. Si un componente se vuelve muy grande (más de 150 líneas), considera dividirlo.

**P: ¿Puedo usar Bootstrap o Tailwind?**
R: Sí, pero por ahora enfócate en CSS puro para entender bien los conceptos. En sesiones futuras podrías explorar frameworks CSS.

---

## CHECKLIST DE FIN DE SESIÓN

Antes de terminar, verificar que todos los estudiantes:

- ✅ Tienen el proyecto funcionando en su computadora
- ✅ Pueden crear un componente nuevo
- ✅ Entienden cómo pasar props
- ✅ Pueden aplicar estilos de al menos 2 formas
- ✅ Tienen claro qué es JSX y sus reglas básicas
- ✅ Saben importar y exportar componentes
- ✅ Tienen la tarea clara

---

## CÓDIGO COMPLETO DE REFERENCIA

**Estructura final del proyecto después de la Sesión 1:**

```
mi-primera-app-react/
├── node_modules/
├── public/
├── src/
│   ├── components/
│   │   ├── Header.jsx
│   │   ├── Header.css
│   │   ├── Hero.jsx
│   │   ├── Hero.css
│   │   ├── ProductCard.jsx
│   │   ├── ProductCard.css
│   │   ├── Footer.jsx
│   │   └── Footer.module.css
│   ├── App.jsx
│   ├── App.css
│   ├── index.css
│   └── main.jsx
├── index.html
├── package.json
└── vite.config.js
```

---

## NOTAS PARA EL INSTRUCTOR

**Timing sugerido:**
- No apresurarse en los conceptos fundamentales (JSX, componentes)
- Dejar tiempo para que practiquen escribiendo código
- Circular por el salón para ayudar individualmente
- Hacer pausas cada 45-50 minutos

**Puntos críticos a enfatizar:**
- Importancia de `className` vs `class`
- Cerrar todas las etiquetas en JSX
- Nombres de componentes en PascalCase
- Props son inmutables (solo lectura)
- Un componente debe retornar UN solo elemento raíz

**Errores comunes a anticipar:**
- Olvidar importar componentes
- Olvidar exportar componentes
- Usar `class` en lugar de `className`
- No cerrar etiquetas auto-cerradas
- Olvidar las llaves en props numéricas: `edad={25}` no `edad="25"`

**Motivación:**
- Celebrar cuando logren crear su primer componente
- Mostrar entusiasmo por sus progresos
- Recordarles que es normal sentirse abrumados al principio
- Enfatizar que con práctica todo se vuelve natural

---

## FIN DE LA SESIÓN 1

**Mensaje final para los estudiantes:**

"¡Felicidades! Han completado la primera sesión de React. Hoy sentaron las bases fundamentales: saben crear componentes, pasar datos con props, y aplicar estilos. Estos son los bloques de construcción de CUALQUIER aplicación React, por simple o compleja que sea.

En la próxima sesión aprenderemos a hacer que nuestras apps sean interactivas con `useState` y formularios. Será emocionante ver cómo sus componentes cobran vida.

Recuerden hacer la tarea del portafolio personal. No tiene que ser perfecto, lo importante es practicar lo que aprendimos hoy.

¡Nos vemos en la Sesión 2! 🚀"
