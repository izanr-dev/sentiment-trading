Sentiment Trader: Análisis de Mercado mediante NLP y Economía Conductual

https://izanr-dev.github.io/sentiment-trading/

(Nota: Esta aplicación se ejecuta completamente en tu navegador. No requiere instalación.)

1. Resumen Ejecutivo

Este proyecto explora la intersección entre la Economía Conductual y la Inteligencia Artificial. El objetivo es demostrar empíricamente cómo la asimetría de la información y el sentimiento del mercado (miedo/euforia) influyen en la formación de precios a corto plazo, desafiando parcialmente la Hipótesis del Mercado Eficiente (EMH).

Se ha desarrollado una herramienta de Procesamiento de Lenguaje Natural (NLP) que utiliza léxicos financieros especializados para cuantificar el "estado de ánimo" de las noticias y generar señales de trading. Además, implementa un sistema de aprendizaje adaptativo que calibra sus umbrales de riesgo basándose en la retroalimentación del usuario sobre el movimiento real del mercado.

2. Fundamentación Económica

2.1. ¿Sienten los Mercados? Crítica a la Eficiencia

En teoría, la bolsa debería ser un mecanismo racional que descuenta toda la información instantáneamente. En la práctica, los mercados exhiben comportamientos irracionales documentados por la economía conductual:

Asimetría del Miedo (Loss Aversion): Los inversores reaccionan con mayor rapidez y volatilidad a las noticias negativas que a las positivas. El dolor psicológico de la pérdida es asimétrico respecto al placer de la ganancia.

Comportamiento de Manada (Herding): En momentos de alta incertidumbre (VIX alto), los inversores tienden a ignorar sus propios análisis fundamentales y siguen la tendencia predominante, exacerbando las caídas (pánico) o las burbujas (euforia).

2.2. Casos de Estudio Históricos

El algoritmo se ha diseñado observando fenómenos de mercado recientes:

El COVID-19 (El sesgo de normalidad): Inicialmente, el mercado ignoró el riesgo. Cuando el pánico se desató en febrero de 2020, la venta fue indiscriminada. Un algoritmo eficaz debe diferenciar sectores (ej. vender aerolíneas, comprar tecnológicas "stay-at-home").

La Guerra de Ucrania (La paradoja de la incertidumbre): El mercado cayó antes de la invasión debido a la incertidumbre ("Sell the rumor"). El día de la invasión, el mercado subió ("Buy the news"). Esto demuestra que el mercado penaliza más la incertidumbre que las malas noticias confirmadas.

3. Implementación Técnica

Para solucionar la incapacidad de los modelos de lenguaje genéricos para entender el contexto financiero, se ha implementado la siguiente arquitectura:

3.1. El Problema Semántico y el Léxico Loughran-McDonald

Un diccionario estándar considera palabras como "liability" (pasivo), "risk" (riesgo) o "crude" (petróleo crudo) como negativas. En finanzas, son términos operativos neutros.

Solución: Implementación del Léxico Loughran-McDonald, diseñado específicamente para analizar reportes financieros (10-Ks).

Resultado: El algoritmo distingue entre "coste operativo" (neutro) y "litigio imprevisto" (negativo fuerte).

3.2. Algoritmo de Calibración Dinámica (Regime Switching)

El sistema no utiliza reglas estáticas (if score > 0.5 then buy). En su lugar, utiliza un bucle de retroalimentación simple para adaptarse al régimen de volatilidad:

Predicción: El sistema evalúa titulares y emite una recomendación (Comprar/Vender/Mantener).

Feedback: El usuario introduce el resultado real del mercado (Subió/Bajó).

Ajuste (Learning Rate):

Si el sistema fue demasiado optimista (Recomendó comprar y el mercado bajó), eleva sus estándares de seguridad (sube el umbral de compra).

Si el sistema fue demasiado pesimista (Recomendó vender y el mercado subió), reduce su aversión al riesgo.

Esto simula a un trader humano que se vuelve más cauto tras una pérdida y más confiado tras un acierto.

4. Guía de Uso de la Herramienta

La interfaz ha sido diseñada para emular una terminal financiera profesional (tipo Bloomberg), priorizando la funcionalidad y la velocidad de lectura de datos.

Input Stream: Introduzca titulares de noticias financieras en inglés (el idioma franco de los mercados globales).

Ejemplo: "Fed raises rates aggressively to fight inflation."

Ejecutar Análisis: El motor NLP procesará las palabras clave y calculará un Sentiment Score entre -1 (Pánico extremo) y +1 (Euforia máxima).

Visualización: Una barra de progreso mostrará la posición del sentimiento respecto a los umbrales de compra/venta actuales.

Entrenamiento (Feedback Loop): Utilice los botones inferiores (BAJÓ, LATERAL, SUBIÓ) para informar a la IA de qué hizo realmente el mercado. Observe cómo los parámetros Umbral Compra y Umbral Venta se ajustan en tiempo real en el panel derecho.

5. Stack Tecnológico

HTML5 / CSS3 (Tailwind): Interfaz reactiva y ligera sin frameworks pesados.

JavaScript (ES6+): Lógica de procesamiento de lenguaje natural en el cliente.

LocalStorage: Persistencia de datos para "recordar" el entrenamiento del usuario entre sesiones.

Autor y Licencia

Este proyecto ha sido desarrollado con fines académicos y de investigación. El código es abierto para su revisión y mejora.
