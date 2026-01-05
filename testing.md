# Java Testing Interview Q&A

---

### 1. What is unit testing in Java?

> Unit testing checks small parts of code, like methods or classes, to ensure they work correctly.

- Focuses on isolated components.
- Uses frameworks like JUnit or TestNG.
- Helps find bugs early.
- Improves code quality.

> Unit tests run fast and are automated, often part of build processes.
> Unit testing promotes better design and refactoring confidence. In Java, it integrates with tools like Maven for
> continuous integration.

---

### 2. What is JUnit?

> JUnit is a popular open-source framework for writing and running unit tests in Java.

- Supports annotations like @Test, @BeforeEach.
- Provides assertions for expected results.
- Integrates with IDEs like Eclipse or IntelliJ.
- Encourages test-driven development.

> JUnit 5 introduces modular design with Jupiter, Vintage, and Platform.
> JUnit is essential for TDD and CI/CD pipelines, making Java code more reliable and maintainable.

---

### 3. Why use JUnit for testing?

> JUnit simplifies writing repeatable tests and automates validation.

- Easy setup with annotations.
- Clear reporting of failures.
- Supports parameterized tests.
- Works well with mocking tools.

> It helps achieve high code coverage and reduces manual testing effort.
> In real interviews, emphasize JUnit's role in agile development for quick feedback loops.

---

### 4. What are JUnit annotations?

> Annotations like @Test mark methods as tests, @BeforeEach runs setup code.

- @AfterEach for cleanup.
- @BeforeAll for class-level setup.
- @Disabled to skip tests.
- @ParameterizedTest for multiple inputs.

> Annotations make tests declarative and easy to read.
> Using annotations properly ensures efficient test lifecycle management in Java projects.

---

### 5. What is an assertion in JUnit?

> Assertions check if the actual result matches the expected one, failing the test if not.

- assertEquals for equality.
- assertTrue for boolean conditions.
- assertThrows for exceptions.
- assertNotNull for non-null checks.

> JUnit provides a rich set of assertions from org.junit.jupiter.api.Assertions.
> Assertions are the core of validation; use them with clear messages for better debugging.

---

### 6. What is Test-Driven Development (TDD)?

> TDD is a practice where you write tests before the actual code.

- Red: Write failing test.
- Green: Make test pass with minimal code.
- Refactor: Improve code while keeping tests green.
- Repeat the cycle.

> TDD ensures code meets requirements from the start.
> In Java, TDD with JUnit leads to cleaner, more testable designs and fewer defects.

---

### 7. What are the benefits of TDD?

> TDD improves code quality and reduces bugs by focusing on requirements first.

- Encourages simple designs.
- Provides regression safety net.
- Speeds up development long-term.
- Enhances documentation through tests.

> Studies show TDD can reduce defect rates by 40-90%.
> Adopt TDD in Java teams for maintainable codebases, especially in agile environments.

---

### 8. What is Behavior-Driven Development (BDD)?

> BDD extends TDD by using natural language to describe behaviors, involving non-technical stakeholders.

- Uses Given-When-Then format.
- Tools like Cucumber or JBehave.
- Focuses on user stories.
- Bridges business and development.

> BDD scenarios are executable specifications.
> In Java, BDD promotes collaboration and ensures features align with business needs.

---

### 9. How does BDD differ from TDD?

> BDD focuses on system behavior from user perspective, while TDD targets code units.

- BDD uses readable language.
- TDD is developer-centric.
- BDD often for acceptance tests.
- TDD for unit tests.

> Both encourage testing first but at different levels.
> Choose BDD for team alignment, TDD for technical precision in Java projects.

---

### 10. What is Mockito?

> Mockito is a mocking framework for creating test doubles in Java unit tests.

- Mocks external dependencies.
- Verifies interactions.
- Stubs method calls.
- Easy syntax with when-then.

> Mockito uses proxies to simulate behavior.
> Essential for isolating units; integrates seamlessly with JUnit.

---

### 11. Why use mocking in unit tests?

> Mocking isolates the code under test from dependencies, focusing on its behavior.

- Avoids real database calls.
- Simulates edge cases.
- Speeds up tests.
- Improves reliability.

> Without mocking, tests become integration tests.
> In Java, tools like Mockito make unit testing practical for complex systems.

---

### 12. What is the difference between mock and spy in Mockito?

> Mock is a fake object with no real behavior; spy wraps a real object and tracks calls.

- Mock needs stubbing for all methods.
- Spy uses real methods unless stubbed.
- Use mock for full control.
- Use spy for partial mocking.

> Both extend ArgumentCaptor for verification.
> Choose based on how much real behavior you need in tests.

---

### 13. How do you verify interactions in Mockito?

> Use verify() to check if methods were called with expected arguments and times.

- verify(mock).method(arg);
- times(n) for call count.
- never() for no calls.
- atLeastOnce() for minimum.

> Verification fails the test if not matched.
> Crucial for behavior testing, not just state.

---

### 14. What is integration testing?

> Integration testing checks how different modules work together.

- Tests APIs, databases, services.
- Uses real or mocked dependencies.
- Slower than unit tests.
- Tools like Spring Boot Test.

> Focuses on interfaces and data flow.
> In Java, essential for ensuring system cohesion beyond units.

---

### 15. What is @SpringBootTest annotation?

> @SpringBootTest loads the full Spring application context for integration tests.

- Simulates real runtime.
- Auto-configures beans.
- Supports web environment.
- Can be slow for large apps.

> Use with @RunWith(SpringRunner.class) in JUnit 4.
> Ideal for end-to-end testing in Spring Boot applications.

---

### 16. What is MockMvc in Spring testing?

> MockMvc tests web controllers without starting a server.

- Simulates HTTP requests.
- Verifies responses.
- Integrates with Mockito.
- Uses perform() for actions.

> Part of spring-test module.
> Great for REST API testing, fast and isolated.

---

### 17. How do you test REST APIs in Spring Boot?

> Use MockMvc or TestRestTemplate for controller and integration tests.

- MockMvc for unit-like tests.
- TestRestTemplate for full HTTP.
- Assert status, body, headers.
- Mock services with Mockito.

> Include @WebMvcTest for focused tests.
> Ensures APIs work as expected in production.

---

### 18. What is TestNG?

> TestNG is a testing framework inspired by JUnit with more features.

- Supports data providers.
- Parallel test execution.
- Groups and dependencies.
- XML configuration.

> Often used with Selenium.
> In Java, choose TestNG for complex test suites over JUnit.

---

### 19. What is the difference between JUnit and TestNG?

> TestNG offers more advanced features like parallel runs and dependencies, while JUnit is simpler.

- TestNG has @DataProvider.
- JUnit 5 has dynamic tests.
- TestNG better for integration.
- JUnit widely used in Spring.

> Both support annotations.
> Pick based on project needs; many prefer JUnit for unit, TestNG for end-to-end.

---

### 20. What is code coverage?

> Code coverage measures how much of the code is executed by tests.

- Tools like JaCoCo or Clover.
- Lines, branches, methods.
- Aim for 80%+.
- Not a quality guarantee.

> Integrates with Maven/Gradle.
> High coverage helps but focus on meaningful tests.

---

### 21. What is a test suite in JUnit?

> A test suite runs multiple test classes together.

- Use @Suite annotation in JUnit 5.
- Groups related tests.
- Improves organization.
- Runs with one command.

> Useful for regression testing.
> In large Java projects, suites ensure comprehensive validation.

---

### 22. How do you handle exceptions in JUnit tests?

> Use assertThrows to verify expected exceptions.

- assertThrows(Exception.class, () -> code());
- Check message or cause.
- @Test(expected = Exception.class) in JUnit 4.
- Fail if no exception.

> Ensures error handling works.
> Critical for robust Java applications.

---

### 23. What is parameterized testing in JUnit?

> Parameterized tests run the same test with different inputs.

- @ParameterizedTest annotation.
- @ValueSource for simple values.
- @CsvSource for multiple args.
- Reduces code duplication.

> From JUnit 5 Jupiter.
> Improves test coverage with varied data.

---

### 24. What is Hamcrest?

> Hamcrest provides matchers for more readable assertions.

- assertThat(actual, matcher).
- Matchers like is(), contains().
- Better error messages.
- Integrates with JUnit.

> Extends basic assertions.
> Use for complex validations in Java tests.

---

### 25. What is PowerMock?

> PowerMock extends Mockito to mock statics, finals, constructors.

- For legacy code testing.
- Uses bytecode manipulation.
- @PrepareForTest annotation.
- Can be overused.

> Not needed for well-designed code.
> In Java, prefer redesign over PowerMock for testability.

---

### 26. What is Selenium?

> Selenium is a framework for automating web browser tests.

- WebDriver for browser control.
- Supports Java bindings.
- For UI and end-to-end tests.
- Integrates with JUnit/TestNG.

> Handles dynamic web elements.
> Essential for Java-based automation testing interviews.

---

### 27. What is Page Object Model (POM) in Selenium?

> POM organizes web elements and actions into page classes.

- Reduces duplication.
- Improves maintainability.
- Uses @FindBy annotations.
- Separates tests from locators.

> With PageFactory.
> Best practice for scalable Selenium tests in Java.

---

### 28. How do you handle waits in Selenium?

> Use explicit waits with WebDriverWait and ExpectedConditions.

- For elements to appear.
- Implicit wait for global timeout.
- FluentWait for custom conditions.
- Avoid Thread.sleep.

> Ensures reliable tests.
> Critical for asynchronous web apps in Java automation.

---

### 29. What is Cucumber?

> Cucumber is a BDD tool that runs plain-text feature files.

- Gherkin syntax: Given-When-Then.
- Step definitions in Java.
- Integrates with JUnit.
- For acceptance tests.

> Promotes collaboration.
> Use in Java for behavior-focused testing.

---

### 30. What are step definitions in Cucumber?

> Step definitions link Gherkin steps to Java code.

- Annotated with @Given, @When, @Then.
- Use regex for parameters.
- Execute test logic.
- Can share state with hooks.

> Keep them simple.
> Enables executable specifications in BDD.

---

### 31. What is a hook in Cucumber?

> Hooks run code before or after scenarios with @Before, @After.

- Setup/teardown.
- Tagged hooks for specific scenarios.
- Orderable.
- For browser open/close in Selenium.

> Improves test independence.
> Useful in Java for managing test environment.

---

### 32. What is shift-left testing?

> Shift-left moves testing earlier in the development cycle.

- Involves testers in requirements.
- TDD and BDD practices.
- Reduces late defects.
- Improves quality.

> Part of DevOps.
> In Java teams, encourages continuous testing.

---

### 33. What is continuous integration (CI) in testing?

> CI automatically builds and tests code on every commit.

- Tools like Jenkins, GitHub Actions.
- Runs unit/integration tests.
- Fast feedback.
- Prevents integration issues.

> Integrates with Maven.
> Essential for agile Java development.

---

### 34. What is a test pyramid?

> Test pyramid suggests more unit tests, fewer integration/UI tests.

- Base: Unit tests (fast, many).
- Middle: Integration (fewer).
- Top: UI/end-to-end (slow, few).
- Balances speed and coverage.

> Mike Cohn's concept.
> Guides efficient testing strategy in Java.

---

### 35. How do you test databases in Java?

> Use JdbcTemplate or JPA in integration tests.

- H2 in-memory database.
- @DataJpaTest annotation.
- Assert queries and data.
- Mock if unit testing.

> Ensures data persistence works.
> Critical for Spring Boot apps.

---

### 36. What is @MockBean in Spring Boot?

> @MockBean replaces a bean with a Mockito mock in tests.

- For integration tests.
- Stubs service calls.
- Verifies interactions.
- Auto-resets after test.

> Part of spring-boot-test.
> Isolates layers in Spring applications.

---

### 37. What is WireMock?

> WireMock mocks HTTP services for testing.

- Stubs API responses.
- Verifies requests.
- Standalone or embedded.
- JSON configuration.

> Great for microservices.
> In Java, use for external API testing without real calls.

---

### 38. What is contract testing?

> Contract testing verifies APIs match agreed contracts.

- Tools like Pact.
- Consumer-driven.
- Ensures compatibility.
- For distributed systems.

> Prevents integration failures.
> Important in Java microservices environments.

---

### 39. What is mutation testing?

> Mutation testing changes code slightly and checks if tests fail.

- Tools like PIT.
- Measures test effectiveness.
- Kills mutants.
- Improves test suite.

> Advanced quality metric.
> Use in Java to ensure strong tests.

---

### 40. What is exploratory testing?

> Exploratory testing is unscripted, learning while testing.

- Finds unexpected issues.
- Complements automated tests.
- Tester's expertise key.
- Time-boxed sessions.

> Not automated.
> Valuable in Java apps for usability and edge cases.

---

### 41. What is the Arrange-Act-Assert pattern?

> AAA structures tests: setup, execute, verify.

- Arrange: Prepare inputs/mocks.
- Act: Call method under test.
- Assert: Check results.
- Keeps tests clear.

> Standard in unit testing.
> Promotes readable Java tests.

---

### 42. How do you test asynchronous code in Java?

> Use CompletableFuture or Awaitility for waiting.

- assertAsync with timeouts.
- Mock callbacks.
- Verify eventual state.
- Avoid sleeps.

> Handles threads and futures.
> Essential for reactive Java applications.

---

### 43. What is a flaky test?

> A flaky test passes/fails inconsistently.

- Caused by timing, order, environment.
- Isolate and fix.
- Quarantine if needed.
- Use retries sparingly.

> Damages trust in suite.
> In Java, debug with logs and consistent setups.

---

### 44. What is acceptance testing?

> Acceptance testing verifies if the system meets business requirements.

- Often BDD with Cucumber.
- End-user perspective.
- Manual or automated.
- Before release.

> Part of UAT.
> In Java, ensures features work as expected.

---

### 45. What is regression testing?

> Regression testing re-runs tests to check new changes didn't break existing features.

- Automated suites.
- After bug fixes or features.
- CI/CD integration.
- Selective based on impact.

> Prevents old bugs returning.
> Crucial in evolving Java projects.

---

### 46. What is smoke testing?

> Smoke testing checks basic functionality after a build.

- Quick, high-level.
- Ensures stability.
- Subset of tests.
- Automated or manual.

> Like sanity check.
> In Java CI, runs first to gate further tests.

---

### 47. What is load testing?

> Load testing simulates many users to check performance.

- Tools like JMeter, Gatling.
- Measures response time.
- Finds bottlenecks.
- Not for functionality.

> Scalability assurance.
> Important for Java web apps under traffic.

---

### 48. What is security testing in Java?

> Security testing checks for vulnerabilities like injection, XSS.

- Tools like OWASP ZAP.
- Static analysis (SonarQube).
- Dynamic scanning.
- Secure coding practices.

> Follows OWASP top 10.
> Essential for protecting Java applications.

---

### 49. What is accessibility testing?

> Accessibility testing ensures apps are usable by people with disabilities.

- WCAG standards.
- Tools like Axe, WAVE.
- Screen reader compatibility.
- Keyboard navigation.

> Legal and ethical.
> In Java web, test with Selenium extensions.

---

### 50. What are best practices for writing tests?

> Write clear, independent tests; follow AAA; aim for high coverage; mock wisely.

- One assertion per test.
- Descriptive names.
- Run fast.
- Version control tests.

> Refactor tests too.
> In Java, these practices lead to reliable, maintainable test suites.

---

### 51. How do you integrate tests with Maven?

> Use surefire plugin for unit tests, failsafe for integration.

- mvn test command.
- Configure in pom.xml.
- Reports generation.
- Profiles for environments.

> Automates build lifecycle.
> Standard in Java projects for CI.

---

### 52. What is AssertJ?

> AssertJ provides fluent assertions for better readability.

- assertThat(actual).isEqualTo(expected).
- Chainable methods.
- Rich for collections, exceptions.
- Alternative to Hamcrest.

> Improves test expressiveness.
> Popular in modern Java testing.

---

### 53. What is REST Assured?

> REST Assured tests REST services with a fluent API.

- Given-when-then syntax.
- Validates JSON/XML.
- Authentication support.
- Integrates with JUnit.

> Simplifies API testing.
> Great for Java backend validation.

---

### 54. What is Karate?

> Karate is a BDD framework for API and UI testing.

- No Java code needed.
- Gherkin-like syntax.
- Built-in assertions.
- Parallel execution.

> Open-source.
> Useful for Java teams wanting simple automation.

---

### 55. What future trends in Java testing?

> AI-assisted testing, shift-right, containerized tests.

- More focus on observability.
- Integration with cloud.
- Low-code tools.
- Security in CI/CD.

> Evolving with Java 21+ features.
> Stay updated for interviews; mention virtual threads impact.
---

### 51.

>
---

### 52.

>
---

### 53.

>
---

### 54.

>
---

### 55.

>
---

### 56.

>
---

### 57.

>
---

### 58.

>
---

### 59.

>
---

### 60.

>
---

### 61.

>
---

### 62.

>
---

### 63.

>
---

### 64.

>
---

### 65.

>
---

### 66.

>
---

### 67.

>
---

### 68.

>
---

### 69.

>
---

### 70.

>
---

### 71.

>
---

### 72.

>
---

### 73.

>
---

### 74.

>
---

### 75.

>
---

### 76.

>
---

### 77.

>
---

### 78.

>
---

### 79.

>
---

### 80.

>
---

### 81.

>
---

### 82.

>
---

### 83.

>
---

### 84.

>
---

### 85.

>
---

### 86.

>
---

### 87.

>
---

### 88.

>
---

### 89.

>
---

### 90.

>
---

### 91.

>
---

### 92.

>
---

### 93.

>
---

### 94.

>
---

### 95.

>
---

### 96.

>
---

### 97.

>
---

### 98.

>
---

### 99.

>
---

### 100.

>
---