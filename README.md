# README

### Overview
This is the repository for the backend application which works in conjunction with our [front end application](https://github.com/csheesley/ccs-frontend), to create the full functioning website - **[inCrisis.herokuapp.com](https://incrisis.herokuapp.com/)**

Visitors who use our application can quickly and easily find the closest Walk-In Crisis Center based on their location, which can be manually entered or gathered from the browser. Our backend application incorporates the latitude and longitude of the user with the Google Distance Matrix API, returning ordered crisis centers based on proximity. Once a user finds the nearest walk-in center, there are links to choose the preferred mode of transportation to that center (driving, walking, biking, or public transit), along with an option to receive a text notification containing information about the closest center.

Due to the sensitive nature of our application, no user information is stored or tracked. Ease of use, accessibility, and reducing barriers were of top concern.

### Links
Production Link: https://incrisis.herokuapp.com/  
Front End Repository: https://github.com/csheesley/ccs-frontend

### Key Learnings
- Consuming and Building API endpoints
- Transforming and sorting data
- Configuration of Circle CI
- Implementation of Twilio
- Documentation and Communication with Front End Team

### Endpoint Documentation  
All endpoints are preceded by the following url: https://cohelp-backend.herokuapp.com

---
**GET /api/v1/locations**  
Returns all crisis center locations in our database, along with their associated information.

Required Parameters:
`no required parameters`

Example Request:
`GET https://cohelp-backend.herokuapp.com/api/v1/locations`
```
Request:
Content-Type: application/json
Accept: application/json
```
```
Response:
status: 200
body:
{
locations: [
  {
    "id": 1,
    "name": "Center for Mental Health: Crisis Walk-In Crisis Center",
    "phone": 3034250300,
    "street": "4643 Wadsworth Blvd",
    "city": "Wheat Ridge",
    "state": "CO",
    "zip": 80033,
    "office_hours": "24/7",
    "lat": 39.7807,
    "lng": -105.0828,
    "created_at": "2019-07-24T21:30:35.904Z",
    "updated_at": "2019-07-24T21:30:35.904Z",
    "website": "https://www.centermh.org/crisis-walk-in-center/",
    "logo": "https://github.com/CSheesley/ccs-frontend/blob/all-centers-pg/src/assets/images/center-logos/wheatridge-logo.png?raw=true"
  },
  {
    "id": 2,
    "name": "AllHealth Network Crisis Walk-In Center",
    "phone": 3037303303,
    "street": "6509 S Santa Fe Dr",
    "city": "Littleton",
    "state": "CO",
    "zip": 80120,
    "office_hours": "24/7",
    "lat": 39.5982,
    "lng": -105.0218,
    "created_at": "2019-07-24T21:30:35.947Z",
    "updated_at": "2019-07-24T21:30:35.947Z",
    "website": "https://www.allhealthnetwork.org/services/crisis-services/",
    "logo": "https://github.com/CSheesley/ccs-frontend/blob/all-centers-pg/src/assets/images/center-logos/littleton-logo.png?raw=true"
  },
    ...
  ]
}
```
---
**GET /api/v1/locations/sort**  
Returns all crisis center locations and their information, ordered from closest to farthest geographically - based on a users location (latitude and longitude).

Required Parameters:
`lat` - Float: Up to four decimal places
`lng` - Float: Up to four decimal places

Example Request:
`GET https://cohelp-backend.herokuapp.com/api/v1/locations/sort?lat=39.7504&lng=-104.9963`
```
Request:
Content-Type: application/json
Accept: application/json
```
```
Response:
status: 200
body:
{
locations: [
  {
    "id": 4,
    "name": "Mental Health Center of Denver",
    "phone": 3035041299,
    "street": "4353 E Colfax Ave",
    "city": "Denver",
    "state": "CO",
    "zip": 80220,
    "office_hours": "24/7",
    "lat": 39.7403,
    "lng": -104.9363,
    "website": "https://mhcd.org/suicide-prevention/",
    "logo": "https://github.com/CSheesley/ccs-frontend/blob/all-centers-pg/src/assets/images/center-logos/mhcd.jpg?raw=true",
    "miles": 3.7,
    "meters": 5979.0,
    "minutes": 15.0,
    "seconds": 878.0
  },
  {
    "id": 1,
    "name": "Center for Mental Health: Crisis Walk-In Crisis Center",
    "phone": 3034250300,
    "street": "4643 Wadsworth Blvd",
    "city": "Wheat Ridge",
    "state": "CO",
    "zip": 80033,
    "office_hours": "24/7",
    "lat": 39.7807,
    "lng": -105.0828,
    "website": "https://www.centermh.org/crisis-walk-in-center/",
    "logo": "https://github.com/CSheesley/ccs-frontend/blob/all-centers-pg/src/assets/images/center-logos/wheatridge-logo.png?raw=true",
    "miles": 8.8,
    "meters": 14236.0,
    "minutes": 16.0,
    "seconds": 953.0
  },
    ...
  ]
}
```
---
**POST /api/v1/locations/information_text**  
Creates two subsequent SMS text messages which are sent to a user's phone number. These SMS messages include (1) the name of the nearest crisis center based on their given location, and (2) information about that center - address, office_hours, phone.

Required Parameters:
`location_id` - Integer: Associated with the closest crisis center which was returned in the previous API call.
`phone` - Integer: Ten consecutive digits

Example Request:
`POST http://localhost:3000/api/v1/locations/information_text?location_id=3&phone=1234567890`
```
Request:
Content-Type: application/json
Accept: application/json
```
```
Response:
status: 201
body:
{
  "response": "Text Message Sent"
}
```
Example SMS Message:   

<img width="479" alt="Screen Shot 2019-07-24 at 8 54 20 AM" src="https://user-images.githubusercontent.com/43529041/61804176-b27fff80-adf0-11e9-94f4-f6adb9a5d5aa.png">

---
### Versions
Ruby 2.4.1  
Rails 5.2.3  
Bundler 2.0.2  

### Local Setup
Install Dependencies  
`$ bundle install`

Database Setup  
`$ rails db:{create, migrate, seed}`

### Testing
`$ rspec` - will run the full test suite.    
`VCR` is being used to mock out API calls in tests.  

### Circle CI
[![CircleCI](https://circleci.com/gh/CSheesley/ccs_cross_poll_backend.svg?style=svg)](https://circleci.com/gh/CSheesley/ccs_cross_poll_backend)

### Authors:

[Corey Sheesley](https://github.com/CSheesley)

[Brennan Duffey](https://github.com/BrennanDuffey)

[Kelly Zick](https://github.com/misskelly/)

[Sally Haefling](https://github.com/SallyHaefling)
