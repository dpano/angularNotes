# Angular Unit testing

### Testing with mocks and spies [link](https://codecraft.tv/courses/angular/unit-testing/mocks-and-spies/#_learning_objectives)
- fake classes
- overriding functions
- using a real instance using a spy

Testing with real instances is resulting in tight coupling and brittle code.

### Angular Test bed [Link](https://codecraft.tv/courses/angular/unit-testing/angular-test-bed/#_learning_objectives)
1. fixture is a wrapper for the compononent ant its template
2. We create an instance of a component fixture through the TestBed, this injects the AuthService into the component constructor.
3. We can find the actual component from the componentInstance on the fixture.
4. We can get resolve dependencies using the TestBed injector by using the get function.

We will continue to use ATB for the rest of this section because:
- It allows us to test the interaction of a directive or component with it’s template.
- It allows us to easily test change detection.
- It allows us to test and use Angulars DI framework,
- It allows us to test using the NgModule configuration we use in our application.
- It allows us to test user interaction via clicks & input fields

### Angular Change detection [Link](https://codecraft.tv/courses/angular/unit-testing/change-detection/#_learning_objectives)

Every time that we change a property of the component angular is not updating the view directly. We have to invoke changeDetection() method.

1. There are imported a few more classes that are needed when interacting with a components view, **DebugElement** and **By**.
2. We have another variable called el which holds something called a **DebugElement**.
3. We store a reference to a DOM element in our **el** variable.

A **DebugElement** is a wrapper to the low level DOM element that represents the components view, via the debugElement property.

### Testing asynchronous Code [Link](https://codecraft.tv/courses/angular/unit-testing/asynchronous/#_learning_objectives)

If the code we are testing is asynchronous then we need to take this into account when writing our tests.

There are three mechanisms we can use.
- The **jasmine done function** and spy callbacks. We attach specific callbacks to spies so we know when promises are resolves, we add our test code to thos callbacks and then we call the done function. This works but means we need to know about all the promises in our application and be able to hook into them.
- We can use the **Angular async and whenStable functions**, we don’t need to track the promises ourselves but we still need to lay our code out via callback functions which can be hard to read.
- We can use the Angular **fakeAsync and tick functions**, this additionally lets us lay out our async test code as if it were synchronous.

### Angular dependency injection [Link](https://codecraft.tv/courses/angular/unit-testing/dependency-injection/#_learning_objectives)
We can resolve dependencies in our tests using a number of methods.

We can resolve using the the test bed itself, usually in the beforeEach function and store the resolved dependencies for use in our test specs.

We can resolve using the inject function at the start of each test spec.

We can also override the default providers for our components using the TestBed.

We can then also use the components child injector to resolve tokens.

### Testing components [Link](https://codecraft.tv/courses/angular/unit-testing/components/#_learning_objectives)
We can test inputs by just setting values on a components input properties.

We can test outputs by subscribing to an EventEmitters observable and storing the emitted values on local variables.

In combination with the previous lectures and the ability to test inputs and outputs we should now have all the information we need to test components in Angular.

In the next lecture we will look at how to test Directives.


