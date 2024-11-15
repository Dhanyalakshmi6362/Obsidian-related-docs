To create a domain document, it’s essential to understand different types of relationships between entities, where an entity represents an object or concept within the system.

## Types of Relationships

1. **Association Relationship**  
    This is the loosest relationship type in UML. Entities in an association can exist independently. However, one entity may still reference another.
    
    - **Representation**: `--` (two hyphens)
    - **Example**: _Title_ and _Genre_—both can exist independently, but titles may be listed under a genre.<br><br>
2. **Composite Relationship**  
    Known as a "composition," this relationship is strong and represents a parent-child dependency. If the parent is removed, the child entities are also deleted.
    
    - **Representation**: `*--` (asterisk with two hyphens) <br><br>
3. **Aggregate Relationship**  
    Similar to a parent-child relation but less rigid than a composite relationship. Here, child entities can exist without the parent.
    
    - **Representation**: `o--` (o with two hyphens)<br><br>

4. **Inheritance Relationship**
	This exhibits ***is-a*** relationship where one entity inherits few properties from other. 

	* **Representation:** --|> <br><br>

Understanding these relationships and their UML representations enables us to create structured domain documents effectively.

#### Let's consider an example of movie to understand these relationships:

A movie/show consists of several elements, such as a title, genre, season, episode, cast, and actor. It also allows viewers to leave reviews.This can be a TV-Show,Short film or film.


**Code:**

			classDiagram
				Title -- Genre
				Title *-- Season
				Title *-- Cast
				Title o-- Actor
				Title *-- Review
				
				Season *-- Episode
				TVShow --|> Title
				Short Film --|> Title
				Film --|> Title

In this diagram:

- The first line indicates it is a class diagram.<br><br>
- **Title & Genre** have an *Association relationship*, meaning they can exist independently of one another. <br><br>
- **Title & Season**, **Title & Cast**, and **Title & Review** have a *Composite relationship*. If a title is cancelled, the associated season, cast, and reviews for that title will also be removed.<br><br>
- **Season & Episode** also have a *Composite relationship*, as episodes depend on the season they belong to.<br><br>
- **Title & Actor** have an *Aggregate relationship*, meaning that an actor can exist independently of the title. Even if the title is cancelled, the actor can continue to exist.<br><br>
-Title has an inheritance relationship with TVShow, ShortFilm, and Film, as these are all specific types of a general Title. In other words, TVShow, ShortFilm, and Film are specialized categories or subtypes of Title.


![[Movie 1.png]]


* Association relationship has a solid line to connect entities.
* Composite relationship has a solid diamond on the line connecting two entities.
* Aggregate relationship has a empty diamond on the line connecting two entities.
* Inheritance relationship has an empty arrows on the line connecting two entities.

## Add Description 

We can add description of the relationship between Entities just by using : (colon) after defining the relationship of entities.

Code:

			classDiagram
				Title -- Genre: is associated with
				Title *-- Season: has
				Title *-- Cast: has
				Title o-- Actor: has
				Title *-- Review: has
				
				Season *-- Episode: contains
				TVShow --|> Title: implements
				Short Film --|> Title: implements
				Film --|> Title: implements



## Add Title

We can add title to the diagram using:

**Code:**

			---
			title: A Movie
			---
			classDiagram
				Title -- Genre: is associated with
				Title *-- Season: has
				Title *-- Cast: has
				Title o-- Actor: has
				Title *-- Review: has
				
				Season *-- Episode: contains
				TVShow --|> Title: implements
				Short Film --|> Title: implements
				Film --|> Title: implements
			
![[movie-des-title.png]]

## Add Links

We can add links to entities, so when the entity is clicked, it will redirect you to a specified website or external documentation.

**Syntax:**

	link Entity_Name "URL" _blank
	
**Example:**
	
	link Title "https://www.google.com/" _blank

link tells Mermaid we want to create the link, Title is the identifier of the node, followed by the URL.

This completes Domain Documentation diagram.

