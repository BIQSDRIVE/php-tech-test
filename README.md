## Task: Craete a CLI script to convert an XML file to Json

#### Work description:

* conversion of an XML file (`data/input/data.xml`) to a JSON file.
* the xml file contains country names and an additional count field for each country.
* a country can appear multiple times in the XML document.
* the JSON file needs to contain a sum of the count values (= totalCount) + country appearances count (= itemCount), grouped by country code.
* additional information for each country needs to be fetched from a REST API.  
* expected output file(s): `data/output/Y-M-d_H-i-s_data.json` (eg. 2022-02-01_17-10-31_data.json).
* an example of the JSON structure can be found in `data/output/example.json`.

#### Requirements:

* create a CLI script to convert the XML file to JSON.
* Sort the information by countryCode in ascending order.
* fetch additional country information from an external API (https://restcountries.com/#api-endpoints-v3-all), e.g. https://restcountries.com/v3.1/name/{countryName}, the countryName field can be found in the XML file.

Additional info in the JSON file (from REST service):

example: https://restcountries.com/v3.1/name/belgium

* countryCode: cca3 country code
* countryNames: list of nativeName, separated by ,
* meta.currency: 1st item in currencies array
* meta.capital: 1st item in capital array

JSON structure of 1 country item:

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
* add a timestamp as batch_id (every time the script is executed this batch_id is created).

For instance:

| batch_id            | country_code | total_count | ... |
| ------------------- | ------------ | ----------- | --- |
| 2022-01_01-09-12-31 | BEL          | 27          | ... |
| 2022-01_01-09-12-31 | DEU          | 4           | ... |
| 2022-02-01_17-10-31 | BEL          | 18          | ... |
| 2022-02-01_17-10-31 | DEU          | 9           | ... |

### Extra task 2: visualise the information in the database in a VueJs/React component.
* display the json data in an HTML table (styling is not important).
* add a dropdown filter for the batch_id:
	* upon initial load, no country information is displayed, it is required to select a batch_id first.
	* when a batch_id is selected the list countries for the selected batch_id is retrieved from the server and displayed.
* expose an API endpoint to fetch a list of country items, filtered by batch_id, sorted by county_code.
* expose an API endpoint to fetch a unique list of sorted batch_ids (for the filter).

### Extra task 3: test your work
* add unit / integration / functional tests to prove your solution works.

## Technology stack
We would use PHP 8, Symfony, Doctrine, MySQL, VueJs, but feel free to use the PHP / Javascipt stack you are most comfortable with.

## Evaluation - what are we looking for in the solution?
* clean code (maintainability, readability, testability and comprehensibility)
* code organisation
* data modelling
* does it work?