# Script de Escenario Procedural y Animación de Cámara en Blender 

Este repositorio contiene un script de Python diseñado para la API de Blender (`bpy`) que automatiza la creación de un entorno 3D complejo, incluyendo geometría paramétrica, materiales dinámicos y un sistema de cámara animada.



##  Índice
1. [Descripción General](#-descripción-general)
2. [Análisis del Código](#-análisis-del-código)
3. [Requisitos](#-requisitos)
4. [Instrucciones de Uso](#-instrucciones-de-uso)
5. [Detalles Técnicos](#-detalles-técnicos)



##  Descripción General
El script genera un pasillo que combina secciones rectilíneas y curvas. No solo coloca los objetos, sino que también gestiona la limpieza de la escena, la creación de materiales con nodos y la configuración de una trayectoria de cámara fluida mediante restricciones físicas.



##  Análisis del Código

### 1. Gestión de Materiales (`crear_material`)
La función utiliza el motor de renderizado **Cycles/Eevee** para crear materiales mediante nodos:
* **Principled BSDF:** Se configura el `Base Color` y se ajusta la rugosidad (`Roughness`) a 0.7 para evitar reflejos excesivos, dándole un aspecto sólido al escenario.



### 2. Construcción Procedural
El pasillo se construye en dos fases:
* **Tramo Recto:** Genera muros laterales. Utiliza un operador de módulo (`i % 2`) para alternar entre materiales oscuros y naranjas, variando también la escala en el eje Z para crear ritmo visual.
* **Tramo Curvo:** Implementa funciones trigonométricas (`math.cos` y `math.sin`) para posicionar cubos en un arco de 90 grados, calculando la rotación exacta en el eje Z para que las paredes sigan la curvatura.



### 3. Sistema de Iluminación
El script configura un esquema de iluminación de tres puntos:
* **Sun Light:** Proporciona luz direccional global.
* **Point Lights:** Luces locales situadas estratégicamente en el pasillo y la curva para generar profundidad y sombras.

  

### 4. Trayectoria y Animación (Follow Path)
Se crea una curva tipo **Spline** que sirve como guía:
* **Empty (Cam_Target):** Se crea un objeto vacío que actúa como el "objetivo" de la cámara.
* **Constraints:** Se aplican restricciones `FOLLOW_PATH` y `TRACK_TO` para asegurar que la cámara no solo se mueva por el camino, sino que siempre apunte hacia su objetivo, creando una sensación de "cinemática".

  

##  Detalles Técnicos
El script utiliza los siguientes conceptos avanzados de graficación:
* **Coordenadas Homogéneas:** Para posicionar y rotar objetos en el espacio 3D.
* **Interpolación de Movimiento:** Configura fotogramas clave (Keyframes) en el frame 1 y 200 para el `offset_factor`.
* **Cálculo de Radianes:** Conversión de grados a radianes para las funciones de la librería `math`.

  

##  Instrucciones de Uso

1. Abre **Blender** (versión 2.8x o superior).
2. Dirígete al espacio de trabajo **Scripting** en la parte superior.
3. Haz clic en el botón **+ New** y pega el código del script.
4. Presiona el botón **Run Script**.
5. En el Viewport 3D, presiona `Numpad 0` para entrar en la vista de cámara y pulsa `Space` para reproducir la animación.


##  Requisitos
* **Blender** 2.80 o superior.
* Conocimientos básicos de la interfaz de Blender para visualizar el render.

