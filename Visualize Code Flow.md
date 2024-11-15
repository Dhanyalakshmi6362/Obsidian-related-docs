We can visualize the code using two types of diagram. To visualize the classes interaction we use **sequence diagram**. To visualize the dependencies between classes we prefer **class diagram**.

#### Lets understand classes interaction using Sequence Diagram

We need to follow same syntax as previous with few more additional syntax.

## Loops
One of the most common things to do in any programming language is to iterate over a piece of data, typically using a loop.

**Syntax:**

	loop
		action
	end

## Parallel process

So far, our sequence diagram is sequential. Each interaction in the sequence is happening one after the other, in a procedural manner. However, in the real world, that’s not always the case. Often, a process’s performance can be improved through parallelizing parts of the flow.

**Syntax:**

	par
		action
	end

**Code:**

	---
	title: POST /users Request Handling
	---
	sequenceDiagram
	autonumber
	participant UserController
	participant CreateUserService
	participant UserModel
	participant SendWelcomeEmailService
	participant Kafka
	UserController->>+CreateUserService: call
	CreateUserService->>UserModel: find_users_by_email
	UserModel-->>CreateUserService: array of Users
	loop
	CreateUserService->>CreateUserService: check_active_users
	end
	CreateUserService->>UserModel: create_user
	UserModel-->>CreateUserService: User
	par
	CreateUserService->>SendWelcomeEmailService: send_welcome_email
	SendWelcomeEmailService-->>CreateUserService: boolean
	CreateUserService->>Kafka: publish_user_created_event
	Kafka-->>CreateUserService: boolean
	end
	CreateUserService-->>-UserController: User
![[vis.png]]

