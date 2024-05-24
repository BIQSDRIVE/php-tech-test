## Task: Create an application to convert an XML file to Json

#### Work description:

You are hired to create an application that needs to process an XML document containing sales info for a number of countries.
The data in the XML needs to be enriched, grouped, sorted and exported to a JSON file.
More export formats (csv, excel, pdf, ...) might be required in the near future, so this might be something to keep in mind when you are creating the application.

#### This is what you know

* this XML file (`data/input/data.xml`) needs to be converted to a JSON file.
* the XML file contains country names and an additional "itemsSold" field for each country.
* a country can appear multiple times in the XML document.
* the JSON file needs to contain a sum of the itemsSold values (= totalItemsSold) + country appearances count (= appearances), grouped by country code.
* additional information for each country needs to be fetched from the `data/countriesV3.1.json` file (by countryName).
* expected output file(s): `data/output/Y-M-d_H-i-s_data.json` (eg. 2024-02-01_17-10-31_data.json).
* an example of the JSON structure can be found in `data/output/example.json`.

#### Requirements:

* create a CLI script to convert the XML file to JSON.
* sort the information by countryCode in ascending order.
* fetch additional country information (see the `data/countriesV3.1.json` file), you can find the country by using the countryName field in the XML.

Additional info that needs to be added to the output JSON file:

* countryCode: cca3 country code
* countryNames: list of name.nativeName.common, separated by ','
* meta.currency: 1st item in currencies (name field)
* meta.capital: 1st item in capital array

JSON structure of 1 country item in the export file:

```
{
    "countryCode": "BEL",                       // cca3 country code,
    "countryNames": "Belgien,Belgique,België",  // list of all country names, separated by ',' (see: name.nativeName.common)
    "totalItemsSold": 27,                       // sum of itemsSold in the XML file for Belgium
    "appearances": 2,                           // number of Belgium items in the XML file
    "meta": {
        "currency": "Euro",                     // currency, (name of 1st currency in list)
        "capital": "Brussels"                   // capital, (name of 1st capital in list)
    }
},
```

---

### Extra task 1: persist the information in a database.
* next to creating the JSON file, persist the JSON data in a database.
* add a timestamp as batch_id (every time the script is executed a new batch_id is created).

For instance:

| batch_id            | country_code | total_items_sold | ... |
|---------------------| ------------ | ---------------- | --- |
| 2022-01_01-09-12-31 | BEL          | 27               | ... |
| 2022-01_01-09-12-31 | DEU          | 4                | ... |
| 2022-02-01_17-10-12 | BEL          | 18               | ... |
| 2022-02-01_17-10-12 | DEU          | 9                | ... |

You can create multiple tables if you want (e.g. batch and batch_entries, ...).

---

### Extra task 2: display the info in the database in an Angular app.
* display the json data from the database (styling is not (that) important).
* add a dropdown filter for the batch_id:
	* upon initial load, no country information is displayed, it is required to select a batch_id first.
	* when a batch_id is selected the list of countries for the selected batch_id is retrieved from the server and the info for each country is displayed (items sold, appearances, ...).
* expose an API endpoint from your backend application to the frontend:
  * to fetch a list of sorted batch_ids (for the filter, most recent first).
  * to fetch a list of country data items, filtered by batch_id, sorted by county_code.

### Extra task 3: test your solution
* add unit / integration / functional tests to prove your solution works.

---

## Technology stack
PHP 8, Laravel/Symfony/..., MySQL, Angular, ...

## Evaluation - what are we looking for in the solution?
* does it work?
* clean code (maintainability, readability, testability and comprehensibility, SOLID)
* code organisation
* data modelling
* extra bonus points for the tests
