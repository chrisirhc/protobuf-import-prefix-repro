1. Download a pre-built binary from https://github.com/protocolbuffers/protobuf/releases
2. Assuming `protoc` is the path to the binary.
3. Run following commands in this directory with this README:
```sh
cd proto-import-statement-with-prefix/

protoc --python_out=. -Ia/b/ dep.proto importer.proto
# Generates files without prefix in this directory.

protoc --python_out=. -I. a/b/dep.proto a/b/importer.proto
# Generaets files with a.b prefix in a/b/
```