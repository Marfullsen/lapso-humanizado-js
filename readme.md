# Lapso Humanizado JS

<img src="https://img.shields.io/badge/Vanilla-JavaScript-yellow.svg" alt="Vanilla JS">

La función **humanizar_lapso(fecha)** devuelve la diferencia entre dos fechas de una manera más agradable para ser usada en el navegador.

<p align="center">
  <a href="./lapso_humanizado.js" rel="noopener">
 <img src=".\docs\img\testing_humanizar_lapso_dev_tools.png" alt="Testing_with_dev_tools">
</p>

## ¿Cómo se utiliza la función?

Incluye el script **lapso_humanizado.js** en tu proyecto y la función estará lista para ser usada.

### Sintaxis
    humanizar_lapso(date, ref_date, date_formats, time_units)
  
**Sólo se requiere el parámetro _date_**

### Ejemplos

    humanizar_lapso("2010/09/10 10:00:00") => "Hace 3 días" (usando el momento actual como referencia.)
  
    humanizar_lapso("2010/09/10 10:00:00", "2010/09/10 12:00:00") => "hace 2 horas"

### Personalizar

Los formatos personalizados de fecha pueden ser ajustados de la siguiente manera:

    var formato_personalizado_de_fecha = {
      past: [
        { ceiling: 60, text: "Hace menos de un minuto" },
        { ceiling: 86400, text: "hace $hours horas, $minutes minutos y $seconds segundos" },
        { ceiling: null, text: "hace $years años" }
      ],
      future: [
        { ceiling: 60, text: "en menos de un minuto" },
        { ceiling: 86400, text: "en $hours horas, $minutes minutos y $seconds segundos" },
        { ceiling: null, text: "en $years años" }
      ]
    }
    
    humanizar_lapso("2010/09/10 10:00:00", "2010/09/10 10:00:05", formato_personalizado_de_fecha) 
      => "Hace menos de un minuto"
    humanizar_lapso("2010/09/10 10:00:00", "2010/09/10 17:01:25", formato_personalizado_de_fecha) 
      => "hace 5 horas, 1 minuto y 25 segundos"
    humanizar_lapso("2010/09/10 10:00:00", "2012/09/10 10:00:00", formato_personalizado_de_fecha) 
      => "en 2 años"

#### Formato personalizado de Marfullsen

``` 
date_formats = date_formats || {
  past: [
    { ceiling: 60, text: "hace menos de un minuto" },
    { ceiling: 120, text: "hace un minuto" },
    { ceiling: 3600, text: "hace $minutes minutos" },
    { ceiling: 7200, text: "hace una hora" },
    { ceiling: 86400, text: "hace $hours horas" },
    { ceiling: 172800, text: "hace un día" },
    { ceiling: 2629744, text: "hace $days días" },
    { ceiling: 5259488, text: "hace un mes" },
    { ceiling: 31556926, text: "hace $months meses" },
    { ceiling: null, text: "hace $years años" },
  ],
  future: [
    { ceiling: 60, text: "en $seconds segundos" },
    { ceiling: 3600, text: "en $minutes minutos" },
    { ceiling: 86400, text: "en $hours horas" },
    { ceiling: 2629744, text: "en $days días" },
    { ceiling: 31556926, text: "en $months meses" },
    { ceiling: null, text: "en $years años" },
  ],
};
```

Here the date format's ceiling is in seconds. Formats are walked through until one is reached where the ceiling is more than the difference between the two times or is null.

Please note that the last date format provided must not have a ceiling.

Variables in the format text should be prefixed with a $. eg. $xxx where xxx is the name of the time unit. The text should always be written in the plural (eg. "$years years ago") and the text will be automatically de-pluralized if, say in this case, there is only 1 year.


For those who live by different time rules, time_units can also be customised:
  
    var formato_personalizado_de_fecha = [
      { ceiling: null, text: "$moggles moggles, $tocks tocks and $ticks ticks ago" },
    ]
  
    var custom_time_units = [
      [20, 'moggles'],
      [10, 'tocks'],
      [1, 'ticks']
    ]
    time_ago("2010/01/01 00:00:00", "2010/01/01 00:00:53", formato_personalizado_de_fecha, custom_time_units) 
      => "2 moggles, 1 tock and 3 ticks ago"
    
Custom date formats will have to be used when using custom time_units.

the default time units are:

    [31556926, 'years'],
    [2629744, 'months'],
    [86400, 'days'],
    [3600, 'hours'],
    [60, 'minutes'],
    [1, 'seconds']
    
## Créditos

Versión original (inglés) [QuantumCatgirl/js_humanizar_lapso](https://github.com/QuantumCatgirl/js_humanized_time_span).

[How to format time since xxx e.g. “4 minutes ago” similar to Stack Exchange sites](https://stackoverflow.com/a/5965935/15466047)