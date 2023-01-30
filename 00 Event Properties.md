

## Real-time Example Primitive


![[ep_layers.png]]


![[ep_data_and_description_layer.png]]



## Real-time Example List





## Data Layer

Stored as a LinkedTreeMap:

A map of comparable keys to values. Unlike `TreeMap`, this class uses insertion order for iteration order. Comparison order is only used as an optimization for efficient insertion and removal.

```
key: s0::name
value: value
```

why s0::name?

![[ep_datalayer 1.png]]

## Time

Timestamp is always required → See Time in StreamPipes
is stored as Unix Timestamp.
What happens if YYY-MM-DD as data sourceo be converted internally to Unix timestamp?



## Description Layer

Event schema; describes each individual attributes of an event. The three most important and required fields are:

|       SP Class              | Attribute      | Type                    | Descibtion                                      |
| ------------------- | -------------- | ----------------------- | ----------------------------------------------- |
| Class EventProperty | runtimeName    | String                  | name of the attribute for unique identification |
|                     | runtimeType    | String                  | primitive data type of the attribute            |
| Class EventProperty | domainProperty | ArrayList < String URI> | semantic description of the attribute           |


-   **Runtime Name**. The runtime name indicates the key of the property at runtime, e.g., if our JSON message contains a structure such as `{"plateNumber" : "KA-F 123"}`, the runtime name must be `plateNumber`.

-   **Runtime Type**. An event property must have a primitive type (we will later see how to model more complex properties such as lists and nested properties). The type must be an instance of `XMLSchema` primitives, however, the SDK provides convenience methods to provide the property type.

-   **Domain Property**. The domain property indicates the semantics of the event property. For instance, the `latitude` property is linked to the `http://www.w3.org/2003/01/geo/wgs84_pos#lat` property of the WGS84 vocabulary. The domain property should be an URI as part of an existing or domain-specific vocabulary. The SDK provides convenience methods for ppopularvocabularies (e.g., Schema.org, Dolce or WGS84).


| SP Class            | Type                           | Type      | Descibtion |
| ------------------- | ------------------------------ | --------- | ---------- |
| Class EventProperty | label                          | String    |            |
| Class EventProperty | description                    | String    |            |
|                     | measurementUnit                | String    |            |
|                     | String valuesSpecitication     | String    |            |
| Class EventProperty | boolean required               | boolean   |            |
| Class EventProperty | eventPropertyQualities         | ArrayList |            |
| Class EventProperty | requiresEventPropertyQualities | ArrayList |            |
| Class EventProperty | propertyScope                  | String    |            |
| Class EventProperty | index                          | int       |            |
| Class EventProperty | runtimeID                      | String    |            |


Why
3 runtimeType => not Part of Class EvbentProperty Class
4 measurementUnit => not Part of Class EvbentProperty Class
5  valuesSpecitication =>  not Part of Class EvbentProperty Class 


![[ep_long.changed.png]]

![[ep_speed.changed.png]]

![[ep_time.changed 1.png]]



## Types

| Type                    | Description                |
| ----------------------- | -------------------------- |
| EventPropertiyPrimitive | flat single value          |
| EventPropertyList       | List of flat single values |
| EventPropertyNested     | Deprecated?                | 



## Read

It can be called in the required Section via

| Read Way            | Desciption |
| -------------- | ---------- |
| EpRequirements |            |

How to read List?


## Write

| Write Way                                                | Description |
| -------------------------------------------------- | ----------- |
| EventPropertiyPrimitiveBuilder                     |             |
| EpProperty                                         |             |
| Arrays.asList( EpProperties... , EpProperties... ) |             | 



### EventPropertiyPrimitiveBuilder

This is used to build a complex Event Schema with the runtimeName, runtimeType and domainProperty and also optional attributes.

| required | method                                                                              | desciption |
| -------- | ----------------------------------------------------------------------------------- | ---------- |
| yes      | .create(Datatypes datatype, String runtimeName)                                     |            |
| yes      | .domainProperty(String domainProperty)                                              |            |
| yes      | .build()                                                                            |            |
|          |                                                                                     |            |
| optional | .description(String description)                                                    |            |
| optional | .label(String label)                                                                |            |
| optional | .scope(PropertyScope propertyScope)                                                 |            |
| optional | .measrumentUnit(URI measurementUnit)                                                |            |
| optional | .resolution(Float resolution)                                                       |            |
| optional | .valueSpecification(Float min, Float max, Float step)                               |            |
| optional | .valueSpecification( String label, String description, List< String> allowedValues) |            |


Why is domainProperty not an Array List?


### EpProperty

this is used to build a basic Event Schema with 
the method also defines the runtimeType


#### Time

| Method                                | description |
| ------------------------------------- | ----------- |
| timestampProperty(String runtimeName) |             |



#### String

| Method                                                                                        | description |
| --------------------------------------------------------------------------------------------- | ----------- |
| stringEp(Label label, String runtimeName, String domainProperty, Enumeration enumeration)     |             |
| stringEp(Label label, String runtimeName, String domainProperty, PropertyScope propertyScope) |             |
| stringEp(Label label, String runtimeName, String domainProperty)                              |             |
| stringEp(Label label, String runtimeName, List < Uri> domainProperties)                       |             |



#### Double

| Method                                                                                                        | description |
| ------------------------------------------------------------------------------------------------------------- | ----------- |
| doubleEp(Label label, String runtimeName, String domainProperty)                                               |             |
| doubleEp(Label label, String runtimeName, String domainProperty, Float minValue, Float maxValue, Float step) |             |



#### Integer

| Method                                                                                                         | description |
| -------------------------------------------------------------------------------------------------------------- | ----------- |
| integerEp(Label label, String runtimeName, List < Uri> domainProperties)                                        |             |
| integerEp(Label label, String runtimeName, String domainProperty, QuantitativeValue valueSpecification)        |             |
| integerEp(Label label, String runtimeName, String domainProperty, Float minValue, Float maxValue, Float step) |             |



#### Number

| Method                                                           | description |
| ---------------------------------------------------------------- | ----------- |
| numberEp(Label label, String runtimeName, String domainProperty) |             |




#### General

| Method                                                                          | description |
| ------------------------------------------------------------------------------- | ----------- |
| ep(Label label, String runtimeType, String runtimeName, String domainProperty) |             |


#### Boolean

| Method                                                            | description |
| ----------------------------------------------------------------- | ----------- |
| booleanEp(Label label, String runtimeName, String domainProperty) |             |


#### Long
| Method                                                              | description |
| ------------------------------------------------------------------- | ----------- |
| longEp(Label label, String runtimeName, String domainProperty)      |             |
| longEp(Label label, String runtimeName, List< URI> domainProperty) |             |



#### Image
| Method                                | description |
| ------------------------------------- | ----------- |
| imageProperty(String runtimeName) |             |



### List


#### General

| Method                                                                                      | description |
| ------------------------------------------------------------------------------------------- | ----------- |
| listEp(Label label, String runtimeName, Datatypes runtimeType, String domainProperty)       |             |
| listEp(Label label, String runtimeName, EventPropety eventProperty, String domainProperty) |             |
| listEp(Label label, String runtimeName, EventProperty eventProperty)                                                                                            |             |



#### String

| Method                                                               | description |
| -------------------------------------------------------------------- | ----------- |
| ListStringEp(Label label, String runtimeName, String domainProperty) |             |


#### Double

| Method                                | description |
| ------------------------------------- | ----------- |
| listDoupleEp(Label label, String runtimeName, String domainProperty) |             |


#### Boolean

| Method                                | description |
| ------------------------------------- | ----------- |
| listBoolean(Label label, String runtimeName, String domainProperty)) |             |


#### Integer

| Method                                                                | description |
| --------------------------------------------------------------------- | ----------- |
| listIntegerEp(Label label, String runtimeName, String domainProperty) |             |


#### Long

| Method                                                             | description |
| ------------------------------------------------------------------ | ----------- |
| listLongEp(Label label, String runtimeName, String domainProperty) |             |



### Nested


| Method                                                                                                        | description |
| ------------------------------------------------------------------------------------------------------------- | ----------- |
| listNestedEp(Label label, String runtimeName, List< EventProperty... eventProperties)                         |             |
| listNestedEp(Label label, String runtimeName, String domainProperty, List< Eventproperty> listItemProperties) |             |




## Scope

There are 4 types of scope

Why needs scope to be mentioned in requiredEvent?

| Type                 | Description                                                                                                                                                                                                                                            |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| HEADER_PROPERTY      | A property that defines meta-information about the event, for instance its occurrence time                                                                                                                                                             |
| DIMENSION_PROPERTY   | A property that describes context of a measurement, e.g., the ID of a machine or a thing.                                                                                                                                                              |
| MEASUREMENT_PROPERTY | A property that contains (often quantitative) measurement values                                                                                                                                                                                       |
| NONE                 | The property scope is not further described. Use this scope for defining property requirements where the data * processor's functionality does not require any specific property scope (e.g., a text filter that can filter any * text-based property) |



## Quality

![[quality.png]]



## DomainProperty

You can either use an own URI Link
or use a varity of Streampipes  implemented vocabularies.
A full list can be found under the vocabulary packade:

![[vocabulary.png]]




## Labels

Labels.withID(String internalID)
Labels.empty()


Deprecated:
Why deprecated?

Labels.from(String internalID, String label, String description)
Labels.withTitle(String label, String desciption)
Labels.fromResourcess(String resourceIdentifier, String resourceName)
