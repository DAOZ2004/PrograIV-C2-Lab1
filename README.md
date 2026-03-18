# Integrantes:

**Andrea Yamileth Rodríguez Hernández   SMSS073124**

**Daniel Antonio Orellana Zelaya        SMSS086223**


# Sistema Inteligente de Control de Gastos



**Situación problemática:**

**Muchas personas, especialmente estudiantes universitarios, no llevan un control adecuado de sus gastos diarios. 
Esto provoca desorden financiero, falta de ahorro y dificultad para identificar en qué se está gastando el dinero.**



**Sector al que va dirigido:**

**-Estudiantes universitarios.**
**-Jóvenes independientes.**
**-Personas que desean mejorar su administración financiera.**



**Solución propuesta:**

**Se desarrolla una aplicación web con Vue.js que permite:**

**-Registrar ingresos y gastos.**
**-Clasificar los gastos.**
**-Visualizar el balance total.**
**-Mostrar alertas cuando los gastos superan los ingresos.**



**Funciones:**

**-Agregar movimientos (ingreso o gasto).**
**-Mostrar lista dinámica.**
**-Eliminar registros.**
**-Calcular balance automáticamente.**
**-Validar datos ingresados.**
**-Mostrar alertas visuales.**



# Preguntas:


**1-¿Qué es Vue.js? y funcion dentro de la página web desarrollada**

**Vue.js es un framework progresivo de JavaScript que permite crear interfaces dinámicas. 
En este sistema permite actualizar automáticamente los datos financieros sin recargar la página.**


**2-Variables reactivas:**

**°descripcion: texto del movimiento.**

**°monto: cantidad de dinero.**

**°tipo: ingreso o gasto.**

**°movimientos: lista de registros.**

**°error: mensajes de validación.**

**°balance: cálculo total.**


**3-v-bind vs v-model:**

**°v-bind: enlaza atributos dinámicos.**

**°v-model: conecta input con datos automáticamente.**


**4-Evento utilizado:**

**Se utiliza @click para agregar y eliminar movimientos.**


**5-Uso de v-for:**

**Se usa para recorrer los movimientos y mostrarlos en pantalla.**


**6-Uso de v-if:**

**Se usa para mostrar alertas cuando el balance es negativo.**


**7-Validación:**

**Se valida que:**

**°No haya campos vacíos**
**°El monto sea un número válido**
**°Esto evita errores en el sistema.**
