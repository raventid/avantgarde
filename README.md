![alt text](https://github.com/raventid/avangarde/blob/master/misc/github/logo.png "avangarde project")
#

## Note: project stalled until late 2018.

Component based, general purpose, declarative language.

Avangarde is a development platform and language inspired by different HDL langauges. It leverage the power of isolated components to build robust and scalabale abstractions.

At the moment Avangarde project in a stage of specification. We are trying to collect some ideas and drafts before starting to implement compiler. We believe that it will take less time and hassle to think, before do :)

We are planning to write compiler in Haskell and use LLVM as our backend optimizer. If you have any design suggestions for the language, feel free to open up an issue. Some of the specs might be out of date, so be careful.

Spec period will end in the late 2018 and we'll start to tweak a draft compiler. Stay tuned :)

### Why?
Aren't you tired about same problems you see everywhere? How to test my code? How to organize my project structure? How to write code? What abstraction to choose, what style of coding? How to make my project comprehensible for other coders?

Avantgarde provides an opinionated approach to sustainable development for medium sized software projects. It's a mixture of the best things author have seen in hardware description languages, general purpose programming languages(Ruby, Java, C#, Haskell, Ocaml, F#, Clojure) and different frameworks and approaches to build software.

Avantgarde simplifies things dramatically and you will never need anything like AbstractFactory, IOC-container, Monad or MVC.

### How?
The only thing Avantgarde gives you is Component, so think about it as about language built for COP (component oriented programming). Your task as a software developer with Avantgarde is to craft components one by one and to wire them together with a purpase to reach required functionality. Despite the fact Avantgarde will have higher-order module system, which will allow you to typecheck your code in compile time and which will act as IOC-container in the same time, it's not what you should think about - you should only craft your components.

You can learn more about module system ideas here:

https://people.mpi-sws.org/~rossberg/papers/Rossberg%20-%201ML%20--%20Core%20and%20modules%20united%20[JFP].pdf

```
Package: User/Authorization

Component: User

Input: login : String, password : String
Output: exists : Boolean

Functionality:
  CheckUserCredentials(login=login, password=password, out=exists)
```

```
Package: User/Authorization

Component: CheckUserCredentials

Input: login : String, password : String
Output: out : Boolean

Functionality:
  FindUser(login : String = login : String, user : Boolean = user? : Boolean)
  IsTrue(a : Boolean = user? : Boolean, out : User = user : User)
  CheckPassword(user : User = user : User, password : String = password : String, out : Boolean = out : Boolean)
```

A lot of programming tasks require you to use some kind of data structures. Avangarde provides a consistent way to create data structures. 

```
Package: User

Structure: User

Fields: 
  login : String, -- This comma is not required. New line is a hint for compiler, that expression is completed.
  password : String

Functionality:
  Eat(food : Food =)
  Sleep(bed : Bed =)
```

Highly encapsulated Avangarde modules might be imported to your component:

```
Package: User

Structure: User

Dependencies:
  User/Payments/CreditCard -- concrete component
  User/Orders/* -- everything from Orders package
  -- User/Payments/CreditCard As CC -- oops, it's not possible, you must not rename component!
  

Fields: 
  login : String, -- This comma is not required. New line is a hint for compiler, that expression is completed.
  password : String

Functionality:
  Eat(food : Food =)
  Sleep(bed : Bed =)
```

TODO: Parallelism and concurrency described with components.

Current open questions:

1) After some consideration typeclasses aka Haskell class looks like a natural way to handle some actions on components. The problem is that it defeats a part of original idea about language semantics.

2) Type system is very unstable even conseptually. Typeclasses? Traits? Linear types? The only embraced thing is that typing is static, with inference.

3) Execution based on HDL circuits is very slow. It's impossible to write a programm using this approach, so we have to either cheet and implement every low-level operation in another language (or subset of avangarde) or accept performance penalty for every action and find the solution(compiler has to know how to take circuits and transform code based on them into general performant IR).

```
Package: User/Authorization

Component: User

-- we can use typeclass when we do not care about some specific type:
Input: login : String, password : String, Enum(a) => user_number : a
Output: exists : Boolean

Functionality:
  CheckUserCredentials(login=login, password=password, user_number=user_nubmer, out=exists)
```
