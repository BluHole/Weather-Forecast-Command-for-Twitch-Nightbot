# Español/English

## Español

Este código implementa 3 comandos separados (pero relacionados) en JavaScript para ver el pronóstico del tiempo en una localización dada en Nightbot, un bot popular utilizado en canales de Twitch para automatizar tareas y responder a comandos introducidos por el chat.
El nombre de los comandos se puede cambiar sin problemas, aunque recomiendo dejarlos como están. Para más información leer *Implementación en Nightbot* más abajo.

### - IMPORTANTE -

Uno de los comandos utiliza la API de pago One Call API 3.0 de OpenWeatherMap.org, con lo que necesitarás una cuenta de pago creada en dicha plataforma para poder utilizar el comando (aunque es gratis para menos de 1000 consultas a la API al día, así que no hará falta gastar dinero en la mayoría de situaciones).

## Descripción de los comandos:

  - !tiempo: Este comando recibe el nombre de una localización (por ejemplo, Alicante) y muestra, mediante una consulta a la API de [wttr.in](https://github.com/chubin/wttr.in), el pronóstico **ACTUAL** para dicha localización.

    ![comando_tiempo_resultado](https://i.imgur.com/1G5FttP.png)

  - !pronostico: Este comando, como el anterior, recibe el nombre de una localización y muestra, mediante una consulta a la API de [wttr.in](https://github.com/chubin/wttr.in), el pronóstico de la temperatura para dicha localización a 2 días vista. Como se puede apreciar, este comando está "incompleto" pues únicamente muestra la temperatura, no el pronóstico del tiempo completo, ya que wttr.in tiene sus limitaciones para mostrar esta información de manera sencilla de recuperar y además estamos limitados a comandos de no más de 500 caracteres en Nightbot. Para solventar esto, le indicamos al usuario que si quiere más información utilice el siguiente comando (*!pronostico2*) seguido de las coordenadas de la localización introducida, recuperadas de la información que nos devuelve la API de wttr.in .
    
    ![comando_pronostico_resultado](https://i.imgur.com/CS7esXR.png)

  - !pronostico2: Este comando, más avanzado, realiza una consulta a la API de pago One Call API 3.0 de OpenWeatherMap.org, la cual necesita de la localización geográfica exacta (latitud y longitud) del lugar del que queramos recuperar la información del tiempo. Para facilitar el uso de este comando a los usuarios, dicha información de latitud y longitud la recuperamos de la consulta a la API de wttr.in en el anterior comando, ya que con Nightbot estamos limitados a un máximo de 1 llamada a otro comando y no podemos realizar primero una llamada a un comando que nos devuelva la latitud y longitud de una localización y después que invoque a este comando con dicha información.
    
    ![comando_pronostico2_resultado](https://i.imgur.com/DckxnVE.png) 

## Implementación en Nightbot:

La implementación en Nightbot es sencilla, únicamente tenemos que crear 5 comandos (los 3 mencionados + 2 extra que filtrarán y mostrarán la salida de los comandos *!pronostico* y *!pronostico2* por el chat de Twitch) y copiar&pegar el código en ellos (recuerda introducir tu API key de OpenWeatherMap.org para que el comando *!pronostico2* funcione). Es necesario también que todos los comandos que creemos en Nightbot puedan ser ejecutados por todos los usuarios (seleccionar *Everyone* en el *UserLevel*).
Se puede consultar la información proporcionada por las APIs para cambiar la salida de los comandos modificando el código de forma acorde, aunque creo que como están, muestran la información más relevante del tiempo.

![implementacion_comando](https://i.imgur.com/sr8LPeR.png)

![implementacion_comando2](https://i.imgur.com/bFMWB0O.png)

- Creación de los comandos:

Nos vamos a *Commands --> Custom* en el panel lateral izquierdo de la web de Nightbot, y hacemos click en el botón grande azul *+Add Command*, ubicado a la derecha, para crear cada comando. Debemos dejar seleccionado para todos ellos el *Userlevel --> Everyone*:

  1. !tiempo: Este primer comando es sencillo y autónomo, no requiere de hacer una llamada a otro comando.
     - En el campo de *Command* introducimos el nombre del comando, en este caso *!tiempo*.
     - En el campo de *Message* copiamos y pegamos el código proporcionado.
  
  2. !pronostico: Este comando y el siguiente requieren de hacer una llamada a otro comando que crearemos en Nightbot, por ello tememos que realizar un par de pasos extra:
     - En el campo de *Command* introducimos el nombre del comando, en este caso *!pronostico*, en la casilla de *Message* copiamos y pegamos el código del comando.
     - Ahora en la casilla de *Alias* tenemos que introducir el nombre del comando al que se le pasará la información recibida de la API consultada en JSON. En mi caso lo he dejado sencillo y simplemente lo he llamado *salida_pronostico*, pero se puede poner cualquier otro nombre.
     - Creamos un nuevo comando, cuyo nombre será el introducido en el campo de *Alias*, así que en el campo de *Command* introducimos *salida_pronostico* (o el que se haya elegido en el anterior paso).
     - Finalmente, en el campo *Message* copiamos y pegamos el código proporcionado.
  
  3. !pronostico2: Como en el anterior comando, tendremos que crear 2 comandos para que funcione, además, en este tendremos también que conseguir e introducir la clave de la API de One Call API 3.0 de OpenWeatherMap.org, para la cual tendremos que crear una cuenta de pago en dicha plataforma.
     - En el campo de *Command* introducimos el nombre del comando, en este caso *!pronostico2*, en la casilla de *Message* copiamos y pegamos el código del comando, **AÑADIENDO NUESTRA CLAVE API PERSONAL DE LA CUENTA DE PAGO DE OpenWeatherMap.org**.
     - Ahora en la casilla de *Alias*, como antes, introducimos el nombre del comando que filtrará el JSON, en mi caso *salida_pronostico2*.
     - Creamos un nuevo comando, cuyo nombre será el introducido en el campo de *Alias*, así que en el campo de *Command* introducimos *salida_pronostico2*.
     - Finalmente, en el campo *Message* copiamos y pegamos el código proporcionado.

----------------

## English

This code implements 3 separate (yet related) JavaScript commands for weather forecasting in a given location in Nightbot, a popular bot in Twitch channels for automation of tasks and responding to commands introduced in the chat.
The name of the commands can be changed without problems, but I reccomend not to. For more information read *Implementation in Nightbot* below.

They are all in spanish and using international units, so feel free to customize & translate them for your needs.

### - IMPORTANT -

One of the commands uses the paid API One Call API 3.0 from OpenWeatherMap.org, so you will need a paid account in the platform to be able to use the command (but it is free for less than 1000 API calls per day, so in the majority of cases you will not spend money).

## Commands description:

  - !tiempo: This command receives the name of a given location (for instance, Alicante, in the South-East of Spain) and shows, making a call to the API of [wttr.in](https://github.com/chubin/wttr.in), the **CURRENT** weather for the location.

    ![tiempo_command_result](https://i.imgur.com/1G5FttP.png)

    Translation: *"Current conditions for Alicante are: Partly cloudy, temperature +17ºC, wind chill +17ºC and 88% humidity. Wind <--13km/h, atmospheric pressure 1018hPA and precipitation of 0.0mm/3h."*

  - !pronostico: This command, like the latter, receives the name of a given location and shows, making a call to the API of [wttr.in](https://github.com/chubin/wttr.in), the temperature forecast for the location 2 days ahead. As it can be appreciated, this command is "incomplete" since it only displays the temperature, not the complete weather forecast. This is due to wttr.in's limitations in presenting this information in an easily accessible manner and also we are limited at 500 characters commands in Nightbot. To solve this, we indicate to the user that if it needs more information it can use the next command (*!pronostico2*) followed by the coordinates of the given location, retrieved from the information that the API of wttr.in gives us.
    
    ![pronostico_command_result](https://i.imgur.com/CS7esXR.png)

    Translation: *"- Tomorrow: max. temperature of 22ºC and min. temperature of 16ºC.| Past tomorrow: max. temperature of 22ºC, min. temperature of 19ºC./// More information--> !pronostico2 38.35 -0.49".*

  - !pronostico2: This more advanced command makes an API call to the paid API One Call API 3.0 from OpenWeatherMap.org, which requires the precise geographical location (latitude and longitude) of the location we want to retrieve the weather forecast from. To facilitate the use of this command for the users, we retrieve the latitude and longitude information from the query to the wttr.in API in the last command, and because we are limited to a maximum of 1 call to other command in Nighbot, we cannot make a first call to a command that retrieves the latitude and longitud of a given location and then invoques this command with that information.

    ![comando_pronostico2_resultado](https://i.imgur.com/DckxnVE.png) 
