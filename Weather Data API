#DSC 510
#Course Project
#Programming Assignment Week 12
#Author: Katie Adams
#2/28/2021

import requests #Use the Requests library in order to request data from the webservice

def weatherdata(location, cityzip): #weatherdata function that passes location and cityzip to obtain weather forecast data from OpenWeatherMap
    APIKey = "0369cfd3fbe11ff6883c54140119eb84" #defined the variable APIKey as my API key that was provided by OpenWeatherMap website
    if cityzip == "1": #if statement that if the answer from main function is 1, then...
        URL = "https://api.openweathermap.org/data/2.5/weather?q={}&appid={}".format(location, APIKey) #use this URL and input the location which is the city name and the API key above
    elif cityzip == "2": #else if statement that if the answer from main function is 2, then...
        URL = "https://api.openweathermap.org/data/2.5/weather?zip={},us&appid={}".format(location, APIKey) #use this URL and input the location which is the zip code and the API key above
    try: #try block to establish a connection to the webservice
        response=requests.get(URL) #defined response as the Requests Library import using a GET request of the above URL
        print("The connection was successful.\n") #prints a message to the user indicating the connection was successful
        return response #return the response from the webservice
    except requests.exceptions.RequestException as err: #except block to show the error connection to the webservice
        print("The connection was not successful, error: {} ".format(err)) #prints a message to the user indicating the connection was not successful and displays the error

def prettyprint(weather): #pretty print function that passes weather and displays the weather forecast in a readable format to the user
    location = weather.json()["name"] #define location variable as the name field from the JSON dictionary
    hightemp = weather.json()["main"]["temp_max"] #defined hightemp variable as the temp_max field from the JSON dictionary under the main section
    hightemp, unit = tempunit(hightemp) #function tempunit returns a tuple that is unpacked into the variables hightemp and unit
    lowtemp = weather.json()["main"]["temp_min"] #defined lowtemp variable  as the temp_min field from the JSON dictionary under the main section
    lowtemp, unit = tempunit(lowtemp, unit)#function tempunit returns a tuple that is unpacked into the variables lowtemp and unit
    pressure = weather.json()["main"]["pressure"] #defined pressure variable as the pressure field from the JSON dictionary under the main section
    humidity = weather.json()["main"]["humidity"] #defined humidity variable as the humidity field from the JSON dictionary under the main section
    cloudcover = weather.json()["weather"][0]["description"]#defined cloudcover variable as the description field from the JSON dictionary under the weather section
    print()#print a blank line
    print("Current Weather Conditions For {}".format(location)) #print the current weather conditions for the user's desired location
    print("High Temp: {} {}".format(hightemp, unit.upper())) #print the high temperature data with units in capital letters
    print("Low Temp: {} {}".format(hightemp, unit.upper())) #print the low temperature data with units in capital letters
    print("Pressure:{}hPa".format(pressure))#print the pressure data with units
    print("Humidity:{}%".format(humidity)) #print the humidity data with units
    print("Cloud Cover:", cloudcover) #print the cloud cover data
    print() #print a blank line

def tempunit(temp, unit=None): #defined function tempunit passing through variables temp and unit with default value none
    while True: #while statement
        if unit == "f": #if statement that if the user's response is f, then...
            temp = (temp-273.15)*9/5+32 #calculate the temperature in farheinheit using Kelvins
        elif unit == "c": #else if statement if the user's response is c, then...
            temp -= 273.15 #calculate the temperature in celcius using Kelvins
        elif unit == "k": #else if statement if the user's response is k, then...
            temp = temp #the temperature is equal to itself since the original temperature given is in Kelvins
        else: #else statement that if the user enters anything other than f, c, or k
            unit = input("Would you like to view temps in Fahrenheit, Celsius, or Kelvin. Enter 'F' for Fahrenheit, 'C' for Celsius, 'K' for Kelvin.\n").casefold() #unit is equal to the user's input of the question asking what units they would like to see: F, C or K
            continue #the program will go back to the beginning of the while loop
        return temp, unit #return the temp and unit values

def zipcheck(zipcode): #function called zipcheck that validates the user's inputted zip code in the main function
    if zipcode.isdigit() and (len(zipcode) == 5): #if statement that the zipcode must be 5 digits, then...
        return True#return true that this is the required format of zip codes
    else: #else statement that if the zip code is anything other than a 5 digit zip code, then...
        print("That is not a valid zip code.\n") #print to the user that it is not a valid zip code
        return False#return false that this is not the required format of zip codes

if __name__ == "__main__": #properly defined main method
    print("Welcome User!\n") #Welcomed the end users to the weather program
    while True: #while statement that allows the user to run the program multiple times to allow them to look up weather conditions for multiple locations
        answer = input("Would you like to look up weather data by US city or zip code? Enter 1 for US city and 2 for zip code, or X to exit: \n").casefold() #answer is defined as the input from the user asking if they want weather using their US City or Zip Code, or if they want to exit. Used casefold so that both upper and lower cases are accepted
        if answer == "1": #if the user's response is 1 and valid, then...
            location = input("Please enter US city name: \n") #the location is defined as the user's input for the US City
        elif answer == "2": #if the user's response is 2 and valid, then...
            location = input("Please enter zip code: \n") #the location is defined as the user's input for the zip code
            if not zipcheck(location): #if the zip code is invalid using the zipcheck function, then...
                continue #the program will go back to the beginning of the while loop
        elif answer == "x": #if the user's response is X, then...
            print("Goodbye! Thank you! Come again!") #this goodbye message is displayed to the user, and...
            break #the program terminates
        else: #if the user's response is anything other than 1, 2, or X, then their response is invalid, and...
            print("This is not valid response. Please try again.\n") #print statement that notifies the user that their input not a valid response
            continue #the program will go back to the beginning of the while loop
        weather = weatherdata(location, answer) #weather variable is defined as weatherdata and passes through location and answer
        if weather.status_code == 404: #if the status code for weather is 404 (not found), then...
            print("Location cannot be found. Please try again.\n") #print that location cannot be found, and..
            continue #the program will go back to the beginning of the while loop
        prettyprint(weather) #pretty print function is called passing weather to display a readable output for the end user
