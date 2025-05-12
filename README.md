# ClikerGame

```markdown
# 📝 Clicker Game - Requisitos y Estructura

## 🛠️ Tecnologías
- **HTML5**: Estructura básica del juego.
- **CSS3**: Estilos, animaciones y diseño responsive.
- **JavaScript**: Lógica del juego (contador, mejoras, etc.).
- **Opcional**: 
  - `localStorage` para guardar el progreso.
  - Librerías como [SweetAlert2](https://sweetalert2.github.io/) para notificaciones.

---

## 📂 Estructura del Proyecto
```
clicker-game/
├── index.html          # Estructura principal
├── style.css           # Estilos
├── script.js           # Lógica del juego
└── assets/             # (Opcional) Imágenes/iconos
```

---

## 📄 **HTML** (`index.html`)
```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Clicker Game</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <h1>Clicker Game</h1>
        <div class="counter" id="counter">0</div>
        <button class="click-btn" id="clickBtn">¡Haz Click!</button>
        
        <div class="upgrades">
            <h2>Mejoras</h2>
            <button class="upgrade-btn" id="autoClicker">Auto-Clicker (10 puntos)</button>
            <button class="upgrade-btn" id="doublePoints">Doble Puntos (25 puntos)</button>
        </div>
    </div>
    <script src="script.js"></script>
</body>
</html>
```

---

## 🎨 **CSS** (`style.css`)
```css
body {
    font-family: 'Arial', sans-serif;
    background-color: #f0f0f0;
    text-align: center;
    margin: 0;
    padding: 20px;
}

.container {
    background-color: white;
    border-radius: 10px;
    padding: 20px;
    max-width: 600px;
    margin: 0 auto;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.counter {
    font-size: 3rem;
    margin: 20px 0;
    color: #333;
}

.click-btn {
    background-color: #4CAF50;
    color: white;
    border: none;
    padding: 15px 30px;
    font-size: 1.2rem;
    border-radius: 5px;
    cursor: pointer;
    transition: transform 0.1s;
}

.click-btn:hover {
    background-color: #45a049;
}

.click-btn:active {
    transform: scale(0.95);
}

.upgrades {
    margin-top: 30px;
}

.upgrade-btn {
    background-color: #2196F3;
    color: white;
    border: none;
    padding: 10px 20px;
    margin: 5px;
    border-radius: 5px;
    cursor: pointer;
}

.upgrade-btn:hover {
    background-color: #0b7dda;
}

.upgrade-btn:disabled {
    background-color: #cccccc;
    cursor: not-allowed;
}
```

---

## ⚙️ **JavaScript** (`script.js`)
```javascript
// Variables del juego
let points = 0;
let clickValue = 1;
let autoClickerInterval;
let autoClickerActive = false;

// Elementos del DOM
const counter = document.getElementById('counter');
const clickBtn = document.getElementById('clickBtn');
const autoClickerBtn = document.getElementById('autoClicker');
const doublePointsBtn = document.getElementById('doublePoints');

// Actualizar el contador
function updateCounter() {
    counter.textContent = points;
}

// Evento de click
clickBtn.addEventListener('click', () => {
    points += clickValue;
    updateCounter();
});

// Mejora: Auto-Clicker
autoClickerBtn.addEventListener('click', () => {
    if (points >= 10 && !autoClickerActive) {
        points -= 10;
        autoClickerActive = true;
        autoClickerBtn.disabled = true;
        autoClickerInterval = setInterval(() => {
            points += clickValue;
            updateCounter();
        }, 1000); // Click automático cada segundo
        updateCounter();
    }
});

// Mejora: Doble Puntos
doublePointsBtn.addEventListener('click', () => {
    if (points >= 25) {
        points -= 25;
        clickValue *= 2;
        doublePointsBtn.disabled = true;
        updateCounter();
    }
});

// Inicializar
updateCounter();
```

---

## ✨ **Extras para Mejorar**
1. **Guardar progreso**:
   ```javascript
   // Al cargar la página
   if (localStorage.getItem('points')) {
       points = parseInt(localStorage.getItem('points'));
       clickValue = parseInt(localStorage.getItem('clickValue'));
       updateCounter();
   }

   // Guardar al cerrar la página
   window.addEventListener('beforeunload', () => {
       localStorage.setItem('points', points);
       localStorage.setItem('clickValue', clickValue);
   });
   ```

2. **Animaciones al hacer click**:
   ```css
   .click-btn:active {
       transform: scale(0.9);
   }
   ```

3. **Sonidos**:
   ```javascript
   const clickSound = new Audio('assets/click.mp3');
   clickBtn.addEventListener('click', () => {
       clickSound.play();
   });
   ```

---

## 🚀 **Despliegue en GitHub Pages**
1. Sube el proyecto a un repositorio en GitHub.
2. Ve a `Settings > Pages` y activa GitHub Pages en la rama `main`.

¡Listo! Ahora tienes un **Clicker Game** funcional y personalizable. 🎮
``` 

### 📌 **Ideas para Expandirlo**
- Añadir más mejoras (ej: multiplicadores temporales).
- Implementar logros (ej: "100 clicks").
- Diseño temático (ej: espacio, fantasía).