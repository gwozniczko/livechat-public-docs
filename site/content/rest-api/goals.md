---
weight: 60
---

# Goals

This method allows you to **get information** about your [Goals](https://www.livechatinc.com/kb/goals-set-up-and-use/) and to **modify** them.

## Available paths {#goals-available-paths}

| Methods      | Path      |
|--------------|-----------|
| `GET`, `POST` | `/goals` |
| `GET`, `PUT`, `DELETE` | `/goals/<GOAL_ID>` |
| `POST` | `/goals/<GOAL_ID>/mark_as_successful` |

## List all goals

> Path

```
GET https://api.livechatinc.com/goals
```

> Sample request

```shell
curl "https://api.livechatinc.com/goals" \
  -u john.doe@mycompany.com:c14b85863755158d7aa5cc4ba17f61cb \
  -H X-API-Version:2
```

> Sample response

```json
[
  {
    "id": 1041,
    "name": "purchase",
    "active": 1,
    "type": "url"
  },
  {
    "id": 1181,
    "name": "nike shoes variable",
    "active": 1,
    "type": "custom_variable"
  }
]
```

Returns all currently set goals. The `active` parameter indicates whether a goal is enabled or not.

#### Optional parameters

| Parameter | Description |
|---------|--------------------|
| `type` | type of the goal: `custom_variable`, `url`, `api` or `sales_tracker` |

## Get a single goal details

> Path

```
GET https://api.livechatinc.com/goals/<GOAL_ID>
```

> Sample request

```shell
curl "https://api.livechatinc.com/goals/1181" \
  -u john.doe@mycompany.com:c14b85863755158d7aa5cc4ba17f61cb \
  -H X-API-Version:2
```

> Sample response

```json
{
  "id": 1181,
  "name": "nike shoes variable",
  "active": 1,
  "type": "custom_variable",
  "custom_variable_name": "nike_shoes",
  "custom_variable_value": "true"
}
```

Returns the goal details for the given `GOAL_ID`.

#### Attributes

| Attribute | Description |
|---------|--------------------|
| `id` | id of the goal |
| `name` | goal name |
| `active` | whether or not the goal is enabled |
| `type` | type of the goal |

#### Additional info

The `type` attribute can take the following values:

*   `custom_variable` – with two additional parameters: `custom_variable_name`, `custom_variable_value`.
*   `url` – with two additional parameters: `url` and `match_type` with possible values: `substring` (default), `exact`.
*   `api` – with no additional parameters.
*   `sales_tracker` – with seven additional parameters: `sales_tracker_id`, `value_type`, `value`, `currency`, `time_range`, `order_field_name` and `value_field_name`

## Mark a goal as successful

> Path

```
POST https://api.livechatinc.com/goals/<GOAL_ID>/mark_as_successful
```

> Sample request

```shell
curl "https://api.livechatinc.com/goals/1181/mark_as_successful" \
  -u john.doe@mycompany.com:c14b85863755158d7aa5cc4ba17f61cb \
  -H X-API-Version:2 \
  -d "visitor_id=S1281361958.2238ee3bd3"
```

> Sample JSON request

```shell
curl "https://api.livechatinc.com/goals/1181/mark_as_successful" \
  -u john.doe@mycompany.com:c14b85863755158d7aa5cc4ba17f61cb \
  -H X-API-Version:2 \
  -H Content-type:application/json \
  -d '{
        "visitor_id":"S1281361958.2238ee3bd3",
     }'
```

> Sample response

```json
{
  "result": "goal marked as successful"
}
```


The `GOAL_ID` is obtained from the [goals list](#list-all-goals).

#### Required parameters

| Parameter | Description |
|---------|--------------------|
| `visitor_id` | obtained using the JavaScript API: [LC_API.get_visitor_id()](//developers.livechatinc.com/javascript-api#get-visitor-id) |

Optionally you can store additional information about the goal. They can be only retrieved using the API.

#### Optional parameters

| Parameter | Example |
|---------|--------------------|
| `order_id` | `AP723HVCA721`|
| `order_description` | `Nike shoes` |
| `order_price` | `199.00`, only the period is allowed as a separation character |
| `order_currency` | `USD` |

## Add a new goal

> Path

```
POST https://api.livechatinc.com/goals
```

> Sample request

```shell
curl "https://api.livechatinc.com/goals" \
  -u john.doe@mycompany.com:c14b85863755158d7aa5cc4ba17f61cb \
  -H X-API-VERSION:2 \
  -d "name=new%20goal&\
  type=url&\
  url=http://www.mystore.com/checkout/thank_you&\
  match_type=exact"
```

> Sample JSON request

```shell
curl "https://api.livechatinc.com/goals" \
  -u john.doe@mycompany.com:c14b85863755158d7aa5cc4ba17f61cb \
  -H X-API-Version:2 \
  -H Content-type:application/json \
  -d '{
        "name":"new goal",
        "type":"url",
        "url":"http://www.mystore.com/checkout/thank_you",
        "match_type":"exact"
     }'
```

> Sample response

```json
{
  "id": 2231,
  "name": "new goal",
  "active": 1,
  "type": "url",
  "match_type": "exact",
  "url": "http://www.mystore.com/checkout/thank_you"
}
```

Creates a new goal.

#### Required parameters

| Parameter | Description |
|---------|--------------------|
| `name` | name of the goal |
| `type`| type of the goal |

#### Additional info

The `type` can take the following values:

*   `custom_variable` – with two additional parameters: `custom_variable_name`, `custom_variable_value`. Both are required.
*   `url` – with two additional parameters: `url` (required) and `match_type` (optional) with possible values: `substring` (default), `exact`.
*   `api` – with no additional parameters.
*   `sales_tracker` – with optional parameters: `value_type` (possible values: `set`, `not_set`, `dynamic`), `value`, `currency`, `time_range`, `order_field_name`, `value_field_name` and `sales_tracker_id`

The `active` parameter indicates whether the goal is active or not.

## Update a goal

> Path

```
PUT https://api.livechatinc.com/goals/<GOAL_ID>
```

> Sample request

```shell
curl "https://api.livechatinc.com/goals/2231" \
  -u john.doe@mycompany.com:c14b85863755158d7aa5cc4ba17f61cb \
  -H X-API-Version:2 \
  -X PUT -d "name=new%20goal%20paused&\
  active=0"
```

> Sample JSON request

```shell
curl "https://api.livechatinc.com/goals/2231" \
  -u john.doe@mycompany.com:c14b85863755158d7aa5cc4ba17f61cb \
  -H X-API-Version:2 \
  -H Content-type:application/json \
  -d '{
        "name":"new goal paused",
        "active":0
     }'
```

> Sample response

```json
{
  "id": 2231,
  "name": "new goal paused",
  "active": 0,
  "type": "url",
  "match_type": "exact",
  "url": "http://www.mystore.com/checkout/thank_you"
}
```

Updates the specified goal by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

The `GOAL_ID` is obtained from the [goals list](#list-all-goals).

#### Optional parameters

| Parameter | Description |
|---------|--------------------|
| `name` | name of the goal |
| `type`| type of the goal |
| `active` | active state of the goal |

#### Additional info

The `type` can take the following values:

*   `custom_variable` – with two additional parameters: `custom_variable_name`, `custom_variable_value`. Both are required.
*   `url` – with two additional parameters: `url` (required) and `match_type` (optional) with possible values: `substring` (default), `exact`.
*   `api` – with no additional parameters.
*   `sales_tracker` – with optional parameters: `order_field_name`, `value_field_name` and `sales_tracker_id`

The `active` parameter indicates whether the goal is active or not.

## Remove a goal

> Path

```
DELETE https://api.livechatinc.com/goals/<GOAL_ID>
```

> Sample request

```shell
curl "https://api.livechatinc.com/goals/2231" \
  -u john.doe@mycompany.com:c14b85863755158d7aa5cc4ba17f61cb \
  -H X-API-Version:2 \
  -X DELETE
```

> Sample response

```json
{
  "result": "goal removed successfully"
}
```

Removes a goal with the given `GOAL_ID`.
