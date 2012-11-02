!SLIDE 
# Cucumber
## Doing it right
<br/>
### tom-clements.com | github.com/seenmyfate
### @Seenmyfate
!SLIDE bullets incremental
# Good Cucumber

* starts a focused conversation
* helps us share a common language
* helps us find edge cases
* improves our communication

!SLIDE bullets incremental
# Bad Cucumber

* is a waste of time and energy

!SLIDE bullets incremental
# Positive side effects

* living, executable documentation
* tracks intention
* prevents regressions

!SLIDE bullets incremental
# Negative side effects

* more code to write 
* more code to maintain
* complexity!

!SLIDE bullets incremental
# The real benefit

* clarity
* but not without effort

!SLIDE
## _Do or do not. There is no try_

To get benefit from cucumber, we must be disciplined

!SLIDE bullets incremental
# Features != User Stories

* User Stories are a planning tool
* Delete them once they're implemented
* Features are a communication tool
* They describe how the system works today

!SLIDE
## Every cucumber example on the internet, ever

    @@@ ruby
      Feature:
        In order to get access to the site
        As a visitor
        I want to sign in
        
!SLIDE
# Features != User Stories

!SLIDE
## Features describe how the system works today

    @@@ ruby
      Feature:
        The content of our site is protected.
        You must sign in before you can see it.

!SLIDE
# Scenarios != Steps

!SLIDE
## Every cucumber example on the internet, ever

    @@@ ruby
      Scenario:
        Given I visit the signin page
        And I fill in "username" with "tom"
        And I fill in "password" with "test"
        And I press "submit"
        Then I can see "Welcome"
        And I can see "Signed in"
        And I am on the dashboard page

!SLIDE incremental
# ┻━┻︵ヽ(`Д´)ﾉ︵┻━┻

This is unmaintainable nonsense

!SLIDE

_"If your scenario starts with ‘When the user enters ‘Smurf’ into ‘Search’ text box…’ then that’s far too low-level. However, even “When the user adds ‘Smurf’ to his basket, then goes to the checkout, then pays for the goods” is also too low-level. You’re looking for something like, ‘When the user buys a Smurf.’"_

Liz Keogh

!SLIDE bullets incremental
# Scenarios
* are acceptance criteria
* written at a high level
* written using consistent language
* are independent and deterministic

!SLIDE incremental
# Steps
## Write and organise your steps like you write and organise your code

* modular
* reusable
* DRY
* do one thing
* delegate to other steps


!SLIDE incremental
## An example

    @@@ ruby
      Scenario:
        Given I visit the signin page
        And I fill in "username" with "tom"
        And I fill in "password" with "test"
        And I press "submit"
        Then I can see "Welcome"
        And I can see "Signed in"
        And I am on the dashboard page

!SLIDE
## An example
    @@@ ruby
      Scenario:
        Given I sign in
        ..

!SLIDE
## Delegate steps
    @@@ ruby
      Given /^I sign in$/ do
        steps %{
          * I sign up
          * I complete the sign in form
        }
      end

!SLIDE
## Delegate some more
    @@@ ruby
      Given /^I sign up$/ do
        steps %{
          * I complete the sign up form
          * I confirm my email address
        }
      end

!SLIDE smaller
## And some more
    @@@ ruby
      Given /^I complete the sign up form$/ do
        steps %{
          * submit the sign up form with valid information
        }
      end
      
!SLIDE smaller
## And some more
    @@@ ruby
      Given /^submit the sign up form with valid information$/ do
        steps %{
          * I fill in "username" with "#{valid_user.name}"
          * I fill in "password" with "#{valid_user.password}"
          * I press "#{I18n.t(:submit)}"
        }
      end      

!SLIDE

!SLIDE bullets smaller
# We should only ever change scenarios when the behaviour changes, not the implementation

!SLIDE
# Happy Cuking
<br/>
### tom-clements.com | github.com/seenmyfate
### @Seenmyfate

