# Xef Reports
## Authentication

```shell 
curl --header "tenant: {myaccount}" \
     --header "authorization: Bearer {token}" \
     --header 'client-token: {client-token}' \
https://revoxef.works/api/external/v3
```

Base endpoint

`https://revoxef.works/api/external/v3`

You should send the headers `tenant` with your account username and `authorization` with the token created at `account > tokens`

> Get your token at [https://revoxef.works/account/tokens](https://revoxef.works/account/tokens)

## Request

```shell
curl --header "tenant: {myaccount}" --header "authorization: Bearer {token}" \ --header 'client-token: {client-token}' \
https://revoxef.works/api/external/v3/reports/{reportName}?start_date=2018-01-01&end_date=2018-01-29
```

`GET reports/{reportName}`

Field        | Type       | Description
-------------|------------|---------------------------
`start_date` | YYYY-mm-dd | The initial date for the report
`end_date`   | YYYY-mm-dd | The final date for the report


### Response

```shell
{
    "current_page": 1,
    "data": {"HERE WILL GO THE SPECIFIC REPORT DATA"},
    "from": 1,
    "last_page": 4,
    "next_page_url": "https://revoxef.works/api/external/v2/reports/{reportName}?page=2",
    "path": "https://revoxef.works/api/external/v2/reports/{reportName}",
    "per_page": 50,
    "prev_page_url": null,
    "to": 50,
    "total": 190
}
```

All responses will have this header

## Available reports
Here is a list of all available reports

* actionLog
* categories
* contentDiscounts
* cookDurations
* customers
* discounts
* groupedInvoices
* hours
* channels
* invoices
* menuProducts
* menus
* openOrders
* orderContents
* orders
* payments
* presences
* products
* rooms
* receipts
* stocks
* stockMovements
* inventoryContents
* taxes
* turns
* tenantUsers
* warehouses
* allProducts
* canceledContents
* canceledOrders



### Filters

Filter        | Type       | Description
--------------|------------|-------------
`start_date`  | YYYY-mm-dd | (required) The initial date for the report
`end_date`    | YYYY-mm-dd | (required) The final date for the report
`start_time`  | HH:mm      | The start time for the report
`end_time`    | HH:mm      | The end time for the report
`room`        | int        | Room id
`dayofweek`   | int        | Where Sunday is 1 and Saturday is 7
`priceRate`   | int        | Price rate id
`withContents`|            | Append contents 
`withItem `   |            | Append item details
`withInvoices`|            | Append invoices

<aside class="notice">
Take into account that not all filters are available for all reports. To exactly know which filters fits on each report is recommended to visit every report at [RevoXef](https://revoxef.works/reports/summary) and take a look at the url paramteres that appear when filtering.
</aside>

## Master
In case you have a master account you can create a token for the master account and use it to access all the chain reports as well as get a list of all the accounts within the master account

### Get Accounts

`GET https://revoxef.works/api/external/v2/accounts`

### Chain reports

`GET https://revoxef.works/api/external/v2/accounts/reports/{reportName}`

And you have to add a new header that defines the chain to connect to

Header        | Value          | Description
--------------|----------------|-----------
tenant        | account        | Master account name,
authorization | Bearer {token} | The [token](https://revoxef.works/account/tokens) created at backoffice
chain         | chain          |chain username returned in the accounts GET method

```
