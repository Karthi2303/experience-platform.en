---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Manage data usage labels using APIs 
topic: developer guide
---

# Manage data usage labels using APIs

This document provides steps on how to manage data usage labels at the dataset- and field-level using the Catalog Service API.

## Getting started

Before you read this guide, it is recommended that you read the [Catalog Service overview](../../catalog/home.md) for a more robust introduction to the service. In addition, you must also follow the steps outlined in the [getting started section](../../catalog/api/getting-started.md) in the Catalog developer guide to gather the required credentials to make calls to the Catalog API.

In order to make calls to the endpoints outlined in the sections below, you must have the unique `id` value for a specific dataset. If you do not have this value, see the developer guide section on [listing Catalog objects](../../catalog/api/list-objects.md) to find the IDs of your existing datasets.

## Look up labels for a dataset {#lookup}

You can look up the data usage labels that have been applied to an existing dataset by making a GET request.

**API format**

```http
GET /dataSets/{DATASET_ID}/labels
```

| Parameter | Description |
| --- | --- |
| `{DATASET_ID}` | The unique `id` value of the dataset whose labels you want to look up. |

**Request**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the data usage labels that have been applied to the dataset.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{IMS_ORG}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| Property | Description |
| --- | --- |
| `labels` | A list of data usage labels that have been applied to the dataset. |
| `optionalLabels` | A list of individual fields within the dataset that have data usage labels applied to them. |

## Apply labels to a dataset

You can create a set of labels for a dataset by providing them in the payload of a POST or PUT request. Using either of these methods overwrites any existing labels and replaces them with those provided in the payload.

**API format**

```http
POST /dataSets/{DATASET_ID}/labels
PUT /dataSets/{DATASET_ID}/labels
```

| Parameter | Description |
| --- | --- |
| `{DATASET_ID}` | The unique `id` value of the dataset that you are creating labels for. |

**Request**

The following POST request adds a series of labels to the dataset, as well as a specific field within that dataset. The fields provided in the payload are the same as would be required for a PUT request.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
  "labels": [ "C1", "C2", "C3", "I1", "I2" ],
  "optionalLabels": [
    {
      "option": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
        "contentType": "application/vnd.adobe.xed-full+json;version=1",
        "schemaPath": "/properties/repositoryCreatedBy"
      },
      "labels": [ "S1", "S2" ]
    }
  ]
}'
```

| Property | Description |
| --- | --- |
| `labels` | A list of data usage labels that you want to add to the dataset. |
| `optionalLabels` | A list of any individual fields within the dataset that you want to add labels to. Each item in this array must have the following properties: <br/><br/>`option`: An object that contains the Experience Data Model (XDM) attributes of the field. The following three properties are required:<ul><li><code>id</code>: The URI <code>$id</code> value of the schema associated with the field.</li><li><code>contentType</code>: The content type and version number of the schema. This should take the form of one of the valid <a href="../../xdm/api/look-up-resource.md">Accept headers</a> for an XDM lookup request.</li><li><code>schemaPath</code>: The path to the field within the dataset's schema.</li></ul>`labels`: A list of data usage labels that you want to add to the field. |

**Response**

A successful response returns the labels that have been added to the dataset.

```json
{
  "labels": [ "C1", "C2", "C3", "I1", "I2" ],
  "optionalLabels": [
    {
      "option": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
        "contentType": "application/vnd.adobe.xed-full+json;version=1",
        "schemaPath": "/properties/repositoryCreatedBy"
      },
      "labels": [ "S1", "S2" ]
    }
  ]
}
```

## Delete labels for a dataset

You can delete the labels applied to a dataset by making a DELETE request.

**API format**

```http
DELETE /dataSets/{DATASET_ID}/labels
```

| Parameter | Description |
| --- | --- |
| `{DATASET_ID}` | The unique `id` value of the dataset whose labels you want to delete. |

**Request**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response HTTP status 200 (OK), indicating that the labels have been deleted. You can [look up the existing labels](#lookup) for the dataset in a separate call to confirm this.

## Next steps

Now that you have added data usage labels at the dataset- and field-level, you can begin to ingest data into Experience Platform. To learn more, start by reading the [data ingestion documentation](../../ingestion/home.md).

You can also now define data usage policies based on the labels you have applied. For more information, see the [data usage policies overview](../policies/overview.md).