# Clima

## Core Features :
1. List of weather data for 8 days
2. Tapping on an item will show weather details
3. Calling an OpenWeatherMap API to get the weather information 
4. It will Support all orientation
5. Local Notifications to show weather alert
6. Settings view to change from Centigrade to Fahrenheit and vice versa
7. Offline/Local storage 
8. Followed MVVM Architecture 

## Work Flow :
- Asked for Notification Permission (to show weather alert)
- Hitting Weather API and Getting Current Weather Data as well as Forecast Data for next 7 Days 
- Saving those data into Local 
- If a weather alert is available in the response then the app will push local notification 
- UI is observing the Local changes so data will reflect the user
- Default parameter for the temperature is centigrade 
- Temperature can be changed from the setting in Fahrenheit and vice versa

## I Used :
- SwiftUI 
- Combine
- Realm 
- Alamofire
- SwiftyJSON
- User Notification

## Understanding the App Architecture 

### Repo :

API_Handler <br> 
WeatherInformationStore <br> 
RealmPersistanceIntializer 

<br>

### Models :
 WeatherInfoDB <br> 
 WeatherAlert <br> 
 TypeOfTemp <br> 
 WeatherInfo 

<br> 

### Views :
DashboardView <br> 
NotificationPermissionView <br> 
LoadApplication <br> 

<br> 

### ViewModel :
DashboardViewModel <br> 
NoticationManger <br> 

<br>

### API_Handler

```swift
// This function will return true only if current date would't match with already saved date
private func isDateChaged() -> Bool


// This function will call the API and update the data after getting the response
func callAPIAndUpdateData()

// This will request for weather data
private func requestWeatherInfo(url : URL , method: HTTPMethod, completion : @escaping (Bool) -> Void)


// Save all data to local using WeatherInformationStore object passed from repo class
private func saveAllData(data : JSON)

```

<br>

### WeatherInformationStore

```swift

// This function will read all data of type weatherInfo
func readWeatherInfoSavedData()


// This function will read data of type weatherAlert
func readWeatherAlertSavedData()


// This function will return the true if saved temp type is centigrade otherwise return false
func getTempType() -> Bool


// This function will save the type of temperature when the user changed from settings
func saveTempType(type : Bool)


// This function will save weather alert in local
func saveWeatherAlerts(sender_name : String, event : String, start : Int64, end : Int64, _description : String, completion : (Bool) -> Void)


// This function will save weather informations in local
func saveWeatherInfo(degree : String, atmophericPressure : String, humidity : String, status : String, timeStamp : Int64, windSpeed : String, image : String, completion : @escaping (Bool) -> Void)


// This function will delete all weatherInfo and WeatherAlert data from local
func deleteData()
```

<br>

### DashboardViewModel

```swift
// This will give access to API_handler and WeatherInformationStore Objects
private var repo : Repo


// UI is observing this variable to show the weather info
@Published var weatherInfo = [WeatherInformation]()


// By default temperature type is in Centigrade. This will be used to update the setting button view.
@Published var isTempCentigrade : Bool = true


// This is used to know when the app comes to Foreground and then Hit the API
@Published var appInForground = true


// This is the object of the notification manager
@Published var notificationManager : NotificationManager


// This is used to store the selected card for UI and Animations
@Published var selectedCard : WeatherInformation


// This function is used to push the local notification
func pushWeatherAlertNotification(data : WeatherAlerts)


// Used to save the selected temperature and corvert it
func isSelectedTempCentigrade(type : Bool)
 
 
// Used to convert Fahrenheit to Centigrade
func convertTemperatureToCentigrade()
 
 
// Used to convert Centigrade to Fahrenheit
func convertTemperatureToFahrenheit()


// Used for update the selectedCardInfo to display on view 
func updateSelectedCard(degree : String, uuid : Int)


// Used to convert timeStamp into dd-MM-yyyy format
func convertTimestampToDate(timeStamp : Int64)

```

![alt text](https://github.com/MdMugish/Clima/blob/master/Notification%20Permission.png)
![alt text](https://github.com/MdMugish/Clima/blob/master/Weather%20Dashboard%20.png)
