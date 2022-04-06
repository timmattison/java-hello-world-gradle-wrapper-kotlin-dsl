FROM ghcr.io/graalvm/native-image:ol8-java17 as BUILD
# git is required to clone the repository from Github
# findutils is required because Gradle depends on xargs
RUN microdnf install git findutils
RUN git clone https://github.com/timmattison/java-hello-world-gradle-wrapper-kotlin-dsl.git
WORKDIR java-hello-world-gradle-wrapper-kotlin-dsl
RUN ./gradlew nativeCompile

FROM debian:latest as RUNNER
COPY --from=BUILD /java-hello-world-gradle-wrapper-kotlin-dsl/build/native/nativeCompile/helloworld helloworld
ENTRYPOINT ["/helloworld"]
