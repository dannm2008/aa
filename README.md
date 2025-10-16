<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trivilocura</title>
    <style>
        :root {
            --azul-principal: #6a8caf;
            --azul-secundario: #3a5a78;
            --morado-principal: #957fef;
            --morado-secundario: #7161ef;
            --rosa: #ff85a1;
            --verde: #8fbc8f;
            --amarillo: #ffd166;
            --rojo: #ff6b6b;
            --naranja: #ff9e64;
            --blanco: #f8f9fa;
            --negro: #212529;
            --sombra: 0 4px 15px rgba(0, 0, 0, 0.2);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Comic Sans MS', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, var(--morado-principal), var(--rosa), var(--naranja));
            color: var(--blanco);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            overflow-x: hidden;
        }

        .container {
            max-width: 900px;
            width: 100%;
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border-radius: 25px;
            padding: 30px;
            box-shadow: var(--sombra);
            margin-top: 20px;
            border: 3px dashed var(--amarillo);
            position: relative;
            overflow: hidden;
        }

        h1 {
            text-align: center;
            font-size: 3.5rem;
            margin-bottom: 10px;
            text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
            background: linear-gradient(to right, var(--rosa), var(--naranja), var(--amarillo));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .subtitle {
            text-align: center;
            margin-bottom: 30px;
            font-size: 1.3rem;
            color: var(--blanco);
            text-shadow: 0 1px 3px rgba(0, 0, 0, 0.3);
        }

        .pantalla {
            display: none;
        }

        .pantalla.activa {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .categorias {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }

        .categoria {
            background: rgba(255, 255, 255, 0.2);
            border-radius: 20px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid transparent;
        }

        .categoria:hover {
            transform: scale(1.05);
            border-color: var(--amarillo);
        }

        .categoria h3 {
            font-size: 1.4rem;
            margin-bottom: 10px;
        }

        .icono {
            font-size: 2.5rem;
            margin-bottom: 15px;
        }

        .boton {
            background: linear-gradient(135deg, var(--rosa), var(--naranja));
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 50px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            margin: 10px;
        }

        .boton:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.3);
        }

        .boton-secundario {
            background: rgba(255, 255, 255, 0.2);
        }

        .centrar {
            display: flex;
            justify-content: center;
            margin-top: 20px;
        }

        .encabezado-juego {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px dashed rgba(255, 255, 255, 0.3);
        }

        .temporizador {
            font-size: 1.5rem;
            font-weight: bold;
            background: rgba(0, 0, 0, 0.3);
            padding: 8px 15px;
            border-radius: 10px;
            border: 2px solid var(--amarillo);
        }

        .puntaje {
            font-size: 1.3rem;
            background: rgba(0, 0, 0, 0.3);
            padding: 8px 15px;
            border-radius: 10px;
            border: 2px solid var(--amarillo);
        }

        .pregunta-contenedor {
            margin-bottom: 30px;
        }

        .pregunta-texto {
            font-size: 1.4rem;
            margin-bottom: 20px;
            line-height: 1.4;
            background: rgba(255, 255, 255, 0.1);
            padding: 20px;
            border-radius: 15px;
            border-left: 5px solid var(--rosa);
            text-align: center;
        }

        .opciones {
            display: grid;
            grid-template-columns: 1fr;
            gap: 15px;
        }

        .opcion {
            background: rgba(255, 255, 255, 0.15);
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 15px;
            padding: 15px 20px;
            cursor: pointer;
            transition: all 0.2s ease;
            display: flex;
            align-items: center;
        }

        .opcion:hover {
            background: rgba(255, 255, 255, 0.25);
        }

        .opcion.correcta {
            background: rgba(143, 188, 143, 0.3);
            border-color: var(--verde);
        }

        .opcion.incorrecta {
            background: rgba(255, 133, 161, 0.3);
            border-color: var(--rosa);
        }

        .letra-opcion {
            display: inline-flex;
            justify-content: center;
            align-items: center;
            width: 30px;
            height: 30px;
            background: var(--morado-principal);
            border-radius: 50%;
            margin-right: 15px;
            font-weight: bold;
        }

        .resultado-final {
            text-align: center;
            padding: 20px;
        }

        .resultado-final h2 {
            font-size: 2.5rem;
            margin-bottom: 20px;
            color: var(--amarillo);
        }

        .puntaje-final {
            font-size: 4rem;
            font-weight: bold;
            margin: 20px 0;
            color: var(--amarillo);
        }

        .resumen-correctas {
            font-size: 1.5rem;
            margin: 20px 0;
            color: var(--verde);
        }

        .oculto {
            display: none;
        }

        .numero-pregunta {
            display: inline-block;
            background: var(--naranja);
            color: white;
            padding: 8px 15px;
            border-radius: 50%;
            font-weight: bold;
            margin-bottom: 15px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Trivilocura</h1>
        <p class="subtitle">¡Pon a prueba tu conocimiento en esta trivia loca!</p>

        <!-- Pantalla de inicio -->
        <div id="pantalla-inicio" class="pantalla activa">
            <h2>¡Bienvenido a la Trivilocura!</h2>
            <p>Selecciona una categoría para comenzar. Tienes 15 segundos por pregunta.</p>
            
            <div class="categorias">
                <div class="categoria" data-categoria="mixta">
                    <div class="icono">🎲</div>
                    <h3>Preguntas Mixtas</h3>
                    <p>10 preguntas de todas las categorías</p>
                </div>
                <div class="categoria" data-categoria="historia">
                    <div class="icono">📜</div>
                    <h3>Historia</h3>
                    <p>10 preguntas sobre eventos históricos</p>
                </div>
                <div class="categoria" data-categoria="ciencia">
                    <div class="icono">🔬</div>
                    <h3>Ciencia</h3>
                    <p>10 preguntas sobre descubrimientos científicos</p>
                </div>
            </div>
        </div>

        <!-- Pantalla de juego -->
        <div id="pantalla-juego" class="pantalla">
            <div class="encabezado-juego">
                <div class="temporizador" id="temporizador">15</div>
                <div class="puntaje" id="puntaje">Puntos: 0</div>
            </div>
            
            <div class="pregunta-contenedor">
                <div class="numero-pregunta" id="numero-pregunta">1/10</div>
                <div class="pregunta-texto" id="pregunta-texto"></div>
                <div class="opciones" id="opciones-contenedor"></div>
            </div>
            
            <div class="centrar">
                <button id="btn-siguiente" class="boton oculto">Siguiente Pregunta</button>
            </div>
        </div>

        <!-- Pantalla de resultados -->
        <div id="pantalla-resultados" class="pantalla">
            <div class="resultado-final">
                <h2>¡Juego Terminado!</h2>
                <p>Tu puntuación final es:</p>
                <div class="puntaje-final" id="puntaje-final">0</div>
                <div class="resumen-correctas" id="resumen-correctas"></div>
                
                <div class="centrar">
                    <button id="btn-jugar-otra-vez" class="boton">Jugar Otra Vez</button>
                    <button id="btn-volver-inicio" class="boton boton-secundario">Volver al Inicio</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Base de datos de preguntas simplificada
        const preguntasBase = {
            mixta: [
                {
                    pregunta: "¿En qué año cayó el Imperio Romano de Occidente?",
                    opciones: ["410 d.C.", "476 d.C.", "1453 d.C.", "312 d.C."],
                    correcta: 1
                },
                {
                    pregunta: "¿Cuál es el planeta más grande del sistema solar?",
                    opciones: ["Saturno", "Neptuno", "Urano", "Júpiter"],
                    correcta: 3
                },
                {
                    pregunta: "¿Quién pintó 'La noche estrellada'?",
                    opciones: ["Pablo Picasso", "Claude Monet", "Salvador Dalí", "Vincent van Gogh"],
                    correcta: 3
                },
                {
                    pregunta: "¿Cuál es el río más largo del mundo?",
                    opciones: ["Nilo", "Misisipi", "Yangtsé", "Amazonas"],
                    correcta: 3
                },
                {
                    pregunta: "¿Cuánto es 8 x 7?",
                    opciones: ["64", "48", "72", "56"],
                    correcta: 3
                },
                {
                    pregunta: "¿Cómo se dice 'hola' en inglés?",
                    opciones: ["Goodbye", "Please", "Thank you", "Hello"],
                    correcta: 3
                },
                {
                    pregunta: "¿Quién descubrió América en 1492?",
                    opciones: ["Vasco da Gama", "Cristóbal Colón", "Fernando de Magallanes", "Américo Vespucio"],
                    correcta: 1
                },
                {
                    pregunta: "¿Qué científico descubrió la penicilina?",
                    opciones: ["Louis Pasteur", "Marie Curie", "Robert Koch", "Alexander Fleming"],
                    correcta: 3
                },
                {
                    pregunta: "¿En qué ciudad se encuentra el Museo del Prado?",
                    opciones: ["Barcelona", "París", "Roma", "Madrid"],
                    correcta: 3
                },
                {
                    pregunta: "¿Cuál es la capital de Australia?",
                    opciones: ["Sídney", "Melbourne", "Brisbane", "Canberra"],
                    correcta: 3
                }
            ],
            historia: [
                {
                    pregunta: "¿En qué año cayó el Imperio Romano de Occidente?",
                    opciones: ["410 d.C.", "476 d.C.", "1453 d.C.", "312 d.C."],
                    correcta: 1
                },
                {
                    pregunta: "¿Quién descubrió América en 1492?",
                    opciones: ["Vasco da Gama", "Cristóbal Colón", "Fernando de Magallanes", "Américo Vespucio"],
                    correcta: 1
                },
                {
                    pregunta: "¿En qué año comenzó la Primera Guerra Mundial?",
                    opciones: ["1918", "1939", "1914", "1945"],
                    correcta: 2
                },
                {
                    pregunta: "¿Quién fue el primer presidente de los Estados Unidos?",
                    opciones: ["Thomas Jefferson", "Abraham Lincoln", "George Washington", "John Adams"],
                    correcta: 2
                },
                {
                    pregunta: "¿Qué civilización construyó Machu Picchu?",
                    opciones: ["Maya", "Azteca", "Inca", "Olmeca"],
                    correcta: 2
                },
                {
                    pregunta: "¿En qué año se firmó la Declaración de Independencia de los Estados Unidos?",
                    opciones: ["1789", "1812", "1492", "1776"],
                    correcta: 3
                },
                {
                    pregunta: "¿Quién pintó la Mona Lisa?",
                    opciones: ["Miguel Ángel", "Rafael", "Leonardo da Vinci", "Donatello"],
                    correcta: 2
                },
                {
                    pregunta: "¿Qué imperio fue gobernado por Julio César?",
                    opciones: ["Imperio Bizantino", "Imperio Otomano", "Imperio Romano", "Imperio Mongol"],
                    correcta: 2
                },
                {
                    pregunta: "¿En qué año terminó la Segunda Guerra Mundial?",
                    opciones: ["1939", "1918", "1950", "1945"],
                    correcta: 3
                },
                {
                    pregunta: "¿Quién fue el primer hombre en pisar la Luna?",
                    opciones: ["Buzz Aldrin", "Yuri Gagarin", "Alan Shepard", "Neil Armstrong"],
                    correcta: 3
                }
            ],
            ciencia: [
                {
                    pregunta: "¿Cuál es el elemento más abundante en el universo?",
                    opciones: ["Oxígeno", "Carbono", "Hidrógeno", "Helio"],
                    correcta: 2
                },
                {
                    pregunta: "¿Quién formuló la teoría de la relatividad?",
                    opciones: ["Isaac Newton", "Stephen Hawking", "Albert Einstein", "Galileo Galilei"],
                    correcta: 2
                },
                {
                    pregunta: "¿Cuál es el planeta más grande del sistema solar?",
                    opciones: ["Saturno", "Neptuno", "Urano", "Júpiter"],
                    correcta: 3
                },
                {
                    pregunta: "¿Qué científico descubrió la penicilina?",
                    opciones: ["Louis Pasteur", "Marie Curie", "Robert Koch", "Alexander Fleming"],
                    correcta: 3
                },
                {
                    pregunta: "¿Cuál es la unidad básica de la vida?",
                    opciones: ["El átomo", "La molécula", "El gen", "La célula"],
                    correcta: 3
                },
                {
                    pregunta: "¿Qué partícula subatómica tiene carga positiva?",
                    opciones: ["Electrón", "Neutrón", "Fotón", "Protón"],
                    correcta: 3
                },
                {
                    pregunta: "¿Qué gas necesitan las plantas para realizar la fotosíntesis?",
                    opciones: ["Oxígeno", "Nitrógeno", "Hidrógeno", "Dióxido de carbono"],
                    correcta: 3
                },
                {
                    pregunta: "¿Cuál es el hueso más largo del cuerpo humano?",
                    opciones: ["Tibia", "Húmero", "Radio", "Fémur"],
                    correcta: 3
                },
                {
                    pregunta: "¿Qué planeta es conocido como el planeta rojo?",
                    opciones: ["Júpiter", "Venus", "Saturno", "Marte"],
                    correcta: 3
                },
                {
                    pregunta: "¿Qué tipo de animal es una ballena?",
                    opciones: ["Pez", "Reptil", "Anfibio", "Mamífero"],
                    correcta: 3
                }
            ]
        };

        // Variables del juego
        let categoriaActual = '';
        let preguntasActuales = [];
        let preguntaActual = 0;
        let puntuacion = 0;
        let temporizador;
        let tiempoRestante = 15;
        let respuestasCorrectas = 0;

        // Elementos DOM
        const pantallaInicio = document.getElementById('pantalla-inicio');
        const pantallaJuego = document.getElementById('pantalla-juego');
        const pantallaResultados = document.getElementById('pantalla-resultados');
        
        const btnSiguiente = document.getElementById('btn-siguiente');
        const btnJugarOtraVez = document.getElementById('btn-jugar-otra-vez');
        const btnVolverInicio = document.getElementById('btn-volver-inicio');
        
        const preguntaTexto = document.getElementById('pregunta-texto');
        const opcionesContenedor = document.getElementById('opciones-contenedor');
        const temporizadorElemento = document.getElementById('temporizador');
        const puntajeElemento = document.getElementById('puntaje');
        const puntajeFinal = document.getElementById('puntaje-final');
        const resumenCorrectas = document.getElementById('resumen-correctas');
        const numeroPregunta = document.getElementById('numero-pregunta');

        // Función para mezclar opciones aleatoriamente
        function mezclarOpciones(pregunta) {
            const opcionesMezcladas = [...pregunta.opciones];
            const respuestaCorrecta = opcionesMezcladas[pregunta.correcta];
            
            // Mezclar las opciones
            for (let i = opcionesMezcladas.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [opcionesMezcladas[i], opcionesMezcladas[j]] = [opcionesMezcladas[j], opcionesMezcladas[i]];
            }
            
            // Encontrar la nueva posición de la respuesta correcta
            const nuevaCorrecta = opcionesMezcladas.indexOf(respuestaCorrecta);
            
            return {
                pregunta: pregunta.pregunta,
                opciones: opcionesMezcladas,
                correcta: nuevaCorrecta
            };
        }

        // Event listeners para las categorías
        document.querySelectorAll('.categoria').forEach(categoria => {
            categoria.addEventListener('click', () => {
                categoriaActual = categoria.getAttribute('data-categoria');
                iniciarJuego();
            });
        });

        // Event listeners para los botones
        btnSiguiente.addEventListener('click', siguientePregunta);
        btnJugarOtraVez.addEventListener('click', iniciarJuego);
        btnVolverInicio.addEventListener('click', volverInicio);

        // Funciones del juego
        function iniciarJuego() {
            // Reiniciar variables
            preguntasActuales = [...preguntasBase[categoriaActual]];
            // Mezclar las preguntas y las opciones
            preguntasActuales = preguntasActuales.map(pregunta => mezclarOpciones(pregunta));
            mezclarPreguntas(preguntasActuales);
            
            preguntaActual = 0;
            puntuacion = 0;
            respuestasCorrectas = 0;
            
            // Actualizar UI
            puntajeElemento.textContent = `Puntos: ${puntuacion}`;
            
            // Cambiar pantalla
            cambiarPantalla(pantallaJuego);
            
            // Mostrar primera pregunta
            mostrarPregunta();
        }

        function mezclarPreguntas(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }

        function mostrarPregunta() {
            // Reiniciar temporizador
            clearInterval(temporizador);
            tiempoRestante = 15;
            temporizadorElemento.textContent = tiempoRestante;
            
            // Actualizar número de pregunta
            numeroPregunta.textContent = `${preguntaActual + 1}/${preguntasActuales.length}`;
            
            // Obtener pregunta actual
            const pregunta = preguntasActuales[preguntaActual];
            
            // Mostrar pregunta
            preguntaTexto.textContent = pregunta.pregunta;
            
            // Limpiar opciones anteriores
            opcionesContenedor.innerHTML = '';
            
            // Crear opciones
            const letras = ['A', 'B', 'C', 'D'];
            pregunta.opciones.forEach((opcion, index) => {
                const elementoOpcion = document.createElement('div');
                elementoOpcion.className = 'opcion';
                elementoOpcion.innerHTML = `
                    <div class="letra-opcion">${letras[index]}</div>
                    <div>${opcion}</div>
                `;
                
                elementoOpcion.addEventListener('click', () => {
                    seleccionarOpcion(index);
                });
                opcionesContenedor.appendChild(elementoOpcion);
            });
            
            // Ocultar botón siguiente
            btnSiguiente.classList.add('oculto');
            
            // Iniciar temporizador
            iniciarTemporizador();
        }

        function iniciarTemporizador() {
            temporizador = setInterval(() => {
                tiempoRestante--;
                temporizadorElemento.textContent = tiempoRestante;
                
                if (tiempoRestante <= 0) {
                    clearInterval(temporizador);
                    tiempoAgotado();
                }
            }, 1000);
        }

        function seleccionarOpcion(indice) {
            clearInterval(temporizador);
            
            const pregunta = preguntasActuales[preguntaActual];
            const opciones = document.querySelectorAll('.opcion');
            
            // Marcar respuesta correcta e incorrecta
            opciones[pregunta.correcta].classList.add('correcta');
            
            if (indice !== pregunta.correcta) {
                opciones[indice].classList.add('incorrecta');
            } else {
                puntuacion += 10;
                respuestasCorrectas++;
                puntajeElemento.textContent = `Puntos: ${puntuacion}`;
            }
            
            // Deshabilitar opciones
            opciones.forEach(opcion => {
                opcion.style.pointerEvents = 'none';
            });
            
            // Mostrar botón siguiente
            btnSiguiente.classList.remove('oculto');
        }

        function tiempoAgotado() {
            const opciones = document.querySelectorAll('.opcion');
            const pregunta = preguntasActuales[preguntaActual];
            
            // Marcar respuesta correcta
            opciones[pregunta.correcta].classList.add('correcta');
            
            // Deshabilitar opciones
            opciones.forEach(opcion => {
                opcion.style.pointerEvents = 'none';
            });
            
            // Mostrar botón siguiente
            btnSiguiente.classList.remove('oculto');
        }

        function siguientePregunta() {
            preguntaActual++;
            
            if (preguntaActual < preguntasActuales.length) {
                mostrarPregunta();
            } else {
                terminarJuego();
            }
        }

        function terminarJuego() {
            // Mostrar puntuación final
            puntajeFinal.textContent = puntuacion;
            
            // Mostrar resumen de correctas
            resumenCorrectas.textContent = `${respuestasCorrectas}/${preguntasActuales.length} preguntas correctas`;
            
            // Cambiar pantalla
            cambiarPantalla(pantallaResultados);
        }

        function cambiarPantalla(pantalla) {
            // Ocultar todas las pantallas
            document.querySelectorAll('.pantalla').forEach(p => {
                p.classList.remove('activa');
            });
            
            // Mostrar pantalla seleccionada
            pantalla.classList.add('activa');
        }

        function volverInicio() {
            cambiarPantalla(pantallaInicio);
        }
    </script>
</body>
</html>
