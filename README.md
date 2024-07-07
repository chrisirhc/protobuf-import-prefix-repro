# Examples of using Protobuf to get an output with import prefixes

I wanted to get the behavior of adding an import prefix to compiled `.proto`
libraries.
This is typically done to prevent package namespace collisions. For example when
the package is already defined by some other files/libraries.

For example, if a proto file contains: `import "deps.proto"`, convert it to
`from a.b import deps` in the case of Python.

The obvious way to do this with protoc plugin, is to nest the proto files within
the directories that you want the import prefix to be (a/b -> a.b). And it sort
of works, except when your proto files need to import each other.

Then, in that scenario, we'd also need to rewrite all the imports in the proto
files with the prefix. See `protoc-import-statement-with-prefix`.

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