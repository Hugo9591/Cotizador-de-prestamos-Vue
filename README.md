# Cotizador de Préstamos en Vue
Este es un cotizador de préstamos hecho con Vue.js que permite al usuario simular cuánto pagaría dependiendo del monto y plazo del préstamo. La interfaz se actualiza en tiempo real y está diseñada con Tailwind CSS.

## Funcionalidades

- Input tipo range para elegir el monto del préstamo (inicia desde $10,000).
- Botones "+" y "−" para ajustar el monto en intervalos de $100.
- Select para elegir el plazo de pago (6, 12 o 24 meses).
- El cálculo varía según:
  - A mayor plazo, mayor interés.
  - A mayor monto, menor interés.
- Muestra automáticamente:
  - Total a pagar
  - Cuánto pagaría por mes
- Todo se actualiza en tiempo real conforme el usuario cambia los valores.

## Tecnologías utilizadas

- Vue
- Tailwind CSS
- Vite
- JavaScript


## Estructura del proyecto
src/
  - components/
    - Header.vue
    - Button.vue

helpers/
  - index.js // Lógica del cálculo

App.vue

main.js

style.css // Estilos con Tailwind


## Instalación y ejecución

1. Clona el repositorio:
   git clone https://github.com/Hugo9591/Cotizador-de-prestamos-Vue.git

2. Instala dependencias:
  npm install

3. Ejecuta el servidor de desarrollo:
  npm run dev

Notas
La lógica de cálculo del préstamo está separada en un archivo js para mantener el código limpio.

Los componentes están diseñados para ser reutilizables.

Tailwind CSS se instaló y configuró para estilizar toda la interfaz de manera rápida y moderna.
