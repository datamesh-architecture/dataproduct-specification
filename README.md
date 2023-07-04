# Data Product Specification

The Data Product Specification is an open initiative to define a common data product format for further automation and quality testing.


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
    links:
      Athena Query Editor: https://eu-central-1.console.aws.amazon.com/athena/home?region=eu-central-1#/query-editor
      Glue Table: https://eu-central-1.console.aws.amazon.com/glue/home?region=eu-central-1#/v2/data-catalog/tables/view/fulfillment_shelf_warmers?database=fulfillment-shelf-warmers&catalogId=528115139298
    custom:
      platform: aws
    containsPii: false
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

Tooling
---
- [Data Mesh Manager](https://www.datamesh-manager.com/) supports the data product specification and allows the user to import or export data products using this specification.

License
---
[MIT License](LICENSE)
