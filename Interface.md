
# Table of Contents
- [[#Accessing the GraphQL Explorer]]
- [[#Writing Your Query]]
	- [[#Exploring Data]]
	- [[#Headers]]
- [[#Query Information]]
- [[#Conclusion]]


# Panadvert API Interface Usage Guide

Welcome to the Panadvert GraphQL API. This guide will walk you through the steps to create and run queries against our GraphQL endpoint to fetch data such as city details. Let's get started.

***API ENDPOINT*** : https://api.panadvert.com/gks/gql/
## Accessing the GraphQL Explorer

The GraphQL [Explorer](https://api.panadvert.com/gks/explorer) is an interactive tool that allows you to build and test queries in real-time.

## Writing Your Query

1. **Start a New Query:**
   - In the GraphQL Explorer, start a new query by clicking on the "New" button or selecting "Add new Query" if you have other queries open.

2. **Constructing the Query:**
   - You can manually type your query or use the Explorer's interface to select the fields you're interested in.
   - For example, to query city details, you might use the following structure:
     ```graphql
     query MyQuery {
       cities {
         country
         country_id
         region
         region_id
         subregion
         subregion_id
         name
         id
       }
     }
     ```

3. **Running the Query:**
   - Once you've constructed your query, run it by clicking the play button on the top right corner of the Explorer.

4. **Viewing Results:**
   - The results of your query will appear in the pane on the right side of the Explorer.
   - If there are any issues, the Explorer will display an error message, often with details about what went wrong.
### Exploring Data

- Use the checkboxes in the Explorer to select or deselect fields, tailoring the query to return only the information you need.
- The Explorer can also auto-generate the query syntax for you as you select fields.
- You reconstruct the query using any language of your choice to get the data. Or you can simply copy and paste the data in a JSON file. 

Here's an example query that fetches cities and their associated details along with the expected JSON result:

```graphql
query MyQuery {
  cities {
    country
    country_id
    region
    region_id
    subregion
    subregion_id
    name
    id
  }
}
```

As mentioned in the [[Quick Start]] Guide, you can change the name of the query from 'MyQuery' to anything you want.

When run, this query would produce a result such as:

```json
{
  "data": [
    {
      "country": "Afghanistan",
      "country_id": 5258,
      "region": "Afghanistan",
      "region_id": 5258,
      "subregion": "Mazar-i-Sharif",
      "subregion_id": 5258,
      "name": "Mazar-i-Sharif",
      "id": 5258
    },
    ...
  ]
}

```

Remember to replace `YOUR_API_TOKEN` with your actual API token provided after registration in your headers as a `json object`. 

### Headers

- To set any necessary headers, such as an API token for authorization, use the 'Headers' section at the bottom left.
- Headers might include:

```json
{"Authorization": "Bearer YOUR_API_TOKEN","Content-Type": "application/json"}
```

for free sources the API Token is not needed, but recommended
## Query Information
The turquoise colored letters are filters, the blue letters are arguments. 

- **BookingData:** Provides information regarding hotels from booking.com. The ID is from Booking.com.
- **Cities:** A free for everyone resource that provides a tree structure of countries, regions, subregions and cities. *Note that there are many regions, subregions and cities with the same name. If you are going to store these in a database, we recommend having a different table for each level or a structure that accounts for duplicates* 
- **countries,regions,subregions:** Another free source, If you are interested in getting only names without duplicates, use these option.
## Conclusion

That's it! You've now learned how to use Panadvert's API to retrieve city details. Explore different queries and see what other insights you can uncover with our API. If you have any questions or need further assistance, please reach out to [api@panadvert.com](mailto:api@panadvert.com).