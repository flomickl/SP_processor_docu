![[processorClass.png]]

return an ProcessingElementBuilder





## 1 create

![[create.png]]

## Basics

Creates a new processing element using the builder pattern.



### Parameters

| Type        | Pameter                | Description                                                                              |   
| ----------- | ---------------------- | ---------------------------------------------------------------------------------------- |
| String      | id                     | A unique identifier and used as internalId of the new element, e.g., com.mycompany.processor.mynewdataprocessor |     
| String      | label                  | A human-readable name of the element.                                                    |     
| String      | description            | A human-readable name of the element.                                                    |     
| Class Label | id, label, desctiption | Label exampleLabel = new Label(id, label, desctibtion)                                   |     



### Methods

| Method                                              | Description                                                                                  |     |
| --------------------------------------------------- | -------------------------------------------------------------------------------------------- | --- |
| create(String id)                                   | Just needs an ID, If this is used, the additional method withLocales(Locales...) is required |     |
| create(String id, String label, String description) |                                                                                              |     |
|       create(Label label)                                              |                                                                                              |     |


### Why and What

The ID is used internally as an identifier and must be unique. It is recommended to use the entire package name of the processor class. This ID is also used to refer to the associated resource folder of the processor class. This is achieved when the resource folder and the ID name match.

The label text represents the name of the processor and is displayed in the "Pipeline Editor" and in the "Install Pipeline Management".


The description is displayed under the label and preferably contains a short text about the function of the processor. It can be a maximum of xxx characters long.

The processor symbol is composed of the first letters of the designation titel.

### Example

```
create("org.apache.streampipes.example.timestampextractor", "Timestamp Extractor", "Extracts a timestamp into its individual time fields.")
```


![[create_result.png]]


