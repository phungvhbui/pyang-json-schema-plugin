# pyang-json-schema-plugin

This is a pyang JSON Schema output plugin. It takes YANG files and tries to produce a JSON Schema that validates JSON content payload as defined in [RFC7951](https://tools.ietf.org/html/rfc7951).

## Prerequisite
Assuming you installed python3 and pip3:
- Install pyang using pip3:
```
$ pip3 install pyang
```

## Usage
1. Navigate to the model directory (compulsory). If you miss this step, pyang will not be able to resolve the path in models
```
$ cd test/yang
```
2. Use the plugin with pyang
- In most case, a valid model should have leaves at the root of the module
```
pyang --plugindir <jsonschema.py file location> -f jsonschema <input filename> > <output path>
```
- There is a special case where you want to convert a module with only groupings, use `--jsonschema-main` to define the main grouping
```
pyang --plugindir <jsonschema.py file location> -f jsonschema --jsonschema-main <grouping name> <input filename> > <output path>
```

Additional arguments:
- If imported modules are located in another directory than the pwd one, use `--path <dir path>` to make pyang check for that folder when resolving imports
```
pyang --plugindir <jsonschema.py file location> -f jsonschema --path <dir path> <input filename> > <output path>
``` 

- To turn on debug mode, use `--jsonschema-debug`
```
pyang --plugindir <jsonschema.py file location> -f jsonschema --jsonschema-debug <input filename> > <output path>
```

## Supported keywords
Mostly following [jsonschema](https://json-schema.org/specification.html) and [jsonschema2pojo](https://github.com/joelittlejohn/jsonschema2pojo/wiki/Reference) specifications
- leaf
- list: Following [jsonschema2pojo array]()
- leaf_list
- container
- choice

## Supported data types
Mostly following [jsonschema](https://json-schema.org/specification.html) and [jsonschema2pojo](https://github.com/joelittlejohn/jsonschema2pojo/wiki/Reference) specifications
- string
- enum: Following [jsonschema2pojo javaEnums](https://github.com/joelittlejohn/jsonschema2pojo/wiki/Reference#javaenums) to add support for custom values
- bits
- boolean
- empty
- union
- instance-identifier
- leafref
- all numeric types (example: int8, uint16,...)
