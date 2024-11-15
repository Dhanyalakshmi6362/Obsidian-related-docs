When considering changes to code or adding new feature first we need to know the dependencies, that's when we go for class Diagram to get all of this information.

Though sequence diagram shows the behaviour of the system how they interact but viewing dependency is not really possible. It shows only public methods called between classes,it doesn't shows the private classes called.

This class diagram is quite different from the one we initialled talked about,in the initial part it shows only the main objects/entities involved in the system & how they are related to each other. More like it gives static structure of the system. Whereas here, it shows how the classes in those entities are dependent on each other & also describes the methods & properties of a class.

## Define Classes

When we learnt about **Domain Diagram** we just stated the entity and it's relationship with other entity,but here we will define a class of that entity and define it's methods & parameters.

**Syntax:**

	class ClassName {
		-PropertyType propertyName
		+MethodName(MethodParamType methodParam) ReturnType
	}
Syntax itself describes how to define the class. Here **+ & -** indicates **public & private** respectively. It can be added as a prefix to  a PropertyType or MethodName.

## Show Dependency with Relationships

We can define dependency of a class using **..>** symbol pointing to the dependent.

**Code:**

	classDiagram
	class UserController {
	-CreateUserService _createUserService
	+UserController(CreateUserService createUserService)
	+Create(string email, string username) User
	}
	
	class CreateUserService {
	-UserModel _userModel
	-SendWelcomeEmailService _sendWelcomeEmailService
	-Kafka _kafka
	+CreateUserService(UserModel um, SendWelcomeEmailService es, Kafka k)
	+Call(CreateUserRequest createUserRequest) User
	-CheckActiveUsers(List~User~ users) bool
	}
	class UserModel {
	+FindUsersByEmail(string email) List~User~
	+CreateUser(string email, string username) User
	}
	class User {
	+int UserId
	+string Username
	+string Email
	}
	class SendWelcomeEmailService {
	+Call(User user) bool
	}
	class Kafka {
	+PublishUserCreatedEvent(User User) bool
	}
	UserController ..> CreateUserService: depends on
	CreateUserService ..> UserModel: depends on
	UserModel ..> User: depends on
	CreateUserService ..> SendWelcomeEmailService: depends on
	CreateUserService ..> Kafka: depends on


![[class-dependency 2.png]]

After analyzing this dependencies of classes we can add a feature or we can modify the existing code based on our needs.

**Code:**

	classDiagram
	class UserController {
	-CreateUserService _createUserService
	+UserController(CreateUserService createUserService)
	+Create(string email, string username) User
	}
	class CreateUserRequest {
	+string Email
	+string Username
	+Validate() bool
	}
	class CreateUserService {
	-UserModel _userModel
	-SendWelcomeEmailService _sendWelcomeEmailService
	-Kafka _kafka
	+CreateUserService(UserModel um, SendWelcomeEmailService es, Kafka k)
	+Call(CreateUserRequest createUserRequest) User
	-CheckActiveUsers(List~User~ users) bool
	}
	class UserModel {
	+FindUsersByEmail(string email) List~User~
	+CreateUser(string email, string username) User
	}
	class User {
	+int UserId
	+string Username
	+string Email
	}
	class SendWelcomeEmailService {
	+Call(User user) bool
	}
	class Kafka {
	+PublishUserCreatedEvent(User User) bool
	}
	UserController ..> CreateUserRequest: depends on
	UserController ..> CreateUserService: depends on
	CreateUserService ..> UserModel: depends on
	UserModel ..> User: depends on
	CreateUserService ..> SendWelcomeEmailService: depends on
	CreateUserService ..> Kafka: depends on

![[class-dependency2.png]]


