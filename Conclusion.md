Below tabular column shows the symbol used in different diagrams to explain the relationship between entities and interaction between them.

| Model               | Relationship/Interaction | Symbol                         | Diagram Type             |
| ------------------- | ------------------------ | ------------------------------ | ------------------------ |
| Domain/classDiagram | Association Relationship | --                             | **![[association.png]]** |
| Domain/classDiagram | Composite Relationship   | *--                            | ![[composite.png]]       |
| Domain/classDiagram | Aggregate Relationship   | o--                            | ![[aggregate.png]]       |
| Domain/classDiagram | Inheritance Relationship | --\|>                          | ![[inheritance.png]]     |
|                     |                          |                                |                          |
| Sequential Diagram  | Synchronous Calls        | -->>(Reception) & ->>(Request) | ![[sync-seq.png]]        |
| Sequential Diagram  | Asynchronous Calls       | --)                            | ![[async-seq.png]]       |
|                     |                          |                                |                          |
| Database Schema     | One-to-many              | \|\|--\|{                      | ![[one.png]]             |
| Database Schema     | zero-to-many             | \|\|--o{                       | ![[zero.png]]            |
| Database Schema     | Zero-or-One              | }o--o\|                        | ![[zo.png]]              |
|                     |                          |                                |                          |
| Class               | Depedency                | ..>                            | ![[cd.png]]              |
|                     |                          |                                |                          |
| C4                  | Synchronous Calls        | --Text-->                      | ![[c4.png]]              |
| C4                  | Asynchronous Calls       | ..Text..>                      | ![[asyn-c4.png]]         |
