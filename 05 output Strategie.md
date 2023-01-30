
![[output.png]]


## Append

![[output_add.png]]

`Class AppendOutputStrategy`

### Description
An arbitrary number of event properties that are appended to any input stream.  


### Methods
```java
append(EventProperty... appendProperties)
```

```java
append(List<EventProperty> appendProperties)
```


### Examples
```
OutputStrategies.append(  
    EpProperties.numberEp(
	    Labels.withId("name_key"),  
        "runtime_name",  
        "http://schema.org/Number"
    )
)
```

```
OutputStrategies.append(
	EpProperties.doubleEp(
		Labels.empty(), 
		"runtime_name",  
	    SO.NUMBER)
	)
)
```

```
OutputStrategies.append(
	PrimitivePropertyBuilder.create( 
		Datatypes.String, 
		"appendedText"
	)
	.build()
)
```

```
OutputStrategies.append(  
    Arrays.asList(  
        EpProperties.numberEp(
	        Labels.empty(), 
	        "runtime_name", 
	        SO.NUMBER
	    ),  
        EpProperties.numberEp(
	        Labels.empty(), 
	        "runtime_name", 
	        SO.NUMBER
	    )
	)
)
```

```
OutputStrategies.append(
	PrimitivePropertyBuilder  
	    .create(Datatypes.Integer, EPSG_RUNTIME)  
	    .domainProperty("http://data.ign.fr/def/ignf#CartesianCS")  
    .build()
)
```

```
OutputStrategies.append(
	PrimitivePropertyBuilder  
	    .create(Datatypes.Float, DISTANCE_RUNTIME_NAME)  
	    .domainProperty(SO.NUMBER)  
	    .measurementUnit(URI.create("http://qudt.org/vocab/unit#Kilometer"))  
    .build()
)
```

```

OutputStrategies.append(
	EpProperties.timestampProperty(
		"key or runtime?"
	)
)
```


---

## custom
![[output_custom.png]]
`Class CustomOutputStrategy`

### Description

Custom output strategies let pipeline developers decide which events are produced by the corresponding pipeline element. 

### Methods

```
custom()
```


If two input streams are expected by a pipeline element, you can use outputBoth to indicate whether the properties of both input streams should be available to the pipeline developer for selection.

```
custom(boolean outputBoth)
```

### Examples

```
declareModel() {
	...
	OutputStrategies.custom(true))
	...
}

 public void onEvent(Event event, SpOutputCollector spOutputCollector) {

	HashMap lastEvents.put(
		event.getSourceInfo().getSelectorPrefix(), 
		event
	); 
	 
	if (lastEvents.size() == 2) {  
		spOutputCollector.collect(
			buildOutEvent(
				event.getSourceInfo().getSelectorPrefix()
			)
		);  
	}
}
```


---


## customTransformation

![[output_transform_custom.png]]

Class CustomTransformOutputStrategy

### Description


### Methods

```
customTransformOutputStrategy customTransformation()
```

### Examples

```
declareModel() {
	...
	OutputStrategies.customTransformation()
	...
}

 public void onEvent(Event event, SpOutputCollector spOutputCollector) {

	Event resultEvent = SomeClass.addLabel(
		event, 
		labelName, 
		value, 
		this.statements, 
		log
	);  
  
event.collect(resultEvent);
}
```


---

## Fixed
![[output_keep_fixed.png]]
Class FixedOutputStrategy

### Description
An arbitrary number of event properties that form the output event schema

### Methods
```
fixed(EventProperty... fixedProperties)
```

```
fixed(List<EventProperty> appendProperties)
```

### Examples
```
OutputStrategies.fixed(  
	EpProperties.timestampProperty("timestamp"),  
	EpProperties.stringEp(
		Labels.empty(), 
		"value", 
		"http://schema.org/Text"),  
    EpProperties.integerEp(
	    Labels.empty(), 
	    "count", 
	    "http://schema.org/Number")
	)
)
```

```
OutputStrategies.fixed(  
    Arrays.asList(  
        EpProperties.timestampProperty("timestamp"),  
        EpProperties.stringEp(Labels.withId(Message),  
            "message", "http://schema.org/text")  
    )
```

```
OutputStrategies.fixed(
	EpProperties.listNestedEp(
		Labels.withId("top"), "top",  
	    Arrays.asList(
		    EpProperties.integerEp(
			    Labels.withId("count"), 
			    "count", 
			    "http://schema.org/count"
			),  
	        EpProperties.stringEp(
		        Labels.withId("value"), 
		        "value", 
		        SO.TEXT)
		    )
		)
	)
)
```

```
OutputStrategies.fixed(  
    EpProperties.timestampProperty(TIMESTAMP_FIELD),  
    EpProperties.longEp(
	    Labels.withId(START_TIME_FIELD), 
	    START_TIME_FIELD, 
	    SO.DATE_TIME),  
    EpProperties.longEp(
	    Labels.withId(END_TIME_FIELD), 
	    END_TIME_FIELD, 
	    SO.DATE_TIME),  
    EpProperties.longEp(
	    Labels.withId(DURATION_FIELD), 
	    DURATION_FIELD, 
	    SO.NUMBER),  
    EpProperties.longEp(
	    Labels.withId(EVENT_COUNT_FIELD), 
	    EVENT_COUNT_FIELD, 
	    SO.NUMBER),  
    EpProperties.doubleEp(
	    Labels.withId(THROUGHPUT_FIELD), 
	    THROUGHPUT_FIELD, 
	    SO.NUMBER)
	)
)
```


---

## Keep

![[output_keep_update.png]]![[output_keep_filter.png]]

`KeepOutputStrategy`

### Description
Keep output strategies do not change the schema of an input event, i.e., the output schema matches the input schema.

### Methods
```
keep()
```

```
keep(boolean mergeInputStreams)
```

### Examples

* Update Value
```
declareModel() {
	...
	OutputStrategies.keep()
	...
}

public void onEvent(Event event, SpOutputCollector collector)
	...
	event.updateFieldBySelector("s0::" + EPSG_RUNTIME, targetEpsg);  
	event.updateFieldBySelector("s0::" + GEOM_RUNTIME, reprojected.toText());  
collector.collect(event);
	...

```

* Filter Value
```
declareModel() {
	...
	OutputStrategies.keep()
	...
}

 public void onEvent(Event event, SpOutputCollector spOutputCollector) {

	Boolean satisfiesFilter = false;
	...
	satisfiesFilter = (Math.abs(value - threshold) < 0.000001);
	...
	
	if (satisfiesFilter) {  
		  spOutputCollector.collect(event);  
	}
}
```

---

## List

![[output_list.png]]

`Class ListOutputStrategy`

### Description



### Methods
```
list(String propertyRuntimeName)
```

### Examples

???

---

## UserDefined

![[output_userdefined.png]]

### Description

User-defined output strategies are fully flexible output strategies which are created by users at pipeline development time.

### Methods
```
userDefined()
```

### Examples
```
declareModel() {
	...
	OutputStrategies.userDefined())
	...
}

 public void onEvent(Event event, SpOutputCollector outputCollector)
	// create new event with input event's source info and schema info.  
	Event outEvent = new Event(
		new HashMap<>(), 
		event.getSourceInfo(), 
		event.getSchemaInfo()
	);  
	
	try {  
  
	    final Map<String, Object> eventData = event.getRaw();  
	    
		Object result = function.execute(ProxyObject.fromMap(eventData));  
	    Map<String, Object> resultEvent = ((Value) result).as(java.util.Map.class);  
	    
    if (resultEvent != null) {  
	    resultEvent.forEach(outEvent::addField);  
	    outputCollector.collect(outEvent);  
    }
```


---


## Transform

![[output_transform.png]]

`Class TransformOutputStrategy`

### Description



### Methods
```
transform(TransformOperation... transformOperations)
```


Method for transform with parameters (String mappingPropertyInternalName, +)
* dynamicMeasurementUnitTransformation (+ String sourceStaticPropertyInternalName)
* staticMeasurementUnitTransformation (+ String targetValue)

* dynamicDatatypeTransformation (+ String linkedStaticProperty)
* staticDatatypeTransformation (+ Datatypes targetDatatype)

* dynamicRuntimeNameTransformation (+ String linkedStaticProperty)
* staticRuntimeNameTransformation (+ String targetValue)

* dynamicDomainPropertyTransformation (+ String linkedStaticProperty)
* staticDomainPropertyTransformation (+ String targetValue)


### Examples

```
OutputStrategies.transform(
	TransformOperations
		.dynamicMeasurementUnitTransformation(
	CONVERT_PROPERTY, OUTPUT_UNIT)))
```


```
OutputStrategies.transform(
	TransformOperations  
	    .dynamicRuntimeNameTransformation(
		    CONVERT_PROPERTY, 
			 FIELD_NAME
		)
)
```
