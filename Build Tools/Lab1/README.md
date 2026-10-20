# Lab 1: Building and Packaging a Java Application with Maven

## Objective
Build, package, and verify the CalculatorMavenApp Java application using Maven.

## Repository
[CalculatorMavenApp on GitHub](https://github.com/Ibrahim-Adel15/CalculatorMavenApp)

## Steps and commands
The project directory used in the terminal was `~/test/lab1/CalculatorMavenApp`.

1. Cloned or copied the CalculatorMavenApp source code into the project directory.
2. Opened the project directory.
3. Built and packaged the application with Maven.
4. Checked the generated files in the `target` directory.
5. Confirmed that `target/calculator.jar` exists and is approximately 3.7 KB.

Commands used to inspect the project and artifact:

```bash
cd ~/test/lab1/CalculatorMavenApp
ls
cat Dockerfile
ls -lh target/
```

The JAR file was present at:

```text
target/calculator.jar
```

## Results
- Generated artifact: `target/calculator.jar`
- Observed JAR size: approximately `3.7K`
- Maven unit-test result: **Add the result from your `mvn test` screenshot**
- Maven package result: **Add the result from your `mvn package` screenshot**
- Application run/verification: **Add the result from your application test screenshot**

## Dockerfile observed in this project
```dockerfile
FROM maven:3.10-eclipse-temurin-17-noble

WORKDIR /app

COPY . .

RUN mvn package

CMD ["java","-jar","target/calculator.jar"]

EXPOSE 8080
```

## Screenshots
Put your real screenshots in `screenshots/lab1/` and update this list with their exact filenames:
- Maven unit-test output
- Maven package/build output
- `target/calculator.jar` visible in the terminal
- Application running or a successful test

> Only mark tests or application execution as successful if the screenshot shows that result.

