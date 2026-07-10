`[ ]`    // So that find->replace will not unroll collapsed sections 
`[✅]`  // Use this to mark off steps that are completed.  

# **TITLE**

## Problem Statement

## Objectives

## Expected Outcome

# Instructions for Agent
* `.github/instructions/*.instructions.md` for repo standards and requirements.
* `.cursor/commands/*.prompt.md` for task-specific direction. 

# Work Breakdown Structure

* **TITLE OF SPRINT** 

## Name of Workstream 
* `[ ]`   `[path]/[function]` **Descriptive explanatory title**

  * `[ ]`   `objective`
    * `[ ]`   Define the *problem being solved* (not the solution)
    * `[ ]`   Separate:
      * Functional goals (what must happen)
      * Non-functional constraints (performance, reliability, etc.)
    * `[ ]`   Each goal is atomic and testable

  * `[ ]`   `role`
    * `[ ]`   Declare the node’s role in the system (domain/app/port/adapter/infra)
    * `[ ]`   Explain *why this role is appropriate*
    * `[ ]`   Identify what this node must NOT do (out-of-scope responsibilities)

  * `[ ]`   `module`
    * `[ ]`   Define the bounded context this node belongs to
    * `[ ]`   List what concepts/data belong inside vs outside this boundary
    * `[ ]`   Each boundary rule is explicit and reviewable

  * `[ ]`   `deps`
    * `[ ]`   For each dependency:
      * Provider (node or external package)
      * Layer classification
      * Direction (why allowed)
      * Purpose (what capability is needed)
    * `[ ]`   Confirm:
      * No reverse dependencies
      * No lateral layer violations

  * `[ ]`   `context_slice`
    * `[ ]`   Define the **minimal interface required** from each dependency
    * `[ ]`   Specify injection shape (pure interface, no concrete types)
    * `[ ]`   Confirm:
      * No over-fetching of dependency surface
      * No hidden coupling

  * `[ ]`   `function.interface.test.ts`
    * `[ ]`   Define:
      * Valid cases (must pass)
      * Invalid cases (must fail)
    * `[ ]`   Include edge cases and boundary values
    * `[ ]`   Define invariants (e.g., “id must be non-empty”)
    * `[ ]`   No implementation details — pure expectation

  * `[ ]`   `function.interface.ts`
    * `[ ]`   Define:
      * Input types
      * Output types
      * Error types (explicitly)
    * `[ ]`   No implicit/any types unless explicitly justified
    * `[ ]`   Each type is minimal and composable

  * `[ ]`   `function.interaction.spec`
    * `[ ]`   Define:
      * Expected call patterns (who calls this, how)
      * Required dependency interactions
    * `[ ]`   For each interaction:
      * Input → output expectation
      * Side effects (if any)
    * `[ ]`   Define failure modes:
      * What errors occur
      * Under what conditions
    * `[ ]`   Define ordering/temporal constraints (if applicable)
    * `[ ]`   No code — purely declarative

  * `[ ]`   `[function].guard.test.ts`
    * `[ ]`   Verify guards against contract tests
    * `[ ]`   Ensure:
      * No false positives
      * No false negatives

  * `[ ]`   `[function].guard.ts`
    * `[ ]`   Implement guards for each interface type
    * `[ ]`   Guards must:
      * Accept all valid contract cases
      * Reject all invalid contract cases

  * `[ ]`   `[function].mock.ts`
    * `[ ]`   Provide controllable implementations of:
      * All external interactions
    * `[ ]`   Must conform to:
      * interface
      * interaction.spec
    * `[ ]`   No new behavior introduced beyond spec

  * `[ ]`   `[function].test.ts`
    * `[ ]`   Validate behavior against:
      * `requirements`
      * `interaction.spec`
    * `[ ]`   Each checklist item validates:
      * Proof that a specific behavioral contract is upheld positively
      * Proof that a specific behavioral contract is not violated negatively
    * `[ ]`   Focus on:
      * Correct transformations
      * Correct branching logic
    * `[ ]`   Do NOT re-test:
      * Type shape
      * Guard correctness

  * `[ ]`   `[function].someOther.test.ts` 
    * Some functions have multiple test files. 
    * In such case, include every test file that must be updated in the node detail. 
    * Test files are generally broken apart when there are large sets of tests for different behaviors.
    * Separate test files generally group similar functional contracts.
    * Having numerous test files is a good signal that the function needs to be decomposed. 

  * `[ ]`   `construction`
    * `[ ]`   Define:
      * Factory/constructor entrypoints
      * Required dependencies at creation
    * `[ ]`   Enforce:
      * No partially constructed instances
    * `[ ]`   Declare invalid construction contexts
    * `[ ]`   Define initialization order (if needed)

  * `[ ]`   `[function].ts`
    * `[ ]`   Implement behavior defined in:
      * `requirements`
      * `interaction.spec`
    * `[ ]`   Must not:
      * Introduce undeclared dependencies
      * Bypass guards or contracts
    * `[ ]`   Each requirement maps to code paths

  * `[ ]`   `[function].provides.ts`
    * `[ ]`   Declare:
      * All exported symbols
      * Public API surface
    * `[ ]`   Define:
      * Stability guarantees
      * Semantic guarantees
    * `[ ]`   Enforce:
      * No external access bypasses this file

  * `[ ]`   `[function].integration.test.ts`
    * `[ ]`   Not every node has an integration test.
      *    Do not specify an integration test until an integration boundary is reached. 
      *    The integration test must use the real functions and only mock at the boundary of the chain. 
    * `[ ]`   Validate:
      * provider → function
      * function → consumer
      * full chain interactions
    * `[ ]`   Use mocks only for external nodes, do not mock any function within the chain.
      * If a function in the chain has a side-effect that reaches outside the codebase (like making an external API call) you may need to stub that call so it does not leave the codebase. 

  * `[ ]`   `directionality`
    * `[ ]`   Declare node layer
    * `[ ]`   Confirm:
      * deps are inward-facing
      * provides are outward-facing
    * `[ ]`   No cycles unless explicitly justified

  * `[ ]`   `requirements`
    * `[ ]`   Define acceptance criteria (binary pass/fail)
    * `[ ]`   Each requirement:
      * Is observable
      * Is testable
      * Maps to tests

  * `[ ]`   **Commit** `[type] [scope] [summary]`
    * `[ ]`   Not every node has a Commit step, Commit steps generally come at a sprint boundary where the new feature is built and integrated. 
    * `[ ]`   Never add Commit steps if the function is not buildable yet. 
    * `[ ]`   The new feature may not be fully integrated at a Commit step, that is fine. 
    * `[ ]`   List structural changes
    * `[ ]`   List behavioral changes
    * `[ ]`   List contract changes

# To-Do List

## Name of deferred work item

