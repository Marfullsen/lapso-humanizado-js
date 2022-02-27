# Lapso Humanizado JS

<img src="https://img.shields.io/badge/Vanilla-JavaScript-yellow.svg" alt="Vanilla JS">

Fork del repo [QuantumCatgirl/js_humanizar_lapso](https://github.com/QuantumCatgirl/js_humanizar_lapso) traducido al español.

"humanizar_lapso(fecha)" returns the difference between two Dates as a nice, human string for use in the browser.

<img src=".\docs\img\testing_humanizar_lapso_dev_tools.png" alt="Testing_with_dev_tools">

## usage

Include the script (it's native JS so doesn't require anything else) and you're ready to go.

### Syntax
    humanizar_lapso(date, ref_date, date_formats, time_units)
  
Only date is required.

### Examples

    humanizar_lapso("2010/09/10 10:00:00") => "3 days ago" (using now as a reference)
  
    humanizar_lapso("2010/09/10 10:00:00", "2010/09/10 12:00:00") => "2 hours ago"

### Customisation

Custom date formats can be set as follows:

    var custom_date_formats = {
      past: [
        { ceiling: 60, text: "less than a minute ago" },
        { ceiling: 86400, text: "$hours hours, $minutes minutes and $seconds seconds ago" },
        { ceiling: null, text: "$years years ago" }
      ],
      future: [
        { ceiling: 60, text: "in less than a minute" },
        { ceiling: 86400, text: "in $hours hours, $minutes minutes and $seconds seconds time" },
        { ceiling: null, text: "in $years years" }
      ]
    }
    
    humanizar_lapso("2010/09/10 10:00:00", "2010/09/10 10:00:05", custom_date_formats) 
      => "less than a minute ago"
    humanizar_lapso("2010/09/10 10:00:00", "2010/09/10 17:01:25", custom_date_formats) 
      => "5 hours, 1 minute and 25 seconds ago"
    humanizar_lapso("2010/09/10 10:00:00", "2012/09/10 10:00:00", custom_date_formats) 
      => "in 2 years"

Here the date format's ceiling is in seconds. Formats are walked through until one is reached where the ceiling is more than the difference between the two times or is null.

Please note that the last date format provided must not have a ceiling.

Variables in the format text should be prefixed with a $. eg. $xxx where xxx is the name of the time unit. The text should always be written in the plural (eg. "$years years ago") and the text will be automatically de-pluralized if, say in this case, there is only 1 year.


For those who live by different time rules, time_units can also be customised:
  
    var custom_date_formats = [
      { ceiling: null, text: "$moggles moggles, $tocks tocks and $ticks ticks ago" },
    ]
  
    var custom_time_units = [
      [20, 'moggles'],
      [10, 'tocks'],
      [1, 'ticks']
    ]
    time_ago("2010/01/01 00:00:00", "2010/01/01 00:00:53", custom_date_formats, custom_time_units) 
      => "2 moggles, 1 tock and 3 ticks ago"
    
Custom date formats will have to be used when using custom time_units.

the default time units are:

    [31556926, 'years'],
    [2629744, 'months'],
    [86400, 'days'],
    [3600, 'hours'],
    [60, 'minutes'],
    [1, 'seconds']
    
