## Task: CLI script to convert an XML file to Json

#### Work description:

* conversion of an XML file to a JSON file.
* the xml file contains country names and an additional count field.
* a country can appear multiple times in the XML document.
* the JSON file needs to contain a sum of the count values (= totalCount) + country appearances count (= itemCount), grouped by country code. 
* additional information for each country needs to be fetched from a REST API.  
* expected output file(s): data/output/YY_MM_DD_HH_MM_SS_data.json
* an example of the JSON structure can be found in data/output/example.json

#### Requirements / todo:

* create a CLI script to convert the XML file to JSON
* Sort the information by countryCode in ascending order.
* fetch additional country information from an external API (https://restcountries.com/#api-endpoints-v3-all), e.g. https://restcountries.com/v3.1/name/{countryName}, the countryName field can be found in the XML file.

Additional info in the JSON file (from REST service):

example: https://restcountries.com/v3.1/name/belgium

* countryCode: cca3 country code
* countryNames: list of nativeName, separated by ,
* meta.currency: 1 item in currencies array
* meta.capital: 1 item in capital array

Json structure of 1 country item:

```
{
    "countryCode": "BEL",                       // cca3 country code, returned from the restcountries service
    "countryNames": "Belgien,Belgique,België",  // list of all country names, separated by ,
    "totalCount": 27,                           // sum of count in the XML file for Belgium
    "itemCount": 2,                             // number of Belgium items in the XML file
    "meta": {
        "currency": "Euro",                     // currency, returned from the restcountries service (name of 1st currency in list)
        "capital": "Brussels"                   // capital, returned from the restcountries service (name of 1st capital in list)
    }
},
```

### Extra task 1: persist the information to the database.
* next to creating the JSON file, persist the JSON data to the database.
* add a timestamp as batch_id, for instance:

| batch_id            | country_code | total_count | ... |
| ------------------- | ------------ | ----------- | --- |
| 2022_01_01_09:12:31 | BEL          | 27          | ... |
| 2022_01_01_09:12:31 | DEU          | 4           | ... |
| 2022_02_01_17:10:31 | BEL          | 18          | ... |
| 2022_02_01_17:10:31 | DEU          | 9           | ... |

### Extra task 2: visualise the information in the database in a VueJs/React component.
* expose the information in the database via an API endpoint that returns JSON
* display the json data in an HTML table (styling is not important)
* add a dropdown filter for the batch_id
	* upon initial load, no information is displayed, it is required to select a batch_id 
	* when a batch_id is selected a new list is retrieved from the server and displayed

### Extra task 3: test your work
* add unit / integration / functional tests to prove your solution works.

## Evaluation - what are we looking for in the solution?
* does it work?
* code organisation
* data modelling
* clean code (maintainability, readability, testability and comprehensibility)