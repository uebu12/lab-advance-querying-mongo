![Ironhack Logo](https://i.imgur.com/1QgrNNw.png)

# Answers

### 1. All the companies whose name match 'Babelgum'. Retrieve only their `name` field.

```shell
db.companies.find(
{name: 'Babelgum'},
{name: 1,\_id: 0}
)
```

### 2. All the companies that have more than 5000 employees. Limit the search to 20 companies and sort them by **number of employees**.

```shell
db.companies
  .find({ number_of_employees: { $gt: 5000 } })
  .sort({ number_of_employees: 1 })
  .limit(20);
```

### 3. All the companies founded between 2000 and 2005, both years included. Retrieve only the `name` and `founded_year` fields.

```shell
db.companies.find(
{founded_year: {$gte: 2000,$lte: 2005}},
{name: 1,founded_year: 1,\_id: 0}
)
```

### 4. All the companies that had a Valuation Amount of more than 100.000.000 and have been founded before 2010. Retrieve only the `name` and `ipo` fields.

```shell
db.companies.find(
{$and: [{ 'ipo.valuation_amount': { $gt: 100000000 }},{ founded_year: { $lt: 2010 }}]},
{name: 1,ipo: 1,\_id: 0}
)
```

### 5. All the companies that have less than 1000 employees and have been founded before 2005. Order them by the number of employees and limit the search to 10 companies.

```shell
db.companies
  .find({
    $and: [
      { number_of_employees: { $lt: 1000 } },
      { founded_year: { $lt: 2005 } },
    ],
  })
  .sort({ number_of_employees: 1 })
  .limit(10);
```

### 6. All the companies that don't include the `partners` field.

```shell
db.companies.find({ partners: { $size: 0 } });
```

### 7. All the companies that have a null type of value on the `category_code` field.

```shell
db.companies.find({ category_code: { $type: 10 } });
```

### 8. All the companies that have at least 100 employees but less than 1000. Retrieve only the `name` and `number of employees` fields.

```shell
db.companies.find(
{number_of_employees: {$gte: 100,$lt: 1000}},
{number_of_employees: 1,name: 1,\_id: 0}
)
```

### 9. Order all the companies by their IPO price in a descending order.

```shell
db.companies.find({ ipo: { $type: 3 } }).sort({ "ipo.valuation_amount": -1 });
```

### 10. Retrieve the 10 companies with most employees, order by the `number of employees`

```shell
db.companies.find(undefined).sort({ number_of_employees: -1 }).limit(10);
```

### 11. All the companies founded on the second semester of the year. Limit your search to 1000 companies.

```shell
db.companies.find({ founded_month: { $gt: 6 } }).limit(1000);
```

### 12. All the companies founded before 2000 that have an acquisition amount of more than 10.000.000

```shell
db.companies.find({
  $and: [
    { founded_year: { $lt: 2000 } },
    { "acquisitions.price_amount": { $gt: 10000000 } },
  ],
});
```

### 13. All the companies that have been acquired after 2010, order by the acquisition amount, and retrieve only their `name` and `acquisition` field.

```shell
db.companies.find(
{'acquisition.acquired_year': {$gt: 2010}},
{name: 1,acquisition: 1,\_id: 0}
).sort({ 'acquisition.price_amount': 1})
```

### 14. Order the companies by their `founded year`, retrieving only their `name` and `founded year`.

```shell
db.companies.find(
undefined,
{name: 1,founded_year: 1,\_id: 0}
).sort({founded_year: 1})
```

### 15. All the companies that have been founded on the first seven days of the month, including the seventh. Sort them by their `acquisition price` in a descending order. Limit the search to 10 documents.

```shell
db.companies
  .find({ founded_day: { $gte: 1, $lte: 7 } })
  .sort({ "acquisition.price_amount": -1 })
  .limit(10);
```

### 16. All the companies on the 'web' `category` that have more than 4000 employees. Sort them by the amount of employees in ascending order.

```shell
db.companies
  .find({
    $and: [{ category_code: "web" }, { number_of_employees: { $gt: 4000 } }],
  })
  .sort({ number_of_employees: -1 });
```

### 17. All the companies whose acquisition amount is more than 10.000.000, and currency is 'EUR'.

```shell
db.companies.find({
  $and: [
    { "acquisition.price_amount": { $gt: 10000000 } },
    { "acquisition.price_currency_code": "EUR" },
  ],
});
```

### 18. All the companies that have been acquired on the first trimester of the year. Limit the search to 10 companies, and retrieve only their `name` and `acquisition` fields.

```shell
db.companies
  .find(
    { $and: [{ "acquisition.acquired_month": { $gte: 1, $lte: 3 } }] },
    { name: 1, acquisition: 1, _id: 0 }
  )
  .limit(10);
```

### 19. All the companies that have been founded between 2000 and 2010, but have not been acquired before 2011.

```shell
db.companies.find({
  $and: [
    { founded_year: { $gt: 2000, $lt: 2010 } },
    { "acquisition.acquired_year": { $gte: 2011 } },
  ],
});
```
