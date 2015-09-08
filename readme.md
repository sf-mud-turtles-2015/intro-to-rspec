# Introduction to Testing, BDD, and RSpec

### Why Do We Care About Testing?
- Programatically specify behavior
- Ensure program correctness
- Cut down debugging time
- Enable refactoring
- Reduce unnecessary code, overdesigning, feature creep

### What is a Spec?
- A description of expected behavior that we can run against production code

### What is TDD/DBB?
- TDD/BDD means we write our spec code before we write production code
- Red, Green, Refactor cycle

### Setting up Rspec
- RSpec is a gem
- RSpec is a DSL for testing (as opposed to a GPL like ruby)

First, we install the gem
```
gem install rspec
```

Then we create a spec file, `test_spec.rb`, and require the code under test within that file
```
require 'production'
```
This loads the code in `production.rb`

### RSpec terminology and syntax
- describe block
- example block `it`
- context block
- expect statement
- matchers
- let

### Resources
- rspec gem documentation
- shoulda matchers gem
