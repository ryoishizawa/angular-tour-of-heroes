# Overview of Angular Test

## Why test code
* To find regression because of your change
  - Regression may happen from new feature you add, new library, modification of library and others.
  - To realize them faster, you need to use auto-testing method
* To refactor code in the future
  - Test code can represent the specification of your code
* To improve the design of implementation
  - When you write test, you need to re-think the design of your code
* Reduce Cost

> You can say that all their benefits come at a great cost: TIME, but this is completely false. All the time that using unit testing may cost you is going to be small compared to the time they are going to save you later when you are introducing new features or making any refactors. The time spent resolving bugs is going to be drastically smaller than if you are not using unit testing. <br>
> (from [Angular: Unit Testing Jasmine, Karma (step by step)][0ab7fa8b])

## Test type
There are 2 ways of testing for Angular:
* Unit test
* E2E test(End-To-End test)

We will use both Unit test and E2E test, but **mainly we will work on Unit test**.

It is said that E2E test is too high cost and difficult to maintain. Here are the basic problems of E2E test from [Angular Testing Guide][436542a7],
* E2E tests are great for high-level validation of the entire system. But they can't give you the comprehensive test coverage that you'd expect from unit tests.
* E2E tests are difficult to write and perform poorly compared to unit tests. They break easily, often due to changes or misbehavior far removed from the site of breakage.
* E2E tests can't easily reveal how your components behave when things go wrong, such as missing or bad data, lost connectivity, and remote service failures.
* E2E tests for apps that update a database, send an invoice, or charge a credit card require special tricks and back-doors to prevent accidental corruption of remote resources. It can even be hard to navigate to the component you want to test.

You can refer to [Google Testing Blog][06d89d4d] to understand more detail about the demerit of E2E testing.

## Framework
For Unit Test, we use
* **Jasmine**: Testing framework
* **Karma**: Task runner for the tests

For E2E, we use
* **Protractor**

## (WIP) How Karma works
* The way of compiling is totally different from Angular. even though it works well usually, you may not be able to compile in testing.
* https://github.com/webpack-contrib/karma-webpack
* (**[TODO]** Write detail later...)

# (WIP) Angular Unit Test Method

## Setup
1) Run `ng test --watch-false` (if you want to check the result in browser, remove `--watch-false` option)

2) You may get some error with the test files you generated. The following is the things you may need to do.

3) Add `CUSTOM_ELEMENTS_SCHEMA` in `TestBed.configureTestingModule#schemas`. (**[TODO]** How does this work?)

```
import { CUSTOM_ELEMENTS_SCHEMA } from '@angular/core';

beforeEach(async(() => {
  TestBed.configureTestingModule({
    schemas: [ CUSTOM_ELEMENTS_SCHEMA ], // HERE!
    declarations: [ SidemenuComponent ]
  })
  .compileComponents();
}));
```

If you don't write this, you will get the error like this:

```
Error: Template parse errors:
Can't bind to 'options' since it isn't a known property of 'floating-action-button'.
...
...
```

4) To resolve dependencies, add the services which you use in `TestBed.configureTestingModule#providers`.

```
beforeEach(async(() => {
  TestBed.configureTestingModule({
    declarations: [ ComponentToTest ],
    providers: [ MyService ] // HERE!
  })
  .compileComponents();
}));
```

## General
1) Use `expect(actual).toBe(expected)` method which is commonly used in Jasmine framework.

Here is the very basic example,
```
it('checkDisable works', () => {
  // 'component' variable should be generated when you generate files with 'ng generate' command
  component.checkDisabled();
  // Let's say checkDisabled() method change 'backDisabled' to be false
  expect(component.backDisabled).toBe(false);
});
```

## Testing with `EventEmitter`
1) Suppose you're implmenting like this:

```
@Output() isNext = new EventEmitter<number>();
...

onBackButtonClick() {
  this.isNext.emit(this.index);
}
```

2) Subscribe variables which is for `EventEmitter` and you can check whether emitting event works correctly.

```
it('onBackButtonClick test', () => {
  component.isNext.subscribe(x => {
    // HERE write your test
  });
  component.onBackButtonClick();
});
```

## Testing with private method
1) (Write later)

## Testing with `RouterLink`
1) To fix the initialization error, add `RouterTestingModule` in `TestBed.configureTestingModule#imports`.

```
import { RouterTestingModule } from '@angular/router/testing';

beforeEach(async(() => {
  TestBed.configureTestingModule({
    imports: [ RouterTestingModule ], // HERE!
    schemas: [ CUSTOM_ELEMENTS_SCHEMA ],
    declarations: [ SidemenuComponent ]
  })
  .compileComponents();
}));
```

2) (Write later)


---
## Reference
* [Angular Testing Guide][436542a7]
* [Google Testing Blog: Just Say No to More End-to-End Tests ][06d89d4d]
* [Angular — Testing Guide (v4+)][6cabc847]
* [Angular: Unit Testing Jasmine, Karma (step by step)][0ab7fa8b]
* [Angular component testing with routerLink and routerOutlet][7a3c95df]

  [436542a7]: https://angular.io/guide/testing "Angular Testing Guide"
  [06d89d4d]: https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html "Google Testing Blog: Just Say No to More End-to-End Tests"
  [6cabc847]: https://medium.com/google-developer-experts/angular-2-testing-guide-a485b6cb1ef0 "Angular — Testing Guide (v4+)"
  [0ab7fa8b]: https://medium.com/frontend-fun/angular-unit-testing-jasmine-karma-step-by-step-e3376d110ab4 "Angular: Unit Testing Jasmine, Karma (step by step)"
  [7a3c95df]: https://kirjai.com/ng2-component-testing-routerlink-routeroutlet/ "Angular component testing with routerLink and routerOutlet"
