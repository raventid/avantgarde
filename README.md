# avangarde
Component base, general purpose, declarative language.

Avangarde is a development platform and language inspired by different HDL langauges. It leverage the power of abstract components to build
robust and scalabale abstractions.

```
Package: User/Authorization

Component: User

Input: login, password
Output: exists

Functionality:
  CheckUserCredentials(login=login, password=password, out=exists)
```

```
Package: User/Authorization

Component: CheckUserCredentials

Input: login, password
Output: out

Functionality:
  FindUser(login=login, user=user)
  IsTrue(a=user, out=isUser)
  Finish(flag=isUser)
  CheckPassword(user=user, password=password, out=out)
```
