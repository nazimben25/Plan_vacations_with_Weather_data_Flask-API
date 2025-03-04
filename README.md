# Using Python scripts and FLASK API
# Visualize the weather of over 500 cities of varying distances from the equator and generate a visualization. 
# Use your weather data skills to plan future vacations


## python-api-challenge

This repository is the output of Challenge 6 : Python API

1) Repository organization
in the main folder
- 2 Jupyter files with the final code to run  both parts
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

    2.1.0) # Dependencies and Setup
    
        import matplotlib.pyplot as plt
        import pandas as pd
        import numpy as np
        import requests
        import time
        from scipy.stats import linregress

        # Impor the OpenWeatherMap API key
        from api_keys import weather_api_key

        # Import citipy to determine the cities based on latitude and longitude
        from citipy import citipy

        from pprint import pprint

    2.1.1) generate cities list
        a set of 1500 positions (lat, lon) is randomly regenerated 
        
        FOR LOOP for each position is matched with the cities database to insure it represents or not a city (function citipy.nearest_city)
        if it is the case, a list [cities] is appended 

        this gives a result of more than 500 cities
        ! : the result will change each time we run the code


    2.1.2) retrieve weather data for each city
    a FOR LOOP for each city in the list [cities]
        - to connect to API http://api.openweathermap.org 
        - t generate a JSON FILE  : city_weather
        - if city exist in database OPENWEATHER, data is collected from JSON file city_weather
            * city_lat = city_weather['coord']['lat']
            * city_lng = city_weather['coord']['lon']
            * city_max_temp = city_weather['main']['temp_max']
            * city_humidity = city_weather['main']['humidity']
            * city_clouds = city_weather['clouds']['all']
            * city_wind = city_weather['wind']['speed']
            * city_country = city_weather['sys']['country']
            * city_date = city_weather['dt']

    A list [city_data] is appended wit this data : Index(['City', 'Latitude', 'Lng', 'Temperature', 'Humidity', 'Cloudiness',
       'Wind Speed', 'Country', 'Date'],
      dtype='object')
    
    this step can last more than 10 minutes (Be patient!)

    2.1.3) create a dataframe
    from list city_data 
        - the DF is exported in a CVS file : "output_data/cities.csv"


    2.1.4) Analysis / vizualisation

        2.2.4.1) Create 4 Scatter plots
        with full data
        compare some variables against the LATITUDE

        2.2.4.2) export to file
        4 png files are generated : "output_data/Figx.png"

    2.1.5) separate between north and south Hemisphere

        2.1.5.1) calculate Regression and create scatter plots
        same variables with distinction between N and S
            - create 8 scatter plots 
            - calculate regression for each

        2.1.5.2) create function 
        the step (2.2.5.1) is performed with a function called regression_plot, it
            - calculates Regression parameters (with function linregress)
            - generates scatter plot
            - generates plot for regression
            - the Annotation + Title are conditional regarding the slope or the hemisphere


2.2) code VacationPymywork

    2.2.0 -a)
        # Dependencies and Setup
        import hvplot.pandas
        import pandas as pd
        import requests

        # Import API key
        from api_keys import geoapify_key

        import json  # Import the json module to handle JSON data

        using the csv file generated in the step above (2.2.3)

    2.2.0 - b) Resources
    use the file generated in step (2.1.3)
    stored as "output_data/cities.csv"

    2.2.1) create map
    with the data in the file more than 500 entries 
    generate a map using  hvplot.points

    2.2.2) filter the prefered city and create new DataFrame
    the data is filtred regarding personnal parameters : temperature, humidity, cloudiness

    a new DF is generated : my_city_df

    than a copy is ccreated with additional column : Copy = hotel_df

    2.2.3) for each city, identify the nearest hotel

    using "https://api.geoapify.com/v2/places"
        - loop for each row of hotel_df
        - build a end point to request the API to retrieve
            - coordinates from hotel_df
            - 1st hotels search in a circle of 10,000 meters
        - download a JSON file
        - extract the name of the hotel from the JSON file
        - fill the new column of hotel_df with the hotel name
    
    a call exception TRY -EXCEPT is used


    2.2.4) create a new map ad add information in hover
    with hotel_df
    generate a map using  hvplot.points
    adding columns 'Country' + 'hotel name' to the hover





