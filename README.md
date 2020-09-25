# Code Review Checklist

- General Code Review 
  - style guide check, 
  - unit test-cases, 
  - SRP

- Functional Code Review 
  - Functionality check, 
  - Requirements check, 
  - Business-logic check


- Language Specific Code Review
  - Following latest (which is used in app) ruby version methods.
  - Refactor old code whenever possible (small changes and provided it does not affect functionality) 
  - Keep views clean, move styles to css/scss files


- Other checks
  - Performance, 
  - Test Cases Coverage
  - Verified on Desktop (Chrome, Firefox, Safari, Edge, IE 11). Verified on Mobile (iOS and Android)
  - API documents or other documents updated, wherever applicable.


- Testing: 
  - Tenancy (ActsAsTenant) in test should mimic application behavior as much as possible. Controller tests should create tenancy via a user sign-in.

## GENERAL CODE REVIEW

General code review will include a generalized code review that will take care of how well the code is written. This step will help us to maintain clean code irrespective of the number of developers who are updating code.

- Style Guide Check
  - Ruby StyleGuide https://github.com/airbnb/ruby
  - Javascript StyleGuide https://github.com/airbnb/javascript	
  - Rspec Guidelines http://www.betterspecs.org/	

- Test Cases
  - Unit test cases
  - Failing and Passing Test cases for each unit-test
  - Mocking of third party API calls

- SRP (Single Responsibility Principle)
  - Small Unit Methods
  - Each method is doing only a single task (Most of the times this is missed out)

## FUNCTIONAL CODE REVIEW

This step will include a functional code review, where a Reviewer having a good understanding of the application, business use cases, who knows in and out of the system performs functional code review of PR.

Functional code review is the most important step of code review, which will give the surety that code developed by the developer is as per the requirement, passing acceptance criteria and will not break or raise any security concern in the existing application.

In this review step, it would be always good and safe to verify the code-changes with the developers who have worked on that particular application area before. 

Steps followed:
  - Check the Ticket associated with PR, also ticket description, acceptance criteria, discussion comments.
  - Review code changes and evaluate whether all the scenarios are covered or not.
  - If possible, do peer review and demo with the developer who has raised PR. 

## LANGUAGE SPECIFIC REVIEW:

- ROR:
  - Migration 
  - Both up and down migration is written correctly (reversible)
  - Data Types, Default Values 
  - Valid Column Names, Join Table Names
  - Backward compatibility (in case if the app is already live) 
  - Check for missing indices where they should be.
  - Migrations that remove data should store that data prior to removal, such that it can be recovered in a down migration. All data should be stored before any database changes occur
- Seed Data 
  - Good amount of development/test data is covered or not
- Model, Services
  - Whenever possible plain ruby classes (services) should be added for a modular feature like Authentication, Third-Party Services used.
  - No SQL injection
  - Valid Model Associations
  - Scopes, Class Methods, Instance Methods
  - Validations	

- Controller
  - Proper filters
  - Base controllers
  - Rendering and Returning of responses are handled for all possible formats

- API
  - JSON output, include only required attributes and related data (no unwanted data)
  - API Documentation
  - API Authentication

- RAKE task
  - Proper Logging
  - Exception handling
  - Batch processing of records.

- Gemfile
  - Gems are grouped properly. For example:  test, development group
  - Updated Gemfile.lock 

- API/secret keys
  - .env file maintained with any third party API keys and environment-dependent constants. For example:  AWS keys, S3 Buckets, etc.

- Routes
  - Proper usage of member/collection routes
  - nested/ namespaced routes

- Data Queries 
  - Consolidated and Optimized Queries for performance 
  - Index Page-type loads (longs lists of objects) should join external data so it may be sorted or filtered by. 
  - Avoid N+1 queries.

## METRICS:

While doing a code review, we will be mainly considering the following aspects:

- Quality 
   - Followed all the general guidelines and language-specific guidelines. (Specified above)
- Testing
  - Covered Unit test cases
  - Fulfills all the functional requirements specified in the ticket.
- Performance
  - PR does not have code changes which will slow down the rendering of app
  - optimized SQL queries, No N+1 queries
  - Not loading unnecessary plugins

## CODE REVIEW PROCEDURE:


To review the code effectively with minimal time spent, here we will be defining the procedure that Reviewer should follow instead of just randomly starting reviewing the code:

1. *Check if PR has any build failure.* If it has any, raise the flag to the PR Assignee. (so that developer will fix the failing test cases first, and other reviewers will not have to spend extra time to review the code again)

2. *Check if PR has enough details* like PR description, Ticket/Issue link, Screenshots (if Ticket is related to UI). In case the PR lacks these details, raise the flag to the PR Assignee and ask to add all the details.

3. *Check the Ticket/Issue attached in the PR.* Quickly check the ticket description, comments on a ticket to understand requirements, that will help to know whether the code changes in the PR are valid or not.

4. Code Review:
    - *Quality Check:* whether it follows general guidelines and language-specific guidelines. 
    - *Functional Review:* whether code changes satisfy the requirements, all the scenarios/cases are covered or not.
    - *Testing:* whether code changes have the unit test cases, covered all the possible positive and negative test cases or not.
    - *Performance Check:* Whether code changes lead to any kind slow rendering of the app like DB-queries, plugins, third-party API calls without a timeout, etc should be verified.

5. If there are any suggestions or changes that you want to provide in code, add review comments with details, if possible attach the reference as that will help Assignee to understand your suggestion better. In case of any doubts/queries, add your question in comment and ask Assignee to give the explanation for the code changes and/or ask for examples. 

6. Re-Review: 
    - When Assignee asks for re-review, check whether your suggestions are addressed properly or not.
    - After new-changes, whether it affects existing test-cases or any other areas, those are handled or not.

## FLOW CHART
![Code Review Flowchart](https://github.com/sampatbadhe/Code-Review-Checklist/blob/master/Code%20Review%20Workflow.jpeg)

## REFERENCES:

https://www.codementor.io/blog/code-review-checklist-76q7ovkaqj	
https://matthewpaulmoore.com/post/5190436725/ruby-on-rails-code-quality-checklist
https://medium.com/palantir/code-review-best-practices-19e02780015f	
