<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¿Quieres ser mi novia?</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: Arial, sans-serif;
            background-color: #f0f8ff;
        }

        #contenedor-pregunta {
            text-align: center;
            margin-bottom: 20px;
        }

        #botones-container {
            position: relative; /* Necesario para el posicionamiento absoluto del botón 'No' */
            width: 300px; /* Ancho para que los botones no se salgan del área de juego */
            height: 100px; /* Alto para que los botones no se salgan del área de juego */
            display: flex;
            justify-content: space-around;
            align-items: center;
        }

        button {
            padding: 10px 20px;
            font-size: 18px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
            transition: background-color 0.3s ease;
        }

        #btnSi {
            background-color: #4CAF50; /* Verde */
            color: white;
        }

        #btnNo {
            background-color: #f44336; /* Rojo */
            color: white;
            position: absolute; /* Para moverlo con JavaScript */
            transition: top 0.1s, left 0.1s; /* Transición suave al moverse */
        }
        
        #btnSi:hover {
            background-color: #45a049;
        }
        
        /* Oculta los mensajes al inicio */
        #mensaje-si, #mensaje-error {
            display: none;
            margin-top: 20px;
            padding: 15px;
            border-radius: 8px;
            font-weight: bold;
        }

        #mensaje-si {
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        #mensaje-error {
            background-color: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
    </style>
</head>
<body>

    <div id="contenedor-pregunta">
        <h1>¿Quieres ser mi novia? ❤️</h1>
    </div>

    <div id="botones-container">
        <button id="btnSi" onclick="aceptar()">Sí</button>
        <button id="btnNo" onclick="moverBotonNo()">No</button>
    </div>

    <div id="mensaje-si">
        ¡SÍ! ¡Sabía que dirías que sí! 🎉🎊
    </div>
    
    <div id="mensaje-error">
        ¡Error! Tienes que presionar el botón "Sí". 😉
    </div>

    <script>
        const btnNo = document.getElementById('btnNo');
        const container = document.getElementById('botones-container');
        const mensajeSi = document.getElementById('mensaje-si');
        const mensajeError = document.getElementById('mensaje-error');

        // Mueve el botón "No" a una posición aleatoria dentro del contenedor
        function moverBotonNo() {
            // Oculta el mensaje de "Sí" y muestra el de "Error" temporalmente
            mensajeSi.style.display = 'none';
            mensajeError.style.display = 'block';
            setTimeout(() => {
                mensajeError.style.display = 'none';
            }, 1000); // Oculta el mensaje de error después de 1 segundo
            
            // Obtiene las dimensiones del contenedor y del botón
            const containerRect = container.getBoundingClientRect();
            const btnRect = btnNo.getBoundingClientRect();

            // Calcula el rango de movimiento (para que el botón no se salga)
            const maxLeft = containerRect.width - btnRect.width;
            const maxTop = containerRect.height - btnRect.height;

            // Genera nuevas posiciones aleatorias
            // Se usa Math.random() para obtener un número entre 0 y 1.
            // Al multiplicarlo por maxLeft/maxTop, se obtiene una posición dentro del rango.
            const newLeft = Math.floor(Math.random() * maxLeft);
            const newTop = Math.floor(Math.random() * maxTop);

            // Aplica las nuevas posiciones al botón "No"
            btnNo.style.left = `${newLeft}px`;
            btnNo.style.top = `${newTop}px`;
        }

        // Función para el botón "Sí"
        function aceptar() {
            // Muestra el mensaje de éxito y oculta el de error
            mensajeSi.style.display = 'block';
            mensajeError.style.display = 'none';
            // Opcional: Centra el botón "No" y lo deshabilita después de aceptar
            btnNo.style.position = 'static'; 
            btnNo.style.visibility = 'hidden';
            
            // También podemos deshabilitar el botón "Sí" para que no se presione de nuevo
            document.getElementById('btnSi').disabled = true;
        }
        
        // Coloca el botón 'No' inicialmente en una posición inicial
        window.onload = function() {
             // Mueve a una posición inicial centrada horizontalmente para que no se superponga
             // Puedes ajustar estos valores si lo deseas
             btnNo.style.left = '180px'; 
             btnNo.style.top = '30px';
        };

    </script>
</body>
</html>
