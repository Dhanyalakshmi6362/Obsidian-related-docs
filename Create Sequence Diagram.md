It helps to understand high-level interactions between the system by diagrams. 

**Let's understand this with an example of user signing up to a website/application:**

All sequence diagrams must have actors and participants. An actor represents a human/medium through which human requests, and a participant represents a process.

#### The user sign-up process works as follows:

1. The **user** accesses the **Sign Up Service** through their **browser** (the actor in this flow).
2. The **Sign Up Service** responds by sending back an HTML sign-up page to the **browser**.
3. The **user** fills out the sign-up form and submits it, sending their information back to the **Sign Up Service**.
4. The **Sign Up Service** validates the provided input.
    - If the input is invalid, it sends an error message back to the **browser**.
    - If the input is valid, it proceeds to the next step.
5. Upon valid input, the **Sign Up Service** sends a request to the **User Service** to create a new user account.
6. The **User Service** creates the user and responds with a `201 Created` status.
7. Finally, the **Sign Up Service** redirects the **browser** to the login page, indicating that the sign-up process was successful.


> [!NOTE]
> The key distinction between a domain (or class) diagram and a sequence diagram lies in their perspectives on system design. A domain diagram captures the **static structure** of the system, emphasizing the relationships among various entities. In contrast, a sequence diagram illustrates the **dynamic behavior** of the system, showing how objects interact in a defined sequence to accomplish specific tasks.

## Types of Interaction

In a sequence diagram, which illustrates the system’s behavior, interactions can be represented in two ways:

1. Synchronous calls: When participants are interacting, a response is required to proceed with the interaction.
	
		Symbol of interaction:  -->>
	
2. Asynchronous Calls: When participants are interacting, a response is not required for the interaction to continue. This type of call serves primarily to notify the other participant.

		Symbol of interaction:  --)


## Branching Logic

To accurately depict different paths in the workflow, branching logic is necessary. This logic allows the sequence diagram to show both the successful and unsuccessful paths of an interaction.

**Syntax:**

		alt description
			action
		else description
			action
		end

You can create multiple `else` conditions. Example syntax:

		alt description
			action
		else description1
			action
		else description2
			action
		end

## Add Note

To add additional context or emphasize a specific part of the sequence, we can use **notes**.

**Syntax**: 

	Note [Left|Right] of [Node]: Description

Here, "left" or "right" specifies whether the note should appear on the left or right side of the specified node.

**Example**: 

	Note left of sign-up: Sign-Up service

**Code:**

	---
	title: User Sign Up Flow
	---
	sequenceDiagram
		actor Browser
		participant Sign Up Service
		participant User Service
		participant Kafka
		Browser->>Sign Up Service: GET /sign_up
		Sign Up Service-->>Browser: 200 OK (HTML page)
		Browser->>Sign Up Service: POST /sign_up
		Sign Up Service->>Sign Up Service: Validate input	
		alt invalid input
			Sign Up Service-->>Browser: Error
		else valid input
			Sign Up Service->>User Service: POST /users
			User Service--)Kafka: User Created Event Published
			Note left of Kafka: other services take action based on this event
			User Service-->>Sign Up Service: 201 Created (User)
			Sign Up Service-->>Browser: 301 Redirect (Login page)
		end

![[seq-branch.png]]


## Activations

We can add activations to display the length of conversation to make the diagram even more readable.It can be achieved in two ways:

1. Use *activate & deactivate* keywords.
		Syntax: activate participant
			 deactivate participant
2. Use *+ & -* keywords 
		Syntax: +participant
			  -participant

## Annotation

Mermaid can provide automatic sequence numbering. This essentially
adds a number to each message on the diagram.It can be added just by mentioning **autonumber** below the type of diagram.

**Code:**

	---
	title: User Sign Up Flow
	---
	sequenceDiagram
		autonumber
		
		actor Browser
		participant Sign Up Service
		participant User Service
		participant Kafka
		
		Browser->>Sign Up Service: GET /sign_up
		activate Sign Up Service
		Sign Up Service-->>Browser: 200 OK (HTML page)
		deactivate Sign Up Service
		
		Browser->>+Sign Up Service: POST /sign_up
		Sign Up Service->>Sign Up Service: Validate input
		
		alt invalid input
		Sign Up Service-->>Browser: Error
		else valid input
		Sign Up Service->>+User Service: POST /users
		User Service--)Kafka: User Created Event Published
		Note left of Kafka: other services take action based on this event
		User Service-->>-Sign Up Service: 201 Created (User)
		Sign Up Service-->>-Browser: 301 Redirect (Login page)
		end
![[autonumber.png]]




