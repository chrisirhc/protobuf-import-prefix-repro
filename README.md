# Examples of using Protobuf to get an output with import prefixes
I wanted to achieve the behavior of adding an import prefix to compiled `.proto` libraries. This is commonly done to avoid package namespace collisions, especially when the package is already defined by other files or libraries.

For instance, if a proto file contains the import statement `import "deps.proto"`, it can be converted to `from a.b import deps` in the case of Python.

The straightforward approach to achieve this with the protoc plugin is to nest the proto files within directories that correspond to the desired import prefix (e.g., `a/b` for `a.b`). This method generally works well, except when the proto files need to import each other.

In such cases, it becomes necessary to rewrite all the imports in the proto files with the appropriate prefix. You can refer to the `protoc-import-statement-with-prefix` for an example of how to do this.

## Bazel rules use (rules_proto_grpc)
Similarly, when using rules_proto_grpc, which delegates to the protoc compiler,
and using the `import_prefix`, the only way to use an import prefix is to also
add it to all of the existing import statements of the `.proto` file. 

Related issues:
* [Support adding a pb2_module_prefix on protoc plugin by chrisirhc · Pull Request #196 · vmagamedov/grpclib][grpclib-pr196]
* [Python: support for optional python_package (or similar) to make import explicit · Issue #7061 · protocolbuffers/protobuf][protobuf#7061] 
* [add support for module import prefix on Python compiler by chrisirhc · Pull Request #17286 · protocolbuffers/protobuf][protobuf-pr17286]

[grpclib-pr196]: https://github.com/vmagamedov/grpclib/pull/196
[protobuf#7061]: https://github.com/protocolbuffers/protobuf/issues/7061
[protobuf-pr17286]: https://github.com/protocolbuffers/protobuf/pull/17286