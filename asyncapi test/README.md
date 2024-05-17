# Introduction

The repository is meant to illustrate issue faced in [this repository](https://github.com/sngular/scs-multiapi-plugin).

As of now, this repository illustrates [this issue](https://github.com/sngular/scs-multiapi-plugin/issues/312).

# Issue faced

## Context

In [asyncapi.yml](./asyncapi.yml), you have two "anonymous" objects called "data" that are referenced.
Line 60, in '#/components/schemas/input/properties/data' and line 80 in '#/components/schemas/output/properties/data'.

With the configuration of plugin com.sngular:scs-multiapi-maven-plugin, you can put these two definitions in two different packages, since one is used as consumer's model, and the other one as supplier's model.

In this case, test2.model for consumer and test.model for the other one.

## Expected result

Based on the [asyncapi json specs](https://github.com/asyncapi/spec-json-schemas) from which [the yaml schema is driven](https://github.com/asyncapi/spec-json-schemas?tab=readme-ov-file#schemastore-compatibility-testing), you can have objects that are defined but not referenced (let's call these objects "anonymous").
That is what is done in the two examples in the 'Context' section.

Running the command `mvn clean package` would result in generation of the correct models, with one object "Data" in the test2.model package, and one in test.model package.
Even if a naming convention imposes variants like Data1 and Data2, the `mvn clean package` should result in a successful build.

## Actual result

Only one Data object is generated in test.model package and not in test2.model package, resulting in a build failure in generated test2.model.Input.java (not being able to import Data.java that is supposed to be in the same package).

# Appendix

Branch [test-alternative](https://github.com/bibiboss/asyncapi-generator-test/tree/test-alternative) provides a possible way to workaround, by defining Data as a specific object, and not "anonymously".

However, this workaround is not standard to the regards of the [schema's specification](https://github.com/asyncapi/spec-json-schemas/blob/master/definitions/2.5.0/schema.json) of asyncapi.