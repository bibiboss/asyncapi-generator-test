# Prerequisite

Read [this README](https://github.com/bibiboss/asyncapi-generator-test/blob/main/asyncapi%20test/README.md) first
to get a grasp of the intent of this branch.

# Introduction

The repository is meant to illustrate issue faced in [this repository](https://github.com/sngular/scs-multiapi-plugin).

As of now, this repository illustrates [this issue](https://github.com/sngular/scs-multiapi-plugin/issues/312).

This branch offers a workaround that is not completely fulfilling the [schema's specification](https://github.com/asyncapi/spec-json-schemas/blob/master/definitions/2.5.0/schema.json) of asyncapi.

# Workaround description

In [asyncpi.yml](./asyncapi.yml), line 61, instead of an "anonymous"
object declaration (see the main branch readme for "anonymous" explanation),
object "commitId" has been declared.

This results in correctly generated objects.