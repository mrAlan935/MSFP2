[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=mrAlan935/MSFP2)

# Práctica 2: Diseño de controlador para un sistema cardiovascular

## Información del estudiante

Obregon Maldonado Alan Yahir [23212221]; l23212221@tectijuana.edu.mx

Modelado de Sistemas Fisiológicos

Ingeniería Biomédica

## Docente

Dr. Paul Antonio Valle Trujillo; paul.valle@tectijuana.edu.mx

Departamento de Ingeniería Eléctrica y Electrónica, Tecnológico Nacional de México/IT Tijuana, Blvd. Alberto Limón Padilla s/n, Tijuana, C.P. 22454, B.C., México.

## Descripción de la asignatura

El modelizado de sistemas fisiológicos es una herramienta importante en Ingeniería Biomédica, permite comprender el funcionamiento del cuerpo humano, así como diseñar y evaluar terapias y dispositivos médicos; se define como el proceso de formular modelos matemáticos o computacionales que representan el comportamiento y la interacción de los sistemas biológicos y fisiológicos. Esta asignatura pretende aportar al perfil del Ingeniero Biomédico la capacidad de realizar investigación científica en el área de Biología de Sistemas con la finalidad de dirigir y participar en equipos de trabajo interdisciplinarios en contextos nacionales e internacionales, así como de proporcionar soluciones informáticas para resolver problemas en el campo de la Ingeniería Biomédica con ética profesional; lo anterior al proporcionar al estudiante bases sólidas para modelizar sistemas y diseñar controladores para la solución de problemas en las áreas de atención médica y del sector industrial médico. La construcción de analogías entre circuitos eléctricos y sistemas fisiológicos para la formulación de modelos matemáticos y el diseño de controladores mediante la experimentación in silico brindan herramientas de gran aplicación en el quehacer profesional del Ingeniero Biomédico.

La asignatura de Modelado de Sistemas Fisiológicos forma parte del plan de estudios de la carrera en Ingeniería Biomédica con la siguiente competencia general del curso: Utiliza las propiedades de los circuitos RLC para describir la dinámica de sistemas fisiológicos, obtener modelos matemáticos y aplicar el control clásico, esto con el objetivo de integrar los principios de la Ingeniería de Control, la Electrónica Analógica y las Ciencias de la Computación con la Anatomía y Fisiología del cuerpo humano para proporcionar descripciones cuantitativas y cualitativas de sistemas fisiológicos complejos con el objetivo de modelizar, analizar, controlar, ilustrar y predecir su dinámica tanto en el corto como en el largo plazo.

## Objetivos

1. Calcular la función de transferencia.
2. Determinar el modelo de ecuaciones integro-diferenciales.
3. Establecer el sistema de ecuaciones diferenciales ordinarias lineales de primer orden.
4. Simular la respuesta del sistema cardiovascular en Simulink/MATLAB para los casos normotenso, hipotenso e hipertenso en lazo abierto.
5. Sintonizar las ganancias de un controlador PID en Simulink/MATLAB para que la respuesta de los casos hipotenso e hipertenso (lazo cerrado) siga a la del caso normotenso.
6. Implementar el modelo en MATLAB mediante integración numérica (método de Euler) y comparar los resultados con la simulación en Simulink.
7. Obtener la respuesta en lazo abierto y en lazo cerrado con el controlador PID en Visual Code/Python con la función de transferencia.

## Descripción detallada del sistema

En esta práctica se modela el sistema cardiovascular mediante un circuito eléctrico de cuatro elementos (Z, L, R y C) en el que la impedancia Z y la inertancia L se conectan en paralelo, seguidas de la capacitancia C en paralelo con la resistencia R. La señal de entrada Pa(t) representa la presión a la salida del ventrículo izquierdo y la señal de salida Pp(t) es la presión resultante en el modelo. Cada elemento se asocia con una estructura anatómica: Z con la base de la aorta (0.010), L con la aorta ascendente (0.001), R con los vasos sanguíneos (1.000) y C con la pared de la aorta.

Se estudian tres casos que se distinguen únicamente por el valor de la capacitancia C: hipertenso (C = 1.000), normotenso (C = 1.500) e hipotenso (C = 3.500). Se simulan 15 s con el solucionador ode15s y un paso máximo de 1e-3 s, usando una señal de entrada Pa(t) muestreada cada 0.01 s e interpolada a 0.001 s. Primero se obtiene la respuesta de los tres casos en lazo abierto y después se diseña un controlador PID, en lazo cerrado, para los casos hipotenso e hipertenso, con el objetivo de que la salida siga a la del caso normotenso.

La función de transferencia del sistema, de segundo orden, es:

G(s) = Pp(s)/Pa(s) = (L·R·s + R·Z) / (C·L·R·Z·s² + (L·R + L·Z)·s + R·Z)

En Python se calcula con la librería `control` para cada caso, junto con sus polos, y se obtiene la respuesta forzada a la señal Pa(t) guardada en `signal.xlsx`. El controlador PID se implementa con su equivalente en amplificadores operacionales (capacitor Cr = 1 µF) y se conecta en lazo cerrado con retroalimentación unitaria negativa. Las ganancias sintonizadas son:

| Caso | kP | kI | kD |
|---|---|---|---|
| Hipotenso | 480.0783 | 1 219 332.2605 | 0.00627 |
| Hipertenso | 311.4801 | 1 796 432.5035 | 0.00178 |

Para ejecutar el código de Python se requieren las librerías `control`, `numpy`, `scipy`, `matplotlib` y `pandas`.

Palabras clave: Circuito RLC; Controlador PID; Sistema cardiovascular; Modelo matemático; Simulaciones numéricas.

## Lista de archivos incluidos en el repositorio

1. Cuaderno computacional de MATLAB [.mlx y .pdf].
2. Modelo de Simulink [.slx].
3. Archivo de Python [.py].
4. Imagen con los parámetros del controlador.
5. Figuras de las simulaciones en MATLAB (4) [.pdf]: lazo abierto, hipotenso, hipertenso e individuos.
6. Figuras de las simulaciones en Python (3) [.pdf]: individuos, hipotenso e hipertenso.
7. Diagrama del sistema cardiovascular elaborado en BioRender [.png].
8. Imagen del modelo de Simulink [.png].
9. Señal de entrada Pa(t) [.xlsx].

## Referencias

\[1] P. A. Valle, Syllabus para Modelado de Sistemas Fisiológicos, Tecnológico Nacional de México / Instituto Tecnológico de Tijuana, Tijuana, B.C., México, 2025. Permalink: https://biomath.xyz/course/

\[2] M. C. Khoo, Physiological Control Systems Analysis Simulation, and Estimation, 2nd ed. Piscataway, New Jersey, USA: IEEE Press, 2018, Section 4, Page 93.

\[3] N. S. Nise, Control Systems Engineering, 8th ed. Hoboken, New Jersey, USA: John Wiley & Sons, 2020.
