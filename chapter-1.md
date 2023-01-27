- Every programming language has the following mechanisms for instructing computers to perform tasks: 
	1. **Primitive expressions**: the simplest entities a language is concerned with 
	2. **Means of combination**: the mechanism for creating compound elements from simpler ones
	3. **Means of abstraction**: the mechanism for naming and manipulating compound elements 
- Expressions which represent numbers can refer to a single number value or a mathematical expression which yields a single number
- We use names to refer to computational objects. These names are called `variables`, and the object is the `value`
- The `global environment` refers to the memory where the interpreter keeps track of name-object pairs 
- A goal of this chapter is learning how to think procedurally, in other words, thinking through how the computer will evaluate what is described in code 
- A `recursive` evaluation rule means that as one of the steps, the rule will call itself 
- `Tree accumulation` is the idea that values will percolate upward as the process is evaluated 
- `Special forms` bypass normal evaluation rules, for example `Define`
- `Procedure definitions` are an abstraction technique where an operation is defined and referred to as a unit 
- **Question**: what is a `compund procedure` versus a `primitive procedure`? **Answer:** compound procedures use procedure definitions and primitive procedures use tooling built into the interpreter  
- The  `Substitution model` of procedure application is: Evaluate the body of the procedure with each formal parameter replaced by the corresponding argument 
	- This is not how the interpreter actually works, but is the simplest way to reason about evaluating a compound procedure 
- In `normal-order` evaluation, the interpreter will first evaluate the operator and operands and then apply the resulting procedure to the resulting arguments (aka "fully expand and then reduce")
- In `applicative-order` evaluation, the interpreter will not evaluate the operands until their values are needed  (aka "evaluate the arguments and then apply")
- Both computer and mathematical procedures are concerned with specifying a value as determined by one or more parameters, but computer procedures must also be effective 
- `Procedural abstraction` means that a user does not need to know how a procedure is implemented in order to use it 
- By studying typical patterns of process evaluation, we can begin to understand the overall impact of a program's construction:
	1. Linear Recursion (process)
		- Process builds up a chain of deferred operations 
		- Contraction occurs as the operations are performed 
		- A recursive process is different from a recursive procedure
		- The amount of space and number of steps will grow linearly with the input 
	2. Linear Iteration (process)
		- at each step, keep track of the current state in a fixed number of variables 
		- define a fixed rule which describes how the state variables are update as the process moves from state to state and the end state under which the process terminates 
		- The number of steps will grow linearly with the input and the amount of space is constant
	3. Tree Recursion (process)
		- Process builds up branches at each level 
		- The number of steps grows exponentially with the input but the amount of space requires grows linearly 
		- Useful for operating on hierarchically structured data 
- `Order of growth` can be used to obtain a measure of the resources required by a process as the inputs get larger 
- `Higher-order procedures` are a powerful abstraction mechanism which refers to creating procedures which manipulate procedures 
- Methods of creating higher-order procedures include: 
	1. Procedures as arguments 
		- A procedure is defined
		- The procedure is passed into another procedure to have the specified effect
	2. Constructing procedures using `Lambda`
		- `lambda` is a special form which creates procedures 
		- A `lambda` expression can be used anywhere you would normally use a procedure name 
		- `let` is syntactic sugar on top of `lambda` which allows you to define local variables within an inline procedure 
	3. Procedures as general methods
		- The method of computation is independent of the particular functions involved 
	4. Procedures as returned values 
		- Allows for chained construction 
- In a programming language, elements with `first-class` status have special rights and privileges, such as: 
	- They may be named by variables 
	- They may be passed as arguments to procedures 
	- They may be returned as the results of procedures 
	- They may be included in data structures 
