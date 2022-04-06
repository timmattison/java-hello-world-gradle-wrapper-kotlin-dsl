FROM openjdk:latest as BUILD
# git is required to clone the repository from Github
# findutils is required because Gradle depends on xargs
RUN microdnf install git findutils
RUN git clone https://github.com/timmattison/java-hello-world-gradle-wrapper-kotlin-dsl.git
WORKDIR java-hello-world-gradle-wrapper-kotlin-dsl
RUN ./gradlew build
RUN jlink --output /custom-runtime --add-modules java.base

FROM debian:latest as RUNNER
COPY --from=BUILD /java-hello-world-gradle-wrapper-kotlin-dsl/build/libs/java-hello-world-gradle-wrapper-kotlin-dsl-all.jar app.jar
COPY --from=BUILD /custom-runtime /custom-runtime
ENTRYPOINT ["/custom-runtime/bin/java", "-cp", "app.jar", "com.timmattison.HelloWorld"]
