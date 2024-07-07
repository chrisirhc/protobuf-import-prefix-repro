1. Download a pre-built binary from https://github.com/protocolbuffers/protobuf/releases
2. Assuming `protoc` is the path to the binary.

```sh
protoc --python_out=. -Ia/b/ importer.proto dep.proto
# Works but generated files does not have b/ (b.) prefix or a/b/ (a.b.).

protoc --python_out=.  -I. -Ia/b/  a/b/importer.proto a/b/dep.proto
# Error:
# a/b/dep.proto:4:9: "tutorial.Dep" is already defined in file "dep.proto".

protoc --python_out=. -Ia b/dep.proto b/importer.proto
# dep.proto: File not found.
# b/importer.proto:4:1: Import "dep.proto" was not found or had errors.
# b/importer.proto:7:3: "tutorial.Dep" seems to be defined in "b/dep.proto", which is not imported by "b/importer.proto".  To use it here, please add the necessary import.

protoc --python_out=. -Ia/ -Ia/b/ b/importer.proto b/dep.proto
# b/dep.proto:4:9: "tutorial.Dep" is already defined in file "dep.proto".

protoc --python_out=. -Ia/ -Ia/b/ b/dep.proto b/importer.proto
# dep.proto:4:9: "tutorial.Dep" is already defined in file "b/dep.proto".
# b/importer.proto:4:1: Import "dep.proto" was not found or had errors.
# b/importer.proto:7:3: "tutorial.Dep" seems to be defined in "b/dep.proto", which is not imported by "b/importer.proto".  To use it here, please add the necessary import.

```