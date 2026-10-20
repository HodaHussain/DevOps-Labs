# Lab 2: Building and Packaging an Application with Gradle

## Objective
Build, test, and package the Gradle calculator project as described in the lab sheet.

## Repository
[CalculatorGradleApp on GitHub](https://github.com/Ibrahim-Adel15/CalculatorGradleApp)

## Required workflow
1. Install Gradle (if it is not already installed).
2. Clone the `CalculatorGradleApp` repository.
3. Open the project directory.
4. Run the unit tests.
5. Build the application using Gradle.
6. Check for the generated JAR at `build/libs/calculator.jar`.
7. Run the application and verify that it works.

## Commands
Run these from the Gradle project's directory. If the repository includes the Gradle Wrapper, use `./gradlew`; otherwise use the installed `gradle` command.

```bash
git clone https://github.com/Ibrahim-Adel15/CalculatorGradleApp.git
cd CalculatorGradleApp
gradle test
gradle build
ls -lh build/libs/
```

Alternatively, with the Gradle Wrapper:

```bash
./gradlew test
./gradlew build
```

## Results
**Status: needs your Lab 2 screenshots/terminal output to complete accurately.** The terminal output shared so far confirms the Maven project and Docker image information, but does not show the Gradle test/build results.

- Unit tests: **Fill in from your screenshot**
- Build result: **Fill in from your screenshot**
- Generated JAR: `build/libs/calculator.jar` — **confirm from your screenshot**
- Application verification: **Fill in from your screenshot**

## Screenshots
Put your actual screenshots in `screenshots/lab2/` and list their exact filenames:
- Gradle unit-test output
- Gradle build output
- `build/libs/calculator.jar`
- Application running or a successful test

> Do not claim that Lab 2 completed until the evidence confirms the required steps.
