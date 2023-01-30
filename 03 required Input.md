
![[requirement_parameters.png]]

----


## Alternatives

When and Why Text

### Methods

method `.requiredAlternatives` 

| Input Parameters                                       | Description | Example | Visual | 
| ------------------------------------------------------ | ----------- | ------- | ------ |
| Label label, Static PropertyAltermative... alternative |             |         |        |

### Extractor 


```java

```


---

## Codeblock

![[stream_requirement_code.png]]

### Methods

method `.requiredCodeblock()` 

| Input Parameters                                               | Desciption | Example | Visual |
| -------------------------------------------------------------- | ---------- | ------- | ------ |
| Label label,                                                   |            |         |        |
| Label label, String defaultSkeleton                            |            |         |        |
| Label label, CodeLanguage codeLanguage                         |            |         |        |
| Label label, CodeLanguage codeLanguage, String defaultSkeleton |            |         |        |

CodeLanguage Types
* None
* Python
* JavaScript

### Extractor

```java
String code = parameters.extractor().codeblockValue(String internalName)
```

---

## Collection

### Methods

method `.requiredCollection()` 

| Input Parameters                                | Desciption | Example | Visual |
| ----------------------------------------------- | ---------- | ------- | ------ |
| Label label, StaticProperty... staticProperties |            |         |        |


### Extractor

```java

```

---


## ColorParameter

![[stream_requirement_color.svg]]

What type of color? RGB? HEX?


### Methods

method `.requiredColorParameter()`

| Input Parameters                 | Desciption | Example | Visual |
| -------------------------------- | ---------- | ------- | ------ |
| Label label                      |            |         |        |
| Label label, String defaultColor |            |         |        |

### Extractor

```java

```

---


## File

![[stream_requirement_file.png]]


### Methods

method `.requiredFile()`

| Input Parameters                            | Desciption | Example | Visual |
| ------------------------------------------- | ---------- | ------- | ------ |
| Label label                                 |            |         |        |
| Label label, String requiredFiletypes       |            |         |        |
| Label label, Filetypes... requiredFiletypes |            |         |        |

Filetypes:
* CSV("csv")
* JPG("jpg", "jpeg")
* JSON("json")  
* XLS("xls") 
* XLSX("xlsx") 
* XML("xml"), 
* ZIP("zip")

### Extractor

```java

```


---


### Float

![[stream_requirement_float.png]]


### Methods

method `.requiredFloadParameter()`

| Input Parameters                                                                      | Desciption | Example | Visual |
| ------------------------------------------------------------------------------------- | ---------- | ------- | ------ |
| Label label                                                                           |            |         |        |
| Label label, Float defaultValue                                                        |            |         |        |
| Label label, Float min, Float max, Float step                                         |            |         |        |
| Label label, String linkedMappingPropertyInternalName                                 |            |         |        |
| String internalId, String label, String description, Float min, Float max, Float step |            |         |        |

### Extractor

```java
Float example = parameters.extractor().singleValueParameter(String internalName, Float.class);
```
---


## HTML

![[stream_requirement_html.png]]

### Methods

method `.requiredHtmlInputParameter()`

| Input Parameters | Desciption | Example | Visual | 
| ---------------- | ---------- | ------- | ------ |
| Label label      |            |         |        |

### Extractor

```java

```


---


## Integer

![[stream_requirement_integer.png]]

### Methods

method `.requiredIntegerParameter()` 

| Input Parameters                                                                            | Desciption | Example | Visual |
| ------------------------------------------------------------------------------------------- | ---------- | ------- | ------ |
| Label label                                                                                 |            |         |        |
| label label, Integer defaultValue                                                           |            |         |        |
| Label label, Integer min, Integer max, Integer step                                         |            |         |        |
| Label label, String linkedMappingPropertyInternalName                                       |            |         |        |
| String internalId, String label, String description, Integer min, Integer max, Integer step |            |         |        |


### Extractor

```java
Integer example = parameters.extractor().singleValueParameter(String internalName, Integer.class);
```


---


## MultiValueSelection

![[stream_requirement_multiSelect.png]]

### Methods

method `.requiredMultiValueSelection()`

| Input Parameters                     | Desciption | Example                                                                                                          | Visual |
| ------------------------------------ | ---------- | ---------------------------------------------------------------------------------------------------------------- | ------ |
| Label label, Options... options      |            | `requiredMultiValueSelection(Labels.withId(String internalName), Options.from("Option1", "Option2", "Option3"))` |        | 
| Label label, List < Option > options |            |                                                                                                                  |        |

### Extractor

```java
List<String> selectedMultiValue = parameters.extractor().selectedMultiValues(String internalName, String.class);
```

---


## MultiValueSelectionFromContainer


### Methods

method `.requiredMultiValueSelectionFromContainer()`

| Input Parameters                       | Desciption | Example | Visual | 
| -------------------------------------- | ---------- | ------- | ------ |
| Label label                            |            |         |        |
| Label label, List < String > dependsOn |            |         |        |

### Extractor

```java

```

---

## OntologyConcept


### Methods

method `.requiredOntologyConcept()`

| Input Parameters                                                                         | Desciption | Example | Visual | 
| ---------------------------------------------------------------------------------------- | ---------- | ------- | ------ |
| Label label, SupportedProperty... supportedOntologyProperties                            |            |         |        |
| Label label, String requiredConceptUri, SupportedProperty... supportedOntologyProperties |            |         |        |

### Extractor

```java

```

---

## SingleValueSelection

![[stream_requirement_singleSelect.png]]

### Methods

method `.requiredSingleValueSelection()`

| Input Parameters                                                  | Desciption | Example                                                                                                           | Visual |
| ----------------------------------------------------------------- | ---------- | ----------------------------------------------------------------------------------------------------------------- | ------ |
| Label label, Option... options                                    |            | `requiredSingleValueSelection(Labels.withId(String internalName), Options.from("Option1", "Option2", "Option3"))` |        |
| Label label, List < Option > options                              |            |                                                                                                                   |        |
| Label label, List < Option > options, boolean horizontalRendering |            |                                                                                                                   |        |

### Extractor

```java
String example = parameters.extractor().selectedSingleValue(String internalName, String.class));
```

---


## SingleValueSelectionFromContainer


### Methods

method `.requiredMultiValueSelectionFromContainer`

| Input Parameters                       | Desciption | Example | Visual | 
| -------------------------------------- | ---------- | ------- | ------ |
| Label label, List < String > dependsOn |            |         |        |

### Extractor

```java

```

---


## SlideToogle


### Methods

method `.requireSlideToggle

| Input Parameters                  | Desciption | Example | Visual | 
| --------------------------------- | ---------- | ------- | ------ |
| Label label, boolean defaultValue |            |         |        |

### Extractor

```java

```

---


## StaticProperty

### Methods

method `.requiredStaticProperty`

| Input Parameters              | Desciption | Example | Visual | 
| ----------------------------- | ---------- | ------- | ------ |
| StaticProperty staticProperty |            |         |        |


### Extractor

```java

```

---

## Stream


### Methods

method `.requiredStream`

| Input Parameters                               | Desciption | Example | Visual | 
| ---------------------------------------------- | ---------- | ------- | ------ |
| CollectedStreamRequirements streamRequirements |            |         |        |

### Extractor

```java

```

---


## Text

![[stream_requirement_text.png]]

### Methods

method `.requiredTextParameter`
| Input Parameters                                              | Desciption | Example | Visual | 
| ------------------------------------------------------------- | ---------- | ------- | ------ |
| Label label                                                   |            |         |        |
| Label label, String defaultValue                              |            |         |        |
| Label loabel, boolean multiline, boolan placeholdersSupported |            |         |        |

### Extractor

```java
String example = parameters.extractor().textParameter(String internalName, String.class);
```

---


## TextParameterWithLink


### Methods

method `.requiredTextParameterWithLink`

| Input Parameters                                      | Desciption | Example | Visual | 
| ----------------------------------------------------- | ---------- | ------- | ------ |
| Label label, String linkedMappingPropertyInternalName |            |         |        |


### Extractor

```java

```

---


## Extractor methods


| Type                        | Method                                                                                                     | Description |
| --------------------------- | ---------------------------------------------------------------------------------------------------------- | ----------- |
| String                      | outputKeySelectors()                                                                                       |             |
| List < String >             | outputTopic()                                                                                              |             |
| String                      | singleValueParameter(String internalName, Class < V > targetClass)                                         |             |
| V                           | singleValueParameter(EventPropertyPromitive targetType, String internalName)                               |             |
| List < StaticPropertyGroup> | collectionMembersAsGroup(String internalName)                                                              |             |
| Boolean                     | comparePropertyRuntimeType(EventProperty eventProperty, Datatypes datatype)                                |             |
| Boolean                     | comparePropertyRuntimeType(EventProperty eventProperty, Datatypes datatype, boolean ignoreListElements)    |             |
| StaticProperty              | extractGroupMember(String internalName, StaticPropertyGroup group)                                         |             |
| List < EventProperty>       | getEventPropertiesByScope(PropetyScope scope)                                                              |             |
| List < EventProperty>       | getEventPropertiesBySelector(List < String > selectors)                                                    |             |
| List < String>              | getEventPropertiesRuntimeNameScope(PropertyScope scope)                                                    |             |
| List < String>              | getEventPropertiesSelectorByScope(PropertyScope scope)                                                     |             |
| EventProperty               | getEventPropertyBySelector(String selector)                                                                |             |
| String                      | getEventPropertyTypeBySelector(String selector)                                                            |             |
| List < EventProperty>       | getInputStreamEventPropertySubset(List < String> propertySelectors)                                        |             |
| List < EventProperty>       | getNoneInputStreamEventPropertySubset(List < String> propertySelectors)                                    |             |
| StaticProperty              | getStaticPropertyByName(String name)                                                                       |             |
| W                           | getStaticPropertyByName(String internalName, Class< W> spType)                                             |             |
| List < String>              | getUnaryMappingsFromCollection(STring collectionsStaticPropertyName)                                       |             |
| String                      | inputTopic(Integer streamIndex)                                                                            |             |
| String                      | mappingPropertyValue(String staticPropertyName)                                                            |             |
| List < String>              | mappingPropertyValues(String staticPropertyName)                                                           |             |
| String                      | measurementUnit(String runtimeName, Integer streamIndex)                                                   |             |
| String                      | propertyDatatype(String runtimeName)                                                                       |             |
| String                      | secretValue(String internalName)                                                                           |             |
| String                      | selectedAlternatuveInternalId(String alternativesInternalId)                                               |             |
| String                      | selectedColor(String internalName)                                                                         |             |
| String                      | selectedFilename(String internalName)                                                                      |             |
| List < V>                   | selectedMultiValues(String internalName, Class < V> targetClass)                                           |             |
| V                           | selectedSingleValue(String internalName, Classs < V> targetClass)                                          |             |
| V                           | selectedSingleValueInternalName(String internalName, class < V> targetClass)                               |             |
| List < V>                   | selectedTreeNodesInternalName(String internalName, Class < V> targetClass, boolean onlyDataNodes)          |             |
| List < V>                   | singleValueParameterFromCollection(String internalName, Class < V> targetClass)                            |             |
| boolean                     | slideToogleValue(String internalName)                                                                      |             |
| V                           | supportedOntologyPropertyValue(String domainPropertyInternalId, String propertyId, Class > V> targetClass) |             |
| String                      | textParameter(String internalName)                                                                                                           |             |





