# Entregable 1 de la asignatura Inteligencia Artificial

## Contexto

En este entregable vamos a replicar el funcionamiento de las competiciones de la plataforma [Kaggle](https://www.kaggle.com/). Kaggle es una plataforma que aloja competiciones de aprendizaje automático. El procedimiento seguido en estas competiciones es el siguiente:
1. El organizador de la competición prepara un dataset y una descripción del problema. Algunas de estas competiciones tienen premios en metálico, otras tienen reconocimiento académico, y otras competiciones se utilizan para simplemente aprender.
2. Los participantes de la competición experimentan con distintas técnicas y compiten entre ellos para crear los mejores modelos.
3. Los participantes envían sus modelos que son evaluados con datos que los modelos no habían visto hasta el momento.
4. Después de que se cumple el plazo de entrega, el ganador es anunciado.

Las competiciones Kaggle han dado lugar a proyectos muy exitosos que han
mejorado las técnicas de [detección de VIH](http://science.sciencemag.org/content/331/6018/698.summary),
[estimación de jugadores de ajedrez](http://en.chessbase.com/post/the-deloitte-fide-che-rating-challenge),
[tiempos de viaje](http://www.theaustralian.com.au/business/technology/smartphone-used-to-predict-nsw-travel-times/news-story/e359c45a168bb59ebd2d9d8dfc66cd89),
o en la [identificación de ballenas](https://www.kaggle.com/c/noaa-right-whale-recognition).

Las competiciones Kaggle no sólo se utilizan para crear clasificadores que resuelvan problemas concretos, sino que los competidores también suelen explicar las técnicas que han utilizado para llegar hasta dichos clasificadores utilizando lo que se conoce como [Kaggle kernels](https://www.kaggle.com/kernels). En este entregable pasará lo mismo, no sólo se evaluará el resultado final, sino también el proceso seguido.

## Tareas a realizar

En la página de [kaggle del curso](https://www.kaggle.com/competitions/ia-2425) se ha organizado una competición para crear un modelo capaz de predecir qué actividad estaba realizando una persona. Para participar en la competición debes:

- Registrarte en la página de kaggle.
- Descargar los datasets de entrenamiento y test disponibles en la pestaña **Data** de la competición.
- Construir un modelo y realizar un envío. Un ejemplo para construir un modelo y almacenar los resultados en el formato adecuado puede verse en el notebook envio.ipynb incluido en este repositorio. El envío lo deberás realizar desde la pestaña **Leaderboard**.

Como hemos comentado anteriormente, en este entregable no solo se evaluará el resultado final sino el proceso seguido. En concreto para superar este entregable debes crear y almacenar en tu repositorio al menos los siguientes notebooks:

- Un notebook similar al notebook de la práctica 3 parte 1 donde se realice un análisis de los datos del dataset. Debes al menos incluir 5 preguntas, y sus respectivas respuestas, similares a las planteadas en los ejercicios de dicha práctica. 
- Un notebook similar al notebook de la práctica 4 parte 1 donde se visualicen los datos del dataset.
- Un notebook donde se realice una comparativa de distintos algoritmos de clasificación para el dataset proporcionado.
- A partir del notebook anterior se deberá seleccionar un algoritmo de clasificación que será el utilizado para crear un notebook similar al de envio.ipynb incluido en este repositorio donde proporciones el mejor modelo que hayas podido construir. 

Los notebooks no deben incluir sólo código sino también explicaciones de lo que se hace en cada paso. 

Además de los notebooks mínimos, puedes crear tantos notebooks como consideres necesarios donde apliques las distintas técnicas vistas en esta parte del curso. Ejemplos:

- Notebook con técnicas de reducción de dimensionalidad para visualizar datos.
- Aplicación de técnicas de selección de descriptores para elegir las características adecuadas.
- Análisis estadístico para comparar los distintos modelos. 
- Cualquier ampliación que se te pueda ocurrir. 

