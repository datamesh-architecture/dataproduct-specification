# Data Product Specification

The Data Product Specification is an open initiative to define a common data product format.
It can be used on its own, or in combination with the [Data Contract Specification](https://datacontract.com).

A [data product](https://www.datamesh-manager.com/learn/what-is-a-data-product) is a logical unit that contains all components to process domain data and provide data sets via output ports for analytical use.

Version
---

0.0.1

Example
---

```yaml
dataProductSpecification: 0.0.1
id: shelf_warmers
info:
  title: Shelf Warmers
  description: Calculated shelfwarmers. Read about calculation in docs.
  status: active
  archetype: consumer-aligned
  maturity: managed
  owner: fulfillment
inputPorts: []
outputPorts:
  - id: glue_catalog_database_shelf_warmers_v1
    name: 'Glue Catalog Database: Shelf Warmers (v1)'
    description: All Shelf Warmers represented as a Glue Catalog table
    dataContract: shelf_warmers_v1
    type: Glue
    status: active
    location: arn:aws:glue:eu-central-1:528115139298:table/fulfillment-shelf-warmers/shelf_warmers
    containsPii: false
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
links:
  Discovery: https://qbffyn0bze.execute-api.eu-central-1.amazonaws.com/prod
  Documentation: http://example.com/datamesh/fulfillment/shelf_warmers
custom:
  platform: aws
tags:
  - athena
  - glue
  - s3
```

Specification
---
We currently offer the Specification in form of a JSON Schema [dataproduct.schema.json](https://dataproduct-specification.com/dataproduct.schema.json).

Roadmap
---
- Support for specifing internals such as the pipelines

Template
---
We're currently working on providing a template to help you fill out the data product specification. Stay tuned!

Tooling
---
- VS Code: name your file `dataproduct.yaml` and you get code completion within your editor.
- [Data Mesh Manager](https://www.datamesh-manager.com/) supports the data product specification and allows the user to import or export data products using this specification.

License
---
[MIT License](LICENSE)
