# Data Product Specification

The Data Product Specification is an open initiative to define a common data product format.
It can be used on its own, or in combination with the [Data Contract Specification](https://datacontract-specification.com).

A [data product](https://www.datamesh-manager.com/learn/what-is-a-data-product) is a logical unit that contains all components to process domain data and provide data sets via output ports for analytical use.

Version
---

0.0.1

Example
---

```yaml
dataProductSpecification: 0.0.1
info:
  id: shelf_warmers
  name: Shelf Warmers
  description: Calculated shelfwarmers. Read about calculation in docs.
  status: active
  archetype: consumer-aligned
  maturity: managed
owner:
  teamId: fulfillment
links:
  Discovery: https://qbffyn0bze.execute-api.eu-central-1.amazonaws.com/prod
  Documentation: http://example.com/datamesh/fulfillment/shelf_warmers
custom:
  platform: aws
tags:
  - athena
  - glue
  - s3
inputPorts: []
outputPorts:
  - id: glue_catalog_database_shelf_warmers_v1
    name: 'Glue Catalog Database: Shelf Warmers (v1)'
    description: All Shelf Warmers represented as a Glue Catalog table
    type: Glue
    status: active
    location: arn:aws:glue:eu-central-1:528115139298:table/fulfillment-shelf-warmers/shelf_warmers
    containsPii: false
    terms:
      usage: Max queries per minute: 10, Max data processing per day: 1 TiB
      limitations: Not in realtime. Do not use for operational inventory cleaning.
      billing: "$1000 / month"
    schema:
      type: dbt
      specification:
        version: 2
        description:
        models:
          - name: orders
            description: >
              One record per order. Includes cancelled and deleted orders.
            columns:
              - name: order_id
                type: string
                description: Primary key of the orders table
                tests:
                  - unique
                  - not_null
              - name: order_timestamp
                type: timestamptz
                description: The business timestamp in UTC when the order was successfully registered in the source system and the payment was successful.
                tests:
                  - not_null
          - name: line_items
            description: >
              The items that are part of an order
            columns:
              - name: lines_item_id
                type: string
                description: Primary key of the lines_item_id table
              - name: order_id`
                type: string
                description: Foreign key to the orders table
    links:
      Athena Query Editor: https://eu-central-1.console.aws.amazon.com/athena/home?region=eu-central-1#/query-editor
      Glue Table: https://eu-central-1.console.aws.amazon.com/glue/home?region=eu-central-1#/v2/data-catalog/tables/view/fulfillment_shelf_warmers?database=fulfillment-shelf-warmers&catalogId=528115139298
    custom:
      platform: aws
    tags:
      - glue
      - athena
  - id: s3_bucket_shelf_warmers_v1
    name: 'S3 Bucket: Shelf Warmers (v1)'
    description: All Shelf Warmers represented as a Glue Catalog table
    type: S3
    status: active
    location: arn:aws:s3:::fulfillment-shelf-warmers
    links:
      s3: https://console.aws.amazon.com/s3/buckets/fulfillment-shelf-warmers?region=eu-central-1&prefix=output/data/
    custom:
      platform: aws
    containsPii: false
    tags:
      - s3
```

Template
---
We're currently working on providing a template to help you fill out the data product specification. Stay tuned!

Tooling
---
- [Data Mesh Manager](https://www.datamesh-manager.com/) supports the data product specification and allows the user to import or export data products using this specification.

License
---
[MIT License](LICENSE)
