---
layout: page
title: API Guide
permalink: /api-guide/
---
*The following is excerpt from an API guide (including sample code) that I wrote for an example REST API.*

## Introduction
Spooky is a cloud-based wildlife imagery platform that uses satellites to capture images over specified locations. It includes a REST API that enables you to integrate the platform capabilities into your own applications.

## Using the API

### Authentication
All operations require an API key in the request header. If an API Key is not provided, you will get a `401 -- Not Authorized` HTTP response code. If the API key is valid, but you do not have the right permissions, you will get a `403 -- Forbidden` HTTP response code.

### Get your API Key
To request an API key, contact [Support](support@spooky-salamander.com).

After getting your API key, you can verify your authentication by sending a request to one of the API endpoints. The following is an example Python script that sends a GET request to the `sites` endpoint and prints the response code. 

```python
import requests

headers = {"Authorization": "<YOUR_API_KEY>"}

response = requests.get(https://api.spooky.com/sites, headers=headers)
if response.status_code == 200
    print("Authorized")
else:
    print("Request Failed: ", response.status_code)
```

### Pagination
The API uses cursor-based pagination that returns an opaque `nextToken` at the end of a response to enable continued operations from the last request. If the response does not include more results, the `nextToken` will be *null*. Additionally, you can control the number of results by specifying the `limit` in your request.

For example: `https://api.spooky.com/products?nextToken=MyNextToken&limit=100`.

### Filtering
To filter responses to include only those objects you're interested in, you can specify one or more response parameters in your request.

For example: `https://api.spooky.com/search?=EXPIRED`.


### Sorting

You can sort the response objects by using the `sort` parameter in your request. Depending on your parameter, you can sort in ascending order using `sort=<parameter>` or in descending order using `sort=-<parameter>`.

For example: `https://api.spooky.com/task?status?sort=-timestamp`.

## Learn the basics
Before you start using the API, you should understand the core components of the ordering workflow and other operations you can perform.

### Offerings
Offerings are the tasking tiers (Cheetah, Wolf, Sloth) that are available in your Spooky subscription. When placing an [order](link) for an image, you specify the offering that you want to use for the request. Each offering has a unique identifier (`id`) that must be specified when submitting a new order.

To see the offerings available in your subscription, send a GET request to the [offerings](link) endpoint. The response will include a list of the available offerings (`sku`) and associated `id` that you will save and use in a new order request.

The following is an example Python script that returns the `id` of a specific offering `sku` that you save to use in subsequent calls.

**Get Offerings - Python Example**

```python
import requests
import json

headers = {"Authorization": "<YOUR_API_KEY>"}
url = "https://api.spooky.com/offerings"
sku = "Wolf"

def get_sku (url, headers):
    response = requests.get(url, headers=headers)
    sku_data = json.loads(response.content.decode("utf-8"))["data"]
    for off in sku_data:
        sku_name = off.get("sku")
        sku_id = off.get("id")
        if sku_name == sku:
            return sku_id
        
get_sku (url, headers)
```

#### Offering parameters 
Offering parameters are the options you specify when sending an order request for a new image. For example, you can specify the maximum cloud coverage, sun elevation, and analytics of your order.

To see the offering parameters available for each offering, send a GET request to the [offerings/SKU_ID/parameters](link) endpoint. The response will include a list of each parameter's `fieldName` and other metadata that are available based on your subscription.

The following is a Python script that builds upon the previous **Get Offerings – Python Example**. Using the `sku_id`, the request gets all parameters available for a given offering (e.g., Wolf) and prints a list of the relevant information that you will use when in an order request, including the `fieldName`, `datatype` and the `minValue`, `maxValue`, and `default` value if applicable.

**Get Offering Parameters - Python Example**

```python
import requests
import json

headers = {"Authorization": "<YOUR_API_KEY>"}
url = "https://api.spooky.com/offerings"
sku = "Wolf"

def get_sku (url, headers):
    response = requests.get(url, headers=headers)
    sku_data = json.loads(response.content.decode("utf-8"))["data"]
    for off in sku_data:
        sku_name = off.get("sku")
        sku_id = off.get("id")
        if sku_name == sku:
            return sku_id
        
    except requests.RequestException as e:
        print(f"Error fetching data: {e}")
        return None

def get_parameters(sku_id):
    if sku_id is None:
        print("Invalid SKU ID. Cannot fetch parameters.")
        return

    parameters_url = url + f"/{sku_id}/parameters"
    try:
        response = requests.get(parameters_url, headers=headers)
        parameters_data = json.loads(response.content.decode("utf-8"))["data"]
        for param in parameters_data:
            field = param.get("fieldName")
            dataType = param.get("dataType")
            minValue = param.get("minValue")
            maxValue = param.get("maxValue")
            default = param.get("default")
            if maxValue is not None:
                print(f"{field} | {dataType} | Max:{maxValue} | Min: {minValue} | Default: {default}")
            else:
                print(f"{field} | {dataType}")
    except requests.RequestException as e:
        print(f"Error fetching parameters: {e}")

sku_id = get_sku_and_id()
get_parameters(sku_id)

```
**Example Output**

```
productType | string
maxCloudPercent | integer | Max: 100 | Min: 30 | Default: None
sunElevation | [integer] | Max:[90, 90] | Min: [-4, -4] | Default: None
mammal_detection | boolean
motion_detection | boolean
building_detection | boolean
```
To specify the offering parameters in an order request, you add the `offeringParamValues` object to your request and populate it with the specific options as shown in the following example:

```json
{
    "offeringParameters": {
        "sunElevation": [
            10,
            60
        ],
        "maxCloudPercent": 50,
        "mammal_detection": true
    }
}
```
The following table shows all of the offering parameters. Depending on your subscription, some of the parameters are not avialable.

<table>
  <tr>
    <th>Field</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
    <tr>
    <td><code>productType</code></td>
    <td><code>string</code></td>
    <td>The imagery product that you want to collect.
        <ul>
            <li><i>STANDARD - </i>Single image scene collected in daylight.</li>
            <li><i>AREA - </i>Multiple images collected over an area larger that a single image scene.</li>
            <li><i>BURST - </i>Multiple images collected in rapid sequence for motion analysis.</li>
        </ul>
    </td>
</tr>
    <tr>
    <td><code>maxCloudPercent</code></td>
    <td><code>integer</code></td>
    <td>The maximum cloud cover percentage over an area allowed to capture image.
        <ul>
            <li>Default: <i>30</i></li>
            <li>Min: <i>30</i></li>
            <li>Max: <i>100</i></li>
        </ul>
    </td>
</tr>
    <tr>
    <td><code>sunElevation</code></td>
    <td><code>[integer]</code></td>
    <td>The angle between the target ground plane and sun.
        <ul>
            <li>Default: <i>[10,90]</i></li>
            <li>Min: <i>[-4,-4]</i></li>
            <li>Max: <i>[90,90]</i></li>
        </ul>
    </td>
</tr>
    <tr>
    <td><code>mammal_detection</code></td>
    <td><code>boolean</code></td>
    <td>Enable analytics to detect mammals.</td>
    <tr>
    <td><code>motion_detection</code></td>
    <td><code>boolean</code></td>
    <td>Enable analytics to detect motion (availabe if <code>productType=<i>BURST</i></code>)</td>
</tr>
    <tr>
    <td><code>building_detection</code></td>
    <td><code>boolean</code></td>
    <td>Enable analytics to detect buildings.</td>
    <tr>
</tr>
