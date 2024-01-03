## Table of Contents
- [[#Introduction]]
- [[#Your API Token]]
	- [[#Make your API Token]]
	- [[#Use your API Token]]
- [[#Examples & Use Cases]]
	- [[#Linux/MacOs Terminal Curl]]
	- [[#Windows command Line Curl]]
	- [[#Windows Power Shell]]
	- [[#PHP]]
	- [[#JavaScript node-fetch]]
	- [[#Java]]
	- [[#C Sharp]]
	- [[#Python]]
	- [[#Ruby]]
	- [[#GO]]
	- [[#Rust]]
	- [[#Notes]]
- [[#Tips]]

## Introduction

Our API works with any programming language that can make http/https requests.
Below you can find some example code snippets to get you started.


1. **acquire your API keys:** contact us in order to make you an account and give you access to your API keys.
2. **Start of by defying the query you would like to make:** Thanks to Yoga GraphQL you can use the UI to build your queries with a simple click of a button. Simply select the filed you would like to to get and you are ready to go.
3. **Use the templates below to kick-start your project:** Copy the code  snippets from your language of preference. The templates are for **PHP,JavaScript,C Sharp, java and more** we also provide the raw **curl**.
**Note:** In graphQL you can name a query, in this case the name of the query is "MyQuery", you can give it any name you want.

## Your API Token

### Make your API Token
First things first is to get your API Token.

Navigate to the [home page](https://api.panadvert.com/gks/) and click on login. Create a free account and proceed with the verification process (Verification email send to your email address). After you have verified your email, login to your account. To make an API key, navigate to [Tokens](https://api.panadvert.com/gks/tokens) Select all the options you want and specify an **Expiration Date**. 

- It is ***highly*** recommended that you specify an Expiration date for your token for security reasons.
- It is also recommended to generate different tokens for different use cases / departments.
- Your tokens ***must*** be stored in a safe location. 

### Use your API Token

In order to use your API token, you must add as header in your **POST request** 'Authorization' with the value 'Bearer {API KEY}'.

Below you can see a CURL Example for Linux/MacOs Terminal using the header.

**Note** that the "Bearer" keyword and the space between "Bearer" & your API key are mandatory.

```bash 
curl -X POST \
  https://api.panadvert.com/gks/gql/ \
  -H 'Accept-Language: en-US,en;q=0.9' \
  -H 'Authorization: Bearer {API_KEY}'\
  -H 'Content-Type: application/json' \
  -d '{"query":"query MyQuery {cities {country country_id region region_id subregion subregion_id id name}}", "operationName":"MyQuery", "extensions":{}}'
```
 

## Examples & Use Cases

In the examples below you can find ready to go queries for accessing the entire *country,region,subregion & city* structure without using an API Token. The location levels are following the order mentioned previously.  From that point on it is very straight forward. You can create the queries you want to run in our [interface](https://api.panadvert.com/gks/explorer) and paste the query in the ***data*** parameter. You can find more information on how to query the API in [[Interface]] Documentation.
### Linux/MacOs Terminal Curl

```bash 
curl -X POST \
  https://api.panadvert.com/gks/gql/ \
  -H 'Accept-Language: en-US,en;q=0.9' \
  -H 'Content-Type: application/json' \
  -d '{"query":"query MyQuery {cities {country country_id region region_id subregion subregion_id id name}}", "operationName":"MyQuery", "extensions":{}}'
```

### Windows command Line Curl

```bash
curl -X POST ^
  https://api.panadvert.com/gks/gql/ ^
  -H "Accept-Language: en-US,en;q=0.9" ^
  -H "Content-Type: application/json" ^
  -d "{\"query\":\"query MyQuery {cities {country country_id region region_id subregion subregion_id id name}}\", \"operationName\":\"MyQuery\", \"extensions\":{}}"
```

### Windows Power Shell

```powershell
$response = Invoke-WebRequest -Uri "https://api.panadvert.com/gks/gql/" -Method POST `
  -Headers @{
    "Accept-Language" = "en-US,en;q=0.9"
    "Content-Type" = "application/json"
  } `
  -Body '{
    "query": "query MyQuery {cities {country country_id region region_id subregion subregion_id id name}}",
    "operationName": "MyQuery",
    "extensions": {}
  }'

# Convert the response from JSON format to a PowerShell object
$responseData = $response.Content | ConvertFrom-Json

# Access and print the 'cities' array from the data
$responseData.data.cities | ForEach-Object {
  Write-Host "Country: $($_.country)"
  Write-Host "City Name: $($_.name)"
  Write-Host "City ID: $($_.id)"
  Write-Host ""
}
  ```

### PHP

```PHP
<?php
$url = 'https://api.panadvert.com/gks/gql/';
$headers = [
    'Accept-Language: en-US,en;q=0.9',
    'Content-Type: application/json'
];
$data = json_encode([
    'query' => 'query MyQuery {cities {country country_id region region_id subregion subregion_id id name}}',
    'operationName' => 'MyQuery',
    'extensions' => new stdClass()
]);

$ch = curl_init($url);
curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($ch);
curl_close($ch);

$countries = json_decode($response, true)['data']['cities'];

foreach ($countries as $country) {
    echo $country['country'] . "\n";
    echo $country['name'] . "\n";
    echo $country['id'] . "\n";
    echo "\n";
}
?>
```

### JavaScript node-fetch

```javascript
const fetch = require('node-fetch');

const url = 'https://api.panadvert.com/gks/gql/';
const headers = {
    'Accept-Language': 'en-US,en;q=0.9',
    'Content-Type': 'application/json'
};
const data = JSON.stringify({
    query: 'query MyQuery {cities {country country_id region region_id subregion subregion_id id name}}',
    operationName: 'MyQuery',
    extensions: {}
});

fetch(url, { method: 'POST', headers: headers, body: data })
    .then(response => response.json())
    .then(data => {
        const countries = data.data.cities;
        countries.forEach(country => {
            console.log(country.country);
            console.log(country.name);
            console.log(country.id);
            console.log('\n');
        });
    })
    .catch(error => console.error('Error:', error));

```

### Java

```java
import okhttp3.*;

import java.io.IOException;

public class Main {
    public static void main(String[] args) throws IOException {
        OkHttpClient client = new OkHttpClient();
        String url = "https://api.panadvert.com/gks/gql/";
        String json = "{\"query\":\"query MyQuery {cities {country country_id region region_id subregion subregion_id id name}}\", \"operationName\":\"MyQuery\", \"extensions\":{}}";
        RequestBody body = RequestBody.create(json, MediaType.parse("application/json"));
        Request request = new Request.Builder()
                .url(url)
                .addHeader("Accept-Language", "en-US,en;q=0.9")
                .addHeader("Content-Type", "application/json")
                .post(body)
                .build();

        try (Response response = client.newCall(request).execute()) {
            // Assuming the response JSON structure is similar to the Python example
            // Additional parsing will be required here
            System.out.println(response.body().string());
        }
    }
}
```
### C Sharp 

```c#
using System;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;

class Program
{
    static async Task Main(string[] args)
    {
        using (HttpClient client = new HttpClient())
        {
            var url = "https://api.panadvert.com/gks/gql/";
            var data = new StringContent("{\"query\":\"query MyQuery {cities {country country_id region region_id subregion subregion_id id name}}\", \"operationName\":\"MyQuery\", \"extensions\":{}}", Encoding.UTF8, "application/json");
            client.DefaultRequestHeaders.Add("Accept-Language", "en-US,en;q=0.9");

            var response = await client.PostAsync(url, data);
            string resultContent = await response.Content.ReadAsStringAsync();

            // Assuming the response JSON structure is similar to the Python example
            // Additional parsing and JSON deserialization will be required here
            Console.WriteLine(resultContent);
        }
    }
}
```

### Python

```python
import requests

url = 'https://api.panadvert.com/gks/gql/'

headers = {
'Accept-Language': 'en-US,en;q=0.9',
'content-type': 'application/json'
}

data = {
'query': 'query MyQuery {cities {country country_id region region_id subregion subregion_id id name}}',
'operationName': 'MyQuery',
'extensions': {}
}
response = requests.post(url, headers=headers, json=data, verify=False)
countries = response.json()['data']['cities']

for country in countries:

print(country['country'])
print(country['name'])
print(country['id'])
print('\n')
```

### Ruby

```ruby
require 'net/http'
require 'uri'
require 'json'

url = URI.parse('https://api.panadvert.com/gks/gql/')
headers = {
  'Accept-Language' => 'en-US,en;q=0.9',
  'Content-Type' => 'application/json'
}
data = {
  query: 'query MyQuery {cities {country country_id region region_id subregion subregion_id id name}}',
  operationName: 'MyQuery',
  extensions: {}
}.to_json

response = Net::HTTP.start(url.host, url.port) do |http|
  request = Net::HTTP::Post.new(url, headers)
  request.body = data
  http.request(request)
end

countries = JSON.parse(response.body)['data']['cities']
countries.each do |country|
  puts country['country']
  puts country['name']
  puts country['id']
  puts "\n"
end
```

### GO
```go
package main

import (
    "bytes"
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
)

func main() {
    url := "https://api.panadvert.com/gks/gql/"
    var jsonData = []byte(`{
        "query": "query MyQuery {cities {country country_id region region_id subregion subregion_id id name}}",
        "operationName": "MyQuery",
        "extensions": {}
    }`)
    req, _ := http.NewRequest("POST", url, bytes.NewBuffer(jsonData))
    req.Header.Set("Accept-Language", "en-US,en;q=0.9")
    req.Header.Set("Content-Type", "application/json")

    client := &http.Client{}
    resp, _ := client.Do(req)
    defer resp.Body.Close()

    body, _ := ioutil.ReadAll(resp.Body)

    var result map[string]interface{}
    json.Unmarshal([]byte(body), &result)

    countries := result["data"].(map[string]interface{})["cities"].([]interface{})
    for _, country := range countries {
        countryMap := country.(map[string]interface{})
        fmt.Println(countryMap["country"])
        fmt.Println(countryMap["name"])
        fmt.Println(countryMap["id"])
        fmt.Println()
    }
}
```

### Rust
```Rust
use reqwest;
use serde_json::{Value, json};
use std::collections::HashMap;

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let client = reqwest::Client::new();
    let url = "https://api.panadvert.com/gks/gql/";
    let mut headers = HashMap::new();
    headers.insert("Accept-Language", "en-US,en;q=0.9");
    headers.insert("Content-Type", "application/json");

    let data = json!({
        "query": "query MyQuery {cities {country country_id region region_id subregion subregion_id id name}}",
        "operationName": "MyQuery",
        "extensions": {}
    });

    let res = client.post(url)
        .headers(headers.into())
        .json(&data)
        .send()
        .await?;

    let json: serde_json::Value = res.json().await?;
    let countries = json["data"]["cities"].as_array().unwrap();

    for country in countries {
        println!("{}", country
```

### Notes

**All examples provide the same result**. _You can modify the query that is passed as JSON data in the request to make the request you want. In all cases we use our publicly available datasets so no authentication key is specified. It is generally recommended to use the API key even if you want to access publicly available datasets in order to make use of your own rate limiting compared to the guest rate limit, which in many cases is less requests per second compared to the licensed API keys. Our current rate limit is 5 requests per second. So you can use our API asynchronously.**._

**Example Response**
```json
{
  "data": {
    "cities": [
      {
        "country": "Greece",
        "country_id": 1,
        "region": "Cyclades",
        "region_id": 1,
        "subregion": "Mykonos",
        "subregion_id": 1,
        "id": 1,
        "name": "Ornos"
      },
      {
        "country": "Greece",
        "country_id": 1,
        "region": "Cyclades",
        "region_id": 1,
        "subregion": "Milos",
        "subregion_id": 2,
        "id": 50,
        "name": "Pollonia"
      }
    ]
  }
}
```

In the case of the example we accessed the cities table, we requested the name of the country this city is located, the id of the country, the name and id of region and sub-region and finally the name and id of the city.

The Response is JSON structured data accessed within the data and cities. You can loop through each element and get all the information you need. Currently we do not offer a filtration option in order to query for example only cities of a curtain country, but it's something we have in the works.

## Tips

- **API clients:** There are a number of applications like [postman](https://www.postman.com/), [Restfox](https://restfox.dev/) or [Insomnia](https://insomnia.rest/) to make requests to our API using a user interface. These API clients are mostly made for REST APIs, but you can provide your GraphQL query in JSON. Also note that Restfox has a GraphQL option.
- **Version Control:** We currently have a single version of our API which is in early access. If you notice our API is not working feel free to contact us at [techsupport@panadvert.com](mailto:techsupport@panadvert.com)in the case there are any different versions of our API, the guides are going to be updated accordingly with any changes.
- **Recommendations:** We are open to feedback and discussion regarding any changes and additions to our systems. Feel free to reach out and give us your feedback, can't wait to hear you out!!

