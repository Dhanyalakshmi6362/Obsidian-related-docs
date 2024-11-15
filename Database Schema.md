The domain is responsible for representing the core concepts whereas the database layer is there to store state in a robust, performant manner. The domain layer doesn’t care about how quickly a given row can be looked up from the database, but the database layer certainly does.Here entity means tables.

## Entity Relationship Diagrams
A common diagram for designing database schemas is called an entity relationship diagram (ERD). It is also called snapshot diagrams because it gives the snapshot of the current databse structure.

It can be utilised:
* When writing an architecture decision record (ADR) for a brand-new service to represent how the databse looks like.
* When making significant schema changes to an existing service.
* When making small schema changes.

#### Define Entity

**Syntax:**

	erDiagram 
		Entity_Name {
				datatype parameter
				....
		}

#### Relate Entities

In ERD their are four different cardinalities to relate entities,they are:

1. One-to-many  -> Symbol: }| or |{
2. Zero-to-many -> Symbol: }o or o{
3. Zero-or-one -> Symbol: o|
4. exactly one -> Symbol: ||

**Syntax:**

	ENTITY1 CARDINALITY--CARDINALITY ENTITY2:Description

Cardinality for a given entity on the opposite side to the entity itself.
Therefore, in the syntax format, the cardinality for ENTITY1 is after the two hyphens.

**Code:**

	erDiagram
		TITLE {
			int title_id
			int type_id
			string name
			datetime release_date
		}
		TITLE_TYPE {
			int type_id
			string type
		}
		GENRE {
			int genre_id 
			string name
		}
		SEASON {
			int season_id 
			int title_id 
			int season_number
			date release_year
		}
		REVIEW {
			int review_id 
			int title_id 
			int season_id 
			string review_by
			datetime review_date
			string review_text
		}
		TITLE_GENRE {
			int title_id
			int genre_id
		}
		TITLE }|--|| TITLE_TYPE: has
		TITLE ||--o{ TITLE_GENRE: "belongs to"
		TITLE_GENRE }o--|| GENRE: references
		REVIEW }o--o| TITLE: "made against"
		REVIEW }o--o| SEASON: "made against"
![[erd 1.png]]


