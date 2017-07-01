![alt text](https://github.com/raventid/avangarde/blob/master/misc/github/logo.jpg "avangarde project")
#

Component base, general purpose, declarative language.

Avangarde is a development platform and language inspired by different HDL langauges. It leverage the power of isolated components to build robust and scalabale abstractions.

At the moment Avangarde project in a stage of specification. We are trying to collect some ideas and drafts before starting to implement compiler. We believe that it will take less time and hassle to think, before do :)

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
  FindUser(login=login, user=user)
  IsTrue(a=user, out=isUser)
  Finish(flag=isUser)
  CheckPassword(user=user, password=password, out=out)
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
