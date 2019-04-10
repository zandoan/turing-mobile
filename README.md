# Turing Mobile

## Welcome
Welcome to the Mobile Turing Challenge. Here you'll find some examples to reach your goal. 

## Swagger Documentation 
[https://mobilebackend.turing.com/docs](https://mobilebackend.turing.com/docs)

## Root Endpoint 
[https://mobilebackend.turing.com](https://mobilebackend.turing.com)

## URL Images

https://mobilebackend.turing.com/images/products/

Example: https://mobilebackend.turing.com/images/products/corsica.gif

## Simple Example - React Native
Below you can see a piece of code:

```javascript
getDepartments = async () => {
    fetch('https://mobilebackend.turing.com/departments', {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
      }
    })
      .then((response) => response.json())
      .then((responseJson) => {
        this.setState({ departments: responseJson})
        //Alert.alert(responseJson[0].name);
      })
      .catch((error) => {
        console.error(error);
      });
  }


  render() {
    return (
      <View style={styles.container}>
        <FlatList
          data={this.state.departments}
          renderItem={({item}) => <Text style={styles.item}>{item.name}</Text>}
          keyExtractor={(item, index) => index.toString()}
        />
      </View>
    );
  }
```
![](image_react_native.png)

## Authentication
Just some endpoint required Authentication, you can check it in the documentation. 
The Customer login provide the Token to use in the other endpoints that required it.

Token's example: ```Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjdXN0b21lcl9pZCI6MTIsIm5hbWUiOiJFZGVyIFRhdmVpcmEiLCJyb2xlIjoiY3VzdG9tZXIiLCJpYXQiOjE1NTA3ODYyMjAsImV4cCI6MTU1MDg3MjYyMH0.QEGdry367EQNxBqzuUDCGJscWkq8YQwJdGBgV3hztR0```
 
The Token need to be in the header param **"user-key"**. Let's see an example below.

Example Using login Authentication (React Native):
```javascript
login = async () => {
    fetch('https://backendapi.turing.com/customer/login', {
      method: 'POST',
      headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json',
      },
      data: JSON.stringify({email: "CUSTOMER EMAIL", passsword: "CUSTOMER PASSWORD"})
    })
      .then((response) => response.json())
      .then((responseJson) => {
        //do something
        console.log(responseJson);
      })
      .catch((error) => {
        console.error(error);
      });
  }	
```

Response example:
```json
{
  "user": {
    "customer_id": 12,
    "name": "Eder Taveira",
    "email": "challenge@turing.com",
    "address_1": "",
    "address_2": "",
    "city": "",
    "region": "",
    "postal_code": "",
    "shipping_region_id": null,
    "day_phone": null,
    "eve_phone": null,
    "mob_phone": null
  },
  "accessToken": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjdXN0b21lcl9pZCI6MTIsIm5hbWUiOiJFZGVyIFRhdmVpcmEiLCJyb2xlIjoiY3VzdG9tZXIiLCJpYXQiOjE1NTA3ODYyMjAsImV4cCI6MTU1MDg3MjYyMH0.QEGdry367EQNxBqzuUDCGJscWkq8YQwJdGBgV3hztR0",
  "expires_in": "24h"
}
```

Example with header and token:
```javascript
getCustomerInfo = async () => {
    fetch('https://backendapi.turing.com/customer', {
      method: 'GET',
      headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json',
        'user-key': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjdXN0b21lcl9pZCI6MTIsIm5hbWUiOiJFZGVyIFRhdmVpcmEiLCJyb2xlIjoiY3VzdG9tZXIiLCJpYXQiOjE1NTA3ODYyMjAsImV4cCI6MTU1MDg3MjYyMH0.QEGdry367EQNxBqzuUDCGJscWkq8YQwJdGBgV3hztR0',
      }
    })
      .then((response) => response.json())
      .then((responseJson) => {
        //do something
        console.log(responseJson);
      })
      .catch((error) => {
        console.error(error);
      });
  }
```

## Pagination
All params of pagination are not required.

The pagination can to have the query params below:

* **page** - Number of page. Default is "1".
* **limit** - Number of limit por page. (Check [the documentation](https://mobilebackend.turing.com/docs) to see what the default for each endpoint).

Examples: 

* https://mobilebackend.turing.com/categories?page=1&limit=20
* https://mobilebackend.turing.com/products?page=1
* https://mobilebackend.turing.com/products?limit=30

Some endpoints (shoppingcart and products) have a  no required param **"description_length"**.

Return of list with pagination:
```json
{
  "count": 40,
  "rows": [
    {
      "category_id": 1,
      "name": "French",
      "description": "The French have always had an eye for beauty. One look at the T-shirts below and you'll see that same appreciation has been applied abundantly to their postage stamps. Below are some of our most beautiful and colorful T-shirts, so browse away! And don't forget to go all the way to the bottom - you don't want to miss any of them!",
      "department_id": 1
    }
  ]
}
```

## Order

To sort some lists use the no required param **"order"**.

The format of param is as this REGEX: '/^([^\s]+),(DESC|ASC)$/'

Example: 

* https://mobilebackend.turing.com/categories?order=name,DESC
 


## Errors

The error response has the following structure:

* **code** - Error's Code.
* **message** - Error's Message.
* **field** - Error's Field.

Example of Error:
```json
{"error":{"status":400,"code":"USR_05","message":"The email don't exists.","field":"email"}}
```

