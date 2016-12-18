# React vs Angular 2
[Angular 2 vs React: The Ultimate Dance Off](https://medium.com/javascript-scene/angular-2-vs-react-the-ultimate-dance-off-60e7dfbc379c#.8bitae6qt)

#### Common:
Almost all the popular front-end frameworks support custom components
Performance was not a big problem with either
You should avoid DOM updates when you can, avoid deep state iteration if you can, avoid excessive creating / tearing down objects and components, etc… 

#### For react:
[MV* and 2-way data binding](https://medium.com/javascript-scene/the-best-way-to-learn-to-code-is-to-code-learn-app-architecture-by-building-apps-7ec029db6e00#.a36q0yx92): With 2-way data binding changes to the view are directly reflected in the model without going through the controller. 

#### For Angular 2:
TypeScript: 
- Type correctness does not guarantee program correctness.TypeScript can only detect a class of bugs, however, it would increase the code complexity.
- Type inference 
- Might increase productiveness for some developer, but it takes time and effort to set it up.
Dependency injection(write a function that takes your dependency, instead of importing your dependencies)

