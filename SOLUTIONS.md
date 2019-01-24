# Solutions to Iteration 2

You already know how this goes, so let's start working:

1. All the companies that it's name match 'Babelgum'. Retrieve only their `name` field:
    The projection parameter determines which fields are returned in the matching documents.

    **COMPASS**

    ```COMPASS
    FILTER: { name: "Babelgum" }
    PROJECT: { name: 1, _id: 0 }
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({ name: "Babelgum" }).projection({ name: 1, _id: 0 })
    ```

___

2. All the companies that have more than 5000 employees. Limit the search to 20 companies and sort them by  **number of employees**:

    `$gt`  selects those documents where the value of the field is greater than (i.e. >) the specified value.  
    `SORT`: -1 order of ascending and 1 in descending

    **COMPASS**

    ```COMPASS
    FILTER: { number_of_employees: { $gt: 5000  }}
    SORT: { number_of_employees: -1 }
    LIMIT: 20
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({number_of_employees: { $gt: 5000  }}).limit(20).sort({number_of_employees: -1})
    ```
___

3. All the companies founded between 2000 and 2005, both years included. Retrieve only the `name` and `founded_year` fileds.
4. All the companies that had a Valuation Amount of more than 100.000.000 and have been founded before 2010. Retrieve only the `name` and `ipo` fields.
5. All the companies that have less than 1000 employees and have been founded before 2005. Order them by the number of employees and limit the search to 10 companies.
6. All the companies that don't include the `partners` field.
7. All the companies that have a null type of value on the `category_code` field.
8. All the companies that have at least 100 employees but less than 1000. Retrieve only the `name` and `number of employees` fields.
9. Order all the companies by their IPO price descendently.
10. Retrieve the 10 companies with more employees, order by the `number of employees`
11. All the companies founded on the second semester of the year. Limit your search to 1000 companies.
12. All the companies founded before 2000 that have and acquisition amount of more than 10.000.000
13. All the companies that have been acquired after 2015, order by the acquisition amount, and retrieve only their `name` and `acquisiton` field.
14. Order the companies by their `founded year`, retrieving only their `name` and `founded year`.
15. All the companies that have been founded on the first seven days of the month, including the seventh. Sort them by their `aquisition price` descendently. Limit the search to 10 documents.
16. All the companies on the 'web' `category` that have more than 4000 employees. Sort them by the amount of employees in ascendant order.
17. All the companies which their acquisition amount is more than 10.000.000, and currency are 'EUR'.
18. All the companies that have been acquired on the first trimester of the year. Limit the search to 10 companies, and retrieve only their `name` and `acquisition` fields.
19. All the companies that have been founded between 2000 and 2010, but have not been acquired before 2011.


Happy Coding! :heart: