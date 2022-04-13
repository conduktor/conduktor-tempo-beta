# Accessing the context in custom inputs

Depending on where you are in the application, the _Field Selection (Json Query)_ and the _Javascript_ fields will let you access different properties. 

_Mustache_ lets you access some of these properties through an UI and build String or Json templates.

_Plain_ is a standard field. The value is not interpreted


For the technical capabilities of _Field Selection (Json Query)_, you can refer to [this link](https://stedolan.github.io/jq/manual/#Basicfilters)


For the Javascript syntax, we'll add documentation as soon as possible.



## Variables and environments

You can always access the _Environment Variables_ (defined in the Environment screen, requiring to have a defined environment during execution) and the _Local Variables_ (defined inside the scenario through the Variables task). The Mustache custom input also lets you access theses through the UI.

| Attribute        | Type           | How to access: Field selection (JQ)  | How to access: Javascript |
| ------------- |-------------  | ----- | ----- |
| Environment Variables      | Map | .env | context.env |
| "myTopic" env var     | String | .env.myTopic | context.env.myTopic |
| Local Variables      | Map | .variables | context.variables |
| "myValue" local var      | Unknown | .variables.myValue | context.variables.myValue |



___
## Checks

In a Check, you can access the record metadata in Produce and Consume tasks, and record data in Consume task

### Metadata
---

To access the metadata, you can use : 


| Attribute        | Type           | How to access: Field selection (JQ)  | How to access: Javascript |
| ------------- |-------------  | ----- | ----- |
| Offset      | Number | .record.offset | context.record.offset |
| Partition     | Number | .record.partition | context.record.partition |
| Timestamp     | Timestamp | .record.timestamp | context.record.timestamp |
| Topic      | String | .record.topic | context.record.topic |


### Record data
---

In Consumer checks, you can also access record data

| Attribute        | Type           | How to access: Field selection (JQ)  | How to access: Javascript |
| ------------- |-------------  | ----- | ----- |
| Key      | Unknown | .record.key | context.record.key |
| Value     | Unknown | .record.value | context.record.value |
| Headers      | List | .record.headers | context.record.headers |

If the key and/or value can be read as Json (Json, Avro, Protobuf), you can also access specific nested properties inside. For example if your record value is 

```json
{
    "id": "abc-123",
    "value": 1000
}

```
you can access the "id" property using : 
- in JQ : `.record.value.id`
- in Javascript : `context.record.value.id`


___

## Advanced : Accessing data from previous tasks

You can access the data of the event having triggered the current task using the `triggeredBy` property.

For example if you have a Consume task, and a Variables task chained on the _On Record_ port of the consumer, you can access the record key by using : 
- JQ: `.triggeredBy[0].record.key`
- Javascript: `context.triggeredBy[0].record.key`

If you have more than one origin for a task, you can use JQ or Javascript advanced filtering options to pick the right one. We'll write more documentation on that soon (and we'll try to simplify this part)
