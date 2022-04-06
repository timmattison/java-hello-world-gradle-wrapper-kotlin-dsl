## Java Hello World using the Gradle Wrapper and the Kotlin DSL

This is a Hello World project that contains the most important parts of the Gradle build scripts I use on my projects.

## Found a bug? Something out of date?

File an issue and I'll try to fix it.

## Tasks

These are the tasks that most people will want to know about:
- `nativeCompile` - Compiles Hello World to the native platform
  - This requires GraalVM and native image support. The output binary is `./build/native/nativeCompile/helloworld`.
- `build` - Compiles Hello World and creates JAR files
  - Since the `com.github.johnrengelman.shadow` plugin is used two JAR files will be created:
    - `./build/libs/java-hello-world-gradle-wrapper-kotlin-dsl-all.jar` - this is the UBER jar that contains everything
    - `./build/libs/java-hello-world-gradle-wrapper-kotlin-dsl.jar` - this is the normal JAR that contains only the classes from this project

## License

MIT

