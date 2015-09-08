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

First, we install the gem.

```
gem install rspec
```

Then we create a spec file, `calendar_spec.rb`, and require the code under test within that file.

```
require 'calendar'
```

This loads the code in `calendar.rb`.  The code is loaded exactly once, so if we were to require the same file again, it would not be loaded again.

Then we can run our spec with the following command.

```
spec calendar_spec.rb 
```

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
