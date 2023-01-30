```java
.create("org.apache.streampipes.example.timestampextractor")  
.category( 01 )  
.withLocales( 02 )  
.withAssets( 03 )
```


## 01 category


With Category you can divide the processors into certain groups. In the pipeline editor, you can sort all installed processors by groups or names (default).

If you set the category
```
.category(DataProcessorType.TIME)
```

the enum DataProcessorType Time with the title "Time Operators"  is used. The description is blank.

```
TIME("Time Operators", "")
```

The visible result looks as follows

![[additional_group.png]]
![[additional_.title.png]]


The DataProcessorType enum has the following structure and is part of the StreamPipes model  SDK description. 

`incubator-streampipes/streampipes-model/src/main/java/org/apache/streampipes/model/DataProcessorType.java`

The enum has the base structure of with
```
NAME(String label, String description)
```

Other available categories are:

* FILTER("Filters and Thresholds", "b")
* BOOLEAN_OPERATOR("Boolean Operators", "")
* STRING_OPERATOR("Text/String Operators", "")
* COUNT_OPERATOR("Count Operators", "")
* AGGREGATE("Aggregation", "") 
* ENRICH_TEXT("Text/NLP Operators", "")
* ENRICH("Enrichment", "")
* GEO("Geospatial Operations", "")
* IMAGE_PROCESSING("Image Processing", "")
* PATTERN_DETECT("Pattern Detection", "")
* ALGORITHM("Algorithm", "")
* VALUE_OBSERVER("Value Observation", "")
* STRUCTURE_ANALYTICS("Structure/Stream Analytics", "")
* TRANSFORM("Transformation", "")
* TIME("Time Operators", "")
* SCRIPTING("Scripting/Code", "")
* UNCATEGORIZED("Uncategorized", "")

---

## 02 Locals

With the locals options  you can outsorce specific text components into a  strings file in the resource folder. Following languages are supported:

```java
EN("en"),  # => string.en
DE("de");  # => string.de
```

```java
.withLocales(Locales.EN)
```

![[additional_locals.png]]



An advantage of this additional facility is that the title and description do not need to be set in the creation method:
```java
.create("org.apache.streampipes.example.timestampextractor", "Timestamp Extractor", "Extracts a timestamp into its individual time fields.")
```

 You can offload this to the appropriate Sting file. Use only the `create(String id)` method.
```java
.create("org.apache.streampipes.example.timestampextractor")
```

This internal ID must be used in the string file and with the extensions "title" and "description" you can now also enter the same text. For this reason, the ID must also be unique!
The result looks like this:
```markdown
org.apache.streampipes.example.timestampextractor.title=Timestamp Extractor  
org.apache.streampipes.example.timestampextractor.description=Extracts a timestamp into its individual time fields.  
```

![[create_result.png]]



In addition to this general information about the functionality, you can also write a user help for each required field. Without this additional information, it may be difficult for the user to understand all the options.

![[string_nothing 1.png]]


For required data streams and properties, you can also add a title or description to these fields by using the string internalId. For this purpose, you can refer to the internalId as follows

```java
.requiredStream(  
    StreamRequirementsBuilder  
        .create()  
        .requiredPropertyWithUnaryMapping(EpRequirements.timestampReq(),  
            Labels.withId("timestampField"), PropertyScope.NONE)  
        .build())  
.requiredMultiValueSelection(Labels.withId("selectedOutputFields"),  
    ...  
)
```

```
timestampField.title=Timestamp Field  
selectedOutputFields.title=Extract Fields  
```


![[string_title.png]]


```
timestampField.title=Timestamp Field  
timestampField.description= Select a timestamp from the event stream.
  
selectedOutputFields.title=Extract Fields  
selectedOutputFields.description= Choose what fields ot the timestamp you want to extract via multiselection.
```


We also recommend not to use too many characters in the description and to use XXX characters maximum!

![[string_title_desciption.png]]


Make sure that you also include the Apache license header in the file before you commit it!
At the end the file "string.en" has the following content:

```
#  
# Licensed to the Apache Software Foundation (ASF) under one or more  
# contributor license agreements.  See the NOTICE file distributed with  
# this work for additional information regarding copyright ownership.  
# The ASF licenses this file to You under the Apache License, Version 2.0  
# (the "License"); you may not use this file except in compliance with  
# the License.  You may obtain a copy of the License at  
#  
#    http://www.apache.org/licenses/LICENSE-2.0  
#  
# Unless required by applicable law or agreed to in writing, software  
# distributed under the License is distributed on an "AS IS" BASIS,  
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  
# See the License for the specific language governing permissions and  
# limitations under the License.  
#  
  
org.apache.streampipes.processors.transformation.jvm.processor.timestampextractor.title=Timestamp Extractor  
org.apache.streampipes.processors.transformation.jvm.processor.timestampextractor.description=Extracts a timestamp into its individual time fields.  
  
timestampField.title=Timestamp Field  
timestampField.description= Select a timestamp from the event stream.  
  
selectedOutputFields.title=Extract Fields  
selectedOutputFields.description= Choose what fields ot the timestamp you want to extract via multiselection.

```

---

## 03 Assets


```
.withAssets(String assets)
```

The withAssets function allows to enrich the processor with additional (visual) information. There are two types of assets and the associated files must be placed in the resource folder like the locales string file.

* Assets.DOCUMENTATION  ⇾ documentation.md
* Assets.ICON  ⇾ icon.png

### Documentation

```java
.withAssets(Assets.DOCUMENTATION)
```

![[additional_locales_doc.png]]

The documentation allows a more detailed description of the main purpose of the processor, some general background information and more details about all required fields. It should also explain a visual description of the output result. 
The documentation file is a simple Markdown file and can be written using a simple Markdown syntax.

In this use case, we can equip more information with the following documentation:

```
<!--  
  ~ Licensed to the Apache Software Foundation (ASF) under one or more  
  ~ contributor license agreements.  See the NOTICE file distributed with  
  ~ this work for additional information regarding copyright ownership.  
  ~ The ASF licenses this file to You under the Apache License, Version 2.0  
  ~ (the "License"); you may not use this file except in compliance with  
  ~ the License.  You may obtain a copy of the License at  
  ~  
  ~    http://www.apache.org/licenses/LICENSE-2.0  
  ~  
  ~ Unless required by applicable law or agreed to in writing, software  
  ~ distributed under the License is distributed on an "AS IS" BASIS,  
  ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  
  ~ See the License for the specific language governing permissions and  
  ~ limitations under the License.  
  ~  
  -->  
  
## Timestamp Extractor  
  
***  
  
## Description  
  
This processor extracts a timestamp into the individual time fields (e.g. day field, hour field, ....)  
  
***  
  
## Required inputs  
  
This processor requires an event that provides a timestamp value (a field that is marked to be of type ``http://schema  
.org/DateTime``.  
  
***  
  
## Configuration  
  
### Timestamp Field  
  
The field of the event containing the timestamp to parse.  
  
### Extract Fields  
  
Select the individual parts of the timestamp that should be extracted, e.g., Year, Minute and Day.  
  
## Output  
  
The output of this processor is a new event that contains the fields selected by the ``Extract Fields`` parameter.

```


The user can access the documentation in the pipeline editor at various points.
1. In the Data Processor Overview by clicking the question mark button.
2. In the Pipeline Processor Element in the Build Board by clicking the question mark button.
3. In the processor setup windows by activating the show documentation button.


 ![[documentation_processor_overview.png]]                           ![[documentation_proceesor_element.png]]



![[documentation_processor_setup.png]]

### Icon

```java
.withAssets(Assets.DOCUMENTATION, Assets.ICON)
```


Up to now, the processor is called TE (Time Extraction) due to the first two capital letters of the title. However, this can lead to a misunderstanding situation. Imagine there is another processor with the name "Threshold Extractor" and also without an provied icon.

![[icon_duplication.png]]

As you can see, they have the same icon, but different titles. Everything still works, but the visual impression and identification could be improved to provide a better user experience!

Therefore, you can create a custom icon (named icon) in PNG format and paste it into the resources folder.

![[additional_all.png]]

The icon should meet the following conditions
* Format should have a format of 300 × 300 pixels.
* Do not use icons that have a license that must be mentioned, such as MIT, flaticon.com or or other appropriate sources.
* Use free license icons e.g. https://fonts.google.com/icons or https://www.svgrepo.com/ (watch out for the correct license for each individual  icon!) or create your own from scratch!
* The icon should be mono-color.
* Use the Roboto fonds (https://fonts.google.com/specimen/Roboto) for text. 

You can also add the icon in the documentation by adding:

```markdown
...
## Timestamp Extractor  
  
<p align="center">  
    <img src="icon.png" width="150px;" class="pe-image-documentation"/>  
</p>
...
```

![[icon_individual.png]]

## Template

### documentation template

```
<!--  
  ~ Licensed to the Apache Software Foundation (ASF) under one or more  
  ~ contributor license agreements.  See the NOTICE file distributed with  
  ~ this work for additional information regarding copyright ownership.  
  ~ The ASF licenses this file to You under the Apache License, Version 2.0  
  ~ (the "License"); you may not use this file except in compliance with  
  ~ the License.  You may obtain a copy of the License at  
  ~  
  ~    http://www.apache.org/licenses/LICENSE-2.0  
  ~  
  ~ Unless required by applicable law or agreed to in writing, software  
  ~ distributed under the License is distributed on an "AS IS" BASIS,  
  ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  
  ~ See the License for the specific language governing permissions and  
  ~ limitations under the License.  
  ~  
  -->  
  
## PROCESOR NAME  

<p align="center">  
    <img src="icon.png" width="150px;" class="pe-image-documentation"/>  
</p>
  
***  
  
## Description  

TEXT
  
***  
  
## Required inputs  

TEXT

***  
  
## Configuration  
  
### Timestamp Field  
  
TEXT
  
### Extract Fields  
  
TEXT
  
## Output 

TEXT with Example
  

```


### Icon PNG template

This template can be used in gimp or other pixel-based programs!

### Icon SVG template

This template can be used in Inkscape or other vector-based programs. This format has to be converted to PNG!


---




