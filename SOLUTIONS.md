# Solutions to Iteration 2

You already know how this goes, so let's start working:

1. All the companies that it's name match 'Babelgum'. Retrieve only their `name` field:

    The ```projection``` parameter determines which fields are returned in the matching documents. 1 or true to include the field in the return documents and 0 or false to exclude the field.

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

3. All the companies founded between 2000 and 2005, both years included. Retrieve only the `name` and `founded_year` fileds:

    `$lte` selects the documents where the value of the field is less than or equal to (i.e. <=) the specified value.

    `$gte` $gte selects the documents where the value of the field is greater than or equal to (i.e. >=) a specified value

    **COMPASS**

    ```COMPASS
    FILTER: { founded_year: { $gte: 2000, $lte: 2005 } }
    PROJECT: { name: 1, founded_year: 1 }
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({ founded_year: { $gt: 1999, $lt: 2006 } }).projection({ name: 1, founded_year: 1 })
    ```
___
4. All the companies that had a Valuation Amount of more than 100.000.000 and have been founded before 2010. Retrieve only the `name` and `ipo` fields:

    `$lt` selects the documents where the value of the field is less than (i.e. <) the specified value.

    **COMPASS**

    ```COMPASS
    FILTER: { "ipo.valuation_amount": { $gt: 1000000 }, founded_year: { $lt: 2010 } }
    PROJECT: { name: 1, ipo: 1 }
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({"ipo.valuation_amount": { $gt: 1000000 }, founded_year: { $lt: 2010 }}).projection({ name: 1, ipo: 1 })
    ```
___

5. All the companies that have less than 1000 employees and have been founded before 2005. Order them by the number of employees and limit the search to 10 companies:

    **COMPASS**

    ```COMPASS
    FILTER: { number_of_employees: {$lt: 1000}, founded_year: {$lt: 2005} }
    SORT: { number_of_employees: 1 }
    LIMIT: 10
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({number_of_employees: {$lt: 1000}, founded_year: {$lt: 2005}}).limit(10).sort({number_of_employees: 1})
    ```
___

6. All the companies that don't include the `partners` field:

    `$exist` receives a boolean. When `boolean` is `true`, `$exists` matches the documents that contain the field, including documents where the field value is `null`. If `boolean` is `false`, the query returns only the documents that do not contain the field.

    **COMPASS**

    ```COMPASS
    FILTER: { partners: { $exists: false } }
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({partners: { $exists: false }})
    ```
___

7. All the companies that have a null type of value on the `category_code` field:

    **COMPASS**

    ```COMPASS
    FILTER: { category_code: null }
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({category_code: null})
    ```
___

8. All the companies that have at least 100 employees but less than 1000. Retrieve only the `name` and `number of employees` fields:

    **COMPASS**

    ```COMPASS
    FILTER: { number_of_employees: { $gt: 100 }, number_of_employees: { $lt: 1000 } }
    PROJECT: { name: 1, number_of_employees: 1 }
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({number_of_employees: {$gt: 100}, number_of_employees: {$lt: 1000}}).projection({name: 1, number_of_employees: 1})
    ```
___

9. Order all the companies by their IPO price descendently:

    **COMPASS**

    ```COMPASS
    SORT: { "ipo.valuation_amount": 1 }
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').createIndex({"ipo.valuation_amount": 1})
    db.getCollection('companies').find({}).sort({"ipo.valuation_amount": 1})
    ```

    **Only in mongo shell**...When there are many documents, the memory overflows when doing the `sort` causing an error. The solution is to create an `Index` before executing the query.
___

10. Retrieve the 10 companies with more employees, order by the `number of employees`:

    **COMPASS**

    ```COMPASS
    SORT: { number_of_employees: -1 }
    LIMIT: 10
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({}).sort({number_of_employees: -1}).limit(10)
    ```
___

11. All the companies founded on the second semester of the year. Limit your search to 1000 companies:

    **COMPASS**

    ```COMPASS
    FILTER: { founded_month: { $gt: 5 } }
    LIMIT: 1000
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({founded_month: { $gt: 5 }}).limit(1000)
    ```
___

12. All the companies founded before 2000 that have and acquisition amount of more than 10.000.000:

    **COMPASS**

    ```COMPASS
    FILTER: { founded_year: { $lt: 2000 }, "acquisition.price_amount": { $gt: 10000000 } }
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({founded_year: {$lt: 2000}, "acquisition.price_amount": { $gt: 10000000}})
    ```
___

13. All the companies that have been acquired after 2015, order by the acquisition amount, and retrieve only their `name` and `acquisiton` field:

    Spoiler: there are no records...

    **COMPASS**

    ```COMPASS
    FILTER: { "acquisition.acquired_year": { $gt: 2015 } }
    PROJECT: { name: 1, acquisition: 1}
    SORT: { "acquisition.price_amount": 1 }
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({"acquisition.acquired_year": {$gt: 2015}}).sort({"acquisition.price_amount": 1}).projection({name: 1, acquisition: 1})
    ```

    **Playing a little with the thirteen query:**

    13.1 All the companies that have been acquired after **2013**, order by the acquisition amount, **but also that the acquisition price is not null**. Retrieve only their name and acquisition field:

    `$ne` selects the documents where the value of the field is not equal to the specified value. This includes documents that do not contain the field.

    `$and` performs a logical AND operation on an array of two or more expressions (e.g. `expression1`, `expression2`, etc.) and selects the documents that satisfy all the expressions in the array. The `$and` operator uses short-circuit evaluation. If the first expression (e.g. `expression1`) evaluates to false, MongoDB will not evaluate the remaining expressions.

    **COMPASS**

    ```COMPASS
    FILTER: { $and: [ {"acquisition.acquired_year": { $gt: 2013 } }, {"acquisition.price_amount": { $ne: null} } ] }
    PROJECT: { name: 1, acquisition: 1}
    SORT: { "acquisition.price_amount": 1 }
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({ $and: [{"acquisition.acquired_year": { $gt: 2013 }}, {"acquisition.price_amount": { $ne: null}} ]}).sort({"acquisition.price_amount": 1}).projection({name: 1, acquisition: 1})
    ```
___


14. Order the companies by their `founded year`, retrieving only their `name` and `founded year`:

    **COMPASS**

    ```COMPASS
    FILTER: { founded_year: { $ne: null } } // Only if you want to skip the nulls
    PROJECT: { name: 1, founded_year: 1 }
    SORT: { founded_year: 1 }
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').createIndex({founded_year: 1}) // to avoid memory overflow
    db.getCollection('companies').find({founded_year: { $ne: null }}).sort({founded_year: 1}).projection({name: 1, founded_year: 1})
    ```
___

15. All the companies that have been founded on the first seven days of the month, including the seventh. Sort them by their `aquisition price` descendently. Limit the search to 10 documents:

    **COMPASS**

    ```COMPASS
    FILTER: { founded_day: { $lte: 7} }
    SORT: { "acquisition.price_amount": -1 }
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').createIndex({"acquisition.price_amount": -1}) // to avoid memory overflow
    db.getCollection('companies').find({founded_day: { $lte: 7}}).sort({"acquisition.price_amount": -1}).limit(10)
    ```
___

16. All the companies on the 'web' `category` that have more than 4000 employees. Sort them by the amount of employees in ascendant order:

    `$regex` provides regular expression capabilities for pattern matching strings in queries. See options [here](https://docs.mongodb.com/manual/reference/operator/query/regex/#op._S_options)

    **COMPASS**

    ```COMPASS
    FILTER: { category_code: { $regex: 'web', $options: 'i' }, number_of_employees: { $gt: 4000 } }
    // $regex it is optional if you are sure that the field is normalized
    SORT: { number_of_employees: 1 }
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').createIndex({number_of_employees: 1}) // to avoid memory overflow
    db.getCollection('companies').find({category_code: {$regex: 'web', $options: 'i'}, number_of_employees: {$gt: 4000}}).sort({number_of_employees: 1})
    ```
___

17. All the companies which their acquisition amount is more than 10.000.000, and currency are 'EUR':

    **COMPASS**

    ```COMPASS
    FILTER: { "acquisition.price_amount": {$gt: 10000000}, "acquisition.price_currency_code": 'EUR' }

    or

    FILTER: { $and: [ {"acquisition.price_amount": {$gt: 10000000}}, {"acquisition.price_currency_code": 'EUR'} ]}
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({"acquisition.price_amount": {$gt: 10000000}, "acquisition.price_currency_code": 'EUR'})
    ```
___

18. All the companies that have been acquired on the first trimester of the year. Limit the search to 10 companies, and retrieve only their `name` and `acquisition` fields:

    **COMPASS**

    ```COMPASS
    FILTER: { "acquisition.acquired_month": { $lte: 3 } }
    PROJECT: { name: 1, acquisition: 1 }
    LIMIT: 10
    ```

    **MONGO SHELL**

    ```MONGO SHELL
    db.getCollection('companies').find({"acquisition.acquired_month": {$lte: 3}}).projection({name: 1, acquisition: 1}).limit(10)
    ```
___

19. All the companies that have been founded between 2000 and 2010, but have not been acquired before 2011.


Happy Coding! :heart: