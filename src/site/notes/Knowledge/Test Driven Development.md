---
{"dg-publish":true,"permalink":"/knowledge/test-driven-development/","tags":["testing","unit-testing","#tdd"]}
---

---
## Red, Green, Refactor
> *[Guidelines for Test-Driven Development \| Microsoft Learn](https://learn.microsoft.com/en-us/previous-versions/aa730844%28v%3Dvs.80%29)*

The motto of test-driven development is "Red, Green, Refactor."

- Red: Create a test and make it fail.
- Green: Make the test pass by any means necessary.
- Refactor: Change the code to remove duplication in your project and to improve the design while ensuring that all tests still pass.

The Red/Green/Refactor cycle is repeated very quickly for each new unit of code.

1. Understand the requirements of the feature that you are working on.
2. **Red**: Create a test and make it fail.
    1. Write a unit test that won't even compile.
    2. Create the new production code stub. 
    3. Run the test. It should compile but fail.
3. **Green**: Make the test pass by any means necessary.
    1. Write the production code to make the test pass. Only write as much code as is required for the test to pass. If you want to write more, a new test is required.
    2. Optional: hardcode the results first to ensure that the tests are correct.
    3. When the test passes, run all tests up to make sure everything still works.
4. **Refactor**: Change the code to remove duplication in your project and to improve the design while ensuring that all tests still pass.
    1. Remove duplication caused by the addition of the new functionality.
    2. Make design changes to improve the overall solution.
    3. Rerun all the tests to ensure that they all still pass.
5. Repeat the cycle. Each cycle should be very short, and a typical hour should contain many Red/Green/Refactor cycles.

## The three laws of TDD
>*[TheThreeRulesOfTdd](http://butunclebob.com/ArticleS.UncleBob.TheThreeRulesOfTdd)*

Uncle Bob describes TDD with the following rules:
1. You are not allowed to write any production code unless it is to make a failing unit test pass.
2. You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures.
3. You are not allowed to write any more production code than is sufficient to pass the one failing unit test.

> You must begin by writing a unit test for the functionality that you intend to write. But by rule 2, you can't write very much of that unit test. As soon as the unit test code fails to compile, or fails an assertion, you must stop and write production code. But by rule 3 you can only write the production code that makes the test compile or pass, and no more.

This results in very small iterations. He states that new tests should be added at least every 10 minutes.

## The Benefits of TDD
> *[Guidelines for Test-Driven Development \| Microsoft Learn](https://learn.microsoft.com/en-us/previous-versions/aa730844%28v%3Dvs.80%29)*

- The suite of unit tests provides constant feedback that each component is still working.
- The unit tests act as documentation that cannot go out-of-date, unlike separate documentation, which can and frequently does.
- When the test passes and the production code is refactored to remove duplication, it is clear that the code is finished, and the developer can move on to a new test.
- Test-driven development forces critical analysis and design because the developer cannot create the production code without truly understanding what the desired result should be and how to test it.
- The software tends to be better designed, that is, loosely coupled and easily maintainable, because the developer is free to make design decisions and refactor at any time with confidence that the software is still working. This confidence is gained by running the tests. The need for a design pattern may emerge, and the code can be changed at that time.
- The test suite acts as a regression safety net on bugs: If a bug is found, the developer should create a test to reveal the bug and then modify the production code so that the bug goes away and all other tests still pass. On each successive test run, all previous bug fixes are verified.
- Reduced debugging time!
