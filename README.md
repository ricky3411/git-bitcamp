**Syntax**: Defines the rules for creating well-formed sentences in logic. Each logic system has its own syntax that dictates the structure of legal expressions.

**Logic**: A language with a syntax for specifying what is a legal expression in the language

- Semantics: associates elements of the language
- Inference rules: manipulating sentences in the language

- Knowledge base: a set of sentences in a formal language representing facts about the world
    - Logics are formal languages to represent information so conclusions can be drawn
- Entailment: one thing follows from another
    - KB |= ⍺
    - Knowledge Base entails sentence ⍺ meaning ⍺ is true in all worlds where KB is true

Propositional Logic

- Connectives
    
    ¬   :    not 
    
    ^    :    and 
    v   :    or 
    → :   implies 
    ↔  :   equivalent (if and only if)
    
- Well-Formed Formulas (WFF): syntactically correct expression that follows the rules of the language
    - A statement variable standing alone is a WFF
        - P
        - ~P

Models: Structured worlds with respect to which truth can be evaluated

- we say *m* is a model of a sentence *⍺* if ⍺ **is true in *m*
- *M(*⍺*)* is the set of all models of ⍺

Inference Soundness/Completeness

- Soundness: all derived conclusions are true
- Completeness: all true conclusions can be derived by the system
- KB ㅏ ⍺ means that ⍺ can be derived from KB

Horn Clauses

- Used to derive new facts from a set of Horn clauses and facts
- Can represent knowledge
- Definite clauses: Horn clause with exactly one positive literal

**Modus Ponens**: A rule of inference that states if `P → Q` and `P` are both true, then `Q` must also be true.

Forward Chaining

1. Fire any rule whose premises are satisfied in the KB
2. Add result to KB
3. Keep going until query is found
- Sound and Complete
- Data driven, automatic, unconscious processing
- May do lots of work that is irrelevent to the goal

Backward Chaining

1. Prove query by backward chaining
2. Check if query is known already
3. prove all premises of some rule concluding the query
- Goal driven, appropriate for problem solving
- Complexity is much less than linear size of KB

Different Types of Logic

- Propositional Logic
    - Proposition: A statement that can either be true or false
    - ex: P: The sky is blue, Q: It is Raining, P ^ Q: The sky is blue and it is raining
    - Assumes the world contains only facts
    - Syntax: P v (~Q ^ R)
- First Order Logic (extends propositional logic)
    - incorporates quantifiers and predicates
    - Assumes the world contains objects, relations, and functions
    - Syntax: ∀x (Cat(x) → Mammal(x))
    - Functions like Cat(x) represent mappings from objects to objects
        - ex: MotherOf(x) is a function that represents the mother of x
        - ex: ∀x (Cat(x) → Mammal(MotherOf(x))) is a function that represents the mother of any cat is a mammal
        - ex: ∃x (Student(x) ∧ EnrolledIn(x, Math101)) is a function that states there exists a student that is enrolled in math101

Resolution:

Proof procedure that involves repeatedly resolving the negation of a logical formula to derive contradictions. This indicates that the original formula is valid

- Creates a new clause when two or more clauses are combined

Unification: process to make different logical expressions identical by finding suitable substitutions
Rule 1: Two constants unify only if they are identical. So, `DAVID` and `DAVID` unify, but `DAVID` and `GEORGE` do not.

Rule 2: A constant and a variable can unify, with the variable taking the value of the constant. For example, `?x` and `DAVID` unify with the substitution `{DAVID / ?x}`.

Rule 3: Two variables can unify, with one variable taking the value of the other. For example, `?x` and `?y` unify with `{?y / ?x}` or 

`{?x / ?y}`.

Rule 4: Two functions unify if their names and number of arguments match, and their arguments can also be unified. For example:

- `Father(?x)` and `Father(DAVID)` unify with `{DAVID / ?x}`.

- Need to Unify to make these two expressions equal
    - `ANCESTOR(?x,Father(?x))`
    - `ANCESTOR(DAVID,GEORGE)`
- Constants:
    - DAVID
    - GEORGE
- Variables:
    - ?x
- Functions:
    - Father()
    - Ancestor()
    

Steps:

1. Start with top level function: 
- Since both top level functions are ANCESTOR, we proceed to unify
2. Unify first arguments:
- We have ?x and DAVID in first parameter. Constant and variable can unify, and we get {DAVID/?x}
3. Apply substitution to second argument:
- We can substitude DAVID in for ?x in the first expression to get Father(DAVID)
4. Unify second arguments:
- Need to unify Father(DAVID) and GEORGE. If Father(DAVID) returns GEORGE, then unification succeeds.

True → The unification is successful

Ontology: 

- Description of all objects and relationships that can exist

Semantic Network: Using graphs to represent knowledge through nodes and their connections

- Nodes represent categories or objects
- Connection between nodes represent relationships between nodes

![Screenshot 2024-11-04 at 10.55.57 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/50dddeca-460c-4c6a-92d7-3fe951e3f6a3/12c7ae5f-845b-4feb-88ea-656e80ed06df/Screenshot_2024-11-04_at_10.55.57_PM.png)

Planning

STRIPS Style Planning: formal language for representing planning problems

Components:

- States: represented by collections of facts, which are propositions that describe the world
    - ex: On(A,B) or Clear(A)
- Actions: defined with preconditions and effects
    - preconditions: conditions that must be true for the action to be applicable
    - effects: changes in the world state after action is performed
- Goals: desired state we want to achieve by applying actions

Progression Planninng: start from initial state and applies actions in sequence, moving forward through states until reaching the goal

- Steps:
    - Start at initial state
        - define initial conditions
    - Apply actions
        - sequentially apply actions whose preconditions are met by current state
    - Generate new states
        - each action creates a new state by adding or removing facts based on action performed
    - Repeat until goal
        - continue applying actions and generating new states until goal state
- Advantages:
    - Intuitive as it resembles how people naturally think about processing
    - Effective when there is a clear path
- Disadvantages:
    - Can lead to large search space if many actions are possible → computationally expensive
    - Often generates irrelevant actions that do not contribute to reaching the goal
- Progession Planning is useful for domains where initial conditions and direct paths to goals are known and straightforward

Regression Planning: starts from the goal and works backward to determine which actions could have produced that goal state

- Steps:
    - Begin with the goal
        - define conditions of final state
    - Identify Relevant Actions
        - look for actions that can produce those goal conditions in their effects
    - Determine Preconditions
        - for each selected action, work backward to identify the preconditions needed to make this action applicable
    - Repeat until final state
        - continue applying this process until reaching a state that matches initial conditions
- Regression Planning is useful when goals are specific as it only considers actions directly leading to the goal, thus narrowing down the search space

Sussman Anomoly: 

- Goals interfere with each other in a such a way that achieving one undoes progress of another
- Sussman Anomoly is an example of Goal Interactions: Occur when achieving one goal interferes with or undoes another.

Linear vs. Nonlinear Planning

Linear Planning/Total Order Planning:

- Creating sequence of actions that must be executed in a specific order, where each action is dependent on the completion of the previous action
- Fixed sequence

Nonlinear Planning/Partial Order Planning:

- Allows for the execution of actions in a flexible order, where multiple actions can occur simultaneously as long as preconditions are met
- Parallel and flexible action sequences

Least Commitment: practice of avoiding premature commitments

- defering decisions so we can visit more states

Hierarchical Planning: organizes complex planning problems into simpler, manageable subtasks

- Hierarchical Decomposition: complex task or goal becomes divided into subtasks
    - each subtask can then be broken down into smaller tasks, which eventually forms a hierarchy of tasks that represent a complete plan

Knowledge Graph: Combination of ontology and data in a structured format (triples)

- Relationships are encoded as triples in knowledge graphs (e.g., `isa`, `subset_of`)
    - (cat, isa, animal)

- **Frame Problem**: Describes the difficulty in specifying what doesn’t change after an action without having to state every irrelevant fact.
- **Qualification Problem**: Deals with the challenge of specifying all conditions necessary for an action.
- **Ramification Problem**: Concerns the indirect effects of actions, which must also be represented in the model.

Temporal Constraints

Time:

- Actions executed in parallel take the time of the longest action
- time never goes backwards
