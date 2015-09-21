# Quick start #

This section contains a description of the minimal steps required to implement a new score calculator. Basically, all you need to do is
  1. implement a class with two methods described below and
  1. tell your server to use this scoring class
If you want to know more details on the Java reference implementation, read on [here](PSISCORE_web_service_implementation_details.md).

## 1) The mandatory scoring methods ##

### `getScores()` method ###
This method is the place where the scoring of individual interactions is performed. The input to the method is an `Interaction` object of the EntrySet representation of the input data. This interaction object contains references to all its participating interactors, their database identifiers, etc. If your method provides confidence scores that are precalculated, then you will only need to look up the scores in your database and add them as new `Confidence` objects to the `Interaction` like in the following:

```
Collection<Confidence> confidences = new HashSet<Confidence>();

Names names = new Names();
names.setShortLabel("confidence");
names.setFullName("your confidence");
Unit unit = new Unit();
unit.setNames(names);
Confidence confidence = new Confidence();
confidence.setUnit(unit);
confidence.setValue(value); // e.g. "1.0"

confidences.add(confidence);

return confidences;
```

The `getScores` method will return the collection of confidences that your calculator generated.

### `getSupportedScoringMethods` method ###
This method tells the PSISCORE server (and indirectly the PSISCORE clients and the PSISCORE registry), what scoring algorithms your server provides and what requirements each method potentially has. Users can use this list to select certain scoring algorithms.
A very simple, hard-coded, example for this method is listed below:

```
List<AlgorithmDescriptor> descriptorList = new ArrayList<AlgorithmDescriptor>();

AlgorithmDescriptor descriptor = new AlgorithmDescriptor();
descriptor.setId("example confidence"); // this id has to be unique within the server
List<String> algorithmTypes = descriptor.getAlgorithmType();
algorithmTypes.add("predicted");
algorithmTypes.add("functional similarity");
descriptor.setRange("0-1");

descriptorList.add(descriptor);

return descriptorList;
```

The id of the scoring method has to be unique within the server. In addition, this id will be used to link your service to a textual description in the [Molecular Interaction controlled vocabulary](http://www.ebi.ac.uk/ontology-lookup/browse.do?ontName=MI) or the [PSISCORE\_registry](PSISCORE_registry.md).

### Your scoring calculator class ###
The two methods `getScores` and `getSupportedScoringMethods` have to be located in a Java class that extends the `AbstractScoreCalculator` (described in more details below). You can see two working exemplary scoring calculators in the reference implementation [source code](http://code.google.com/p/psiscore/source/checkout). Both calculators read confidence scores for certain binary interactions from flat text files. These calculators should only illustrate the general architecture of the reference implementation.

## 2) Registering your score calculator ##
Once you finished the implementation of your scoring class, you only need to register it with the `DefaultPsiscoreService` that manages all score calculators.

The code snippet in the `DefaultPsiscoreService` that contains the calculator listing can be seen below:
```
private String[] calculatorClasses = {"org.hupo.psi.mi.psiscore.ws.ExampleScoreCalculator",
    		"org.hupo.psi.mi.psiscore.ws.YetAnotherExampleScoreCalculator"};
```

In this example, the scoring server provides two calculator classes. If you want to add or remove certain calculators, you can do so by simply changing the list above. Be careful to use the correct combination of package (e.g. "org.hupo.psi.mi.psiscore.ws") and class name ("ExampleScoreCalculator") as your calculator can otherwise not be loaded.

With your new score calculator implemented and registered in the `DefaultPsiscoreService`  you can [compile](Creating_a_new_PSISCORE_server.md) the source code and test your implementation.