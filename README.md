# python-api-challenge

these repository is the output of Challenge 6 : Python API

1) Repository organization
in the main folder
- 2 Jupyter files with the final code to run for both parts
    - WeatherPymywork
    - VacationPymywork

- this README file
- 1 gitignore file

- 2 folders
    - Output_data ; contains outputs for part 1
        - cities cvs file
        - 4 png files with scatter plots 


2) Codes Organization
VacationPymywork is depending on WeatherPymywork outputs
so run (1)  WeatherPymywork than (2) VacationPymywork

2.1) code WeatherPymywork

    2.1.1.) generate cities list
        a set of 1500 positions (lat, lon) is randomly regenerated 
        
        FOR LOOP for each position is matched with the cities database to insure it represents or not a city (function citipy.nearest_city)
        if it is the case, a list [cities] is appended 

        this gives a result of more than 500 cities
        ! : the result will change each time we run the code


    2.1.2) retrieve weather data for each city
    a FOR LOOP for each city in the list [cities]
        - to connect to API http://api.openweathermap.org and JSON FILE generated : city_weather
        - if city exist in database OPENWEATHER, data is collected from JSON file city_weather
            * city_lat = city_weather['coord']['lat']
            * city_lng = city_weather['coord']['lon']
            * city_max_temp = city_weather['main']['temp_max']
            * city_humidity = city_weather['main']['humidity']
            * city_clouds = city_weather['clouds']['all']
            * city_wind = city_weather['wind']['speed']
            * city_country = city_weather['sys']['country']
            * city_date = city_weather['dt']

    A list city_data is appended wit these information : Index(['City', 'Latitude', 'Lng', 'Temperature', 'Humidity', 'Cloudiness',
       'Wind Speed', 'Country', 'Date'],
      dtype='object')

    2.2.3) create a dataframe
    from list city_data 
        - the DF is exported in a CVS file : "output_data/cities.csv"


    2.2.4) Analysis / vizualisation

        2.2.4.1) Create 4 Scatter plots
        with full data
        compare some variables against the LATITUDE

        2.2.4.2) export to file
        4 png files are generated : "output_data/Figx.png"

    2.2.5) separate between north and south Hemisphere
    using the csv file generated in the step above

        2.2.5.1) calculate Regression and create scatter plots
        same variables with distinction between N and S
            - create 8 scatter plots 
            - calculate regression for each

        2.2.4.3) create function 
        the step (2.2.5.1) is performed with a function called regression_plot, it
            - calculates Regression parameters (with function linregress)
            - generates scatter plot
            - generates plot for regression
            - the Annotation + Title are conditional regarding the slope or the hemisphere


2.1) code VacationPymywork
using the csv file generated in the step above (2.2.3)




