# Introduction to Testing, TDD/BDD, and RSpec

### Pairing Discussion
- What went well?
- What was difficult?
- Checking in with your pair
- Giving and receiving feedback

### Why Do We Care About Testing?
- Programatically specify behavior
- Ensure program correctness
- Cut down debugging time
- Enable refactoring
- Reduce unnecessary code, overdesigning, feature creep

### What is a Spec?
- A description of expected behavior that we can run against production code

### What is TDD/BDD?
- TDD/BDD means we write our spec code before we write production code
- Testing a whole code base after it is written is incredibly challenging
- Red, Green, Refactor cycle
- We do just enough to make the tests pass, which disciplines us to write code in small, functional pieces
- The goal is the test
- With BDD we test behavior, which means focusing on business value. TDD focuses on how something will work, BDD focuses on the customer perspective of what we built.  Tools like RSpec (and Cucumber and Capybara, which you will learn about later) are helping push the industry in this direction.

### Setting up Rspec
- RSpec is a gem, composed of several stand alone testing gems
- RSpec is a DSL for testing (as opposed to a GPL like ruby)
- A DSL is specific to a problem domain

First, we install the gem.

```
gem install rspec
```

Then we create a spec file, `calendar_spec.rb`, and require the code under test within that file.

```ruby
require_relative 'calendar'
```

This loads the code in `calendar.rb`.  The code is loaded exactly once, so if we were to require the same file again, it would not be loaded again.  Do you know what the difference between `require` and `require_relative` is?  `require_relative` allows you to "load a file that is relative to the file containing the require_relative statement". With `require`, `./` indicates a path that is relative to your current working directory.

Then we can run our spec with the following command.

```
rspec calendar_spec.rb 
```

We fail with an error.  Our `calendar.rb` file doesn't exist yet.  Let's create an empty file, just enough to pass the spec.

Now let's break our tests and specify that we want to describe a calendar component.  We can add the following to our `calendar_spec.rb`

```ruby
require_relative 'calendar'

describe Calendar do
  let(:calendar) { Calendar.new }
end
```

Now the tests fail again.  Let's make them work by modifying `calendar.rb`

```ruby
class Calendar

end
```

Okay, let's start defining some calendar behavior in our `calendar_spec.rb`

```ruby
require_relative 'calendar'
require 'date'

describe Calendar do
  let(:calendar) { Calendar.new }

  it "should parse a D M Y format string into a date" do
    date_string = "10 9 2015"
    expect(@calendar.parse_date(date_string)).to eq Date.new(2015, 9, 10)
  end
end
```

And let's write the code to pass the test in `calendar.rb`.  First we would address the error by defining a `parse_date` method

```ruby
class Calendar

  def parse_date date_string
  end
  
end
```

When we run the spec again, we see that our method is found, but our spec still doesn't pass.  Okay, let's implement the method.

```ruby
class Calendar

  def parse_date date_string
    day = date_string.split(" ")[0].to_i
    month = date_string.split(" ")[1].to_i
    year = date_string.split(" ")[2].to_i
    Date.new(year, month, day)
  end
end
```

Now that we have an exmaple going, if we run the `rspec` command with `--format doc` flag, we'll get documentation format output from our test run.
```
rspec calendar_spec.rb --format doc
```

Okay, let's play around with a few more rspec tools.  Let's create a nested example group using contexts.

```ruby
describe Calendar do
  before :each do
    @calendar = Calendar.new
  end

  it "should parse a D M Y format string into a date" do
    date_string = "10 9 2015"
    expect(@calendar.parse_date(date_string)).to eq Date.new(2015, 9, 10)
  end
  
    context "when new calendar is created" do
    it "should have no events" do
      # ...
    end
  end

  context "when new calendar is created with event import" do
    it "should have events" do
      # ...
    end
  end
end
```

### RSpec terminology and syntax
- `describe`: The `describe` method creates an example group.  We're calling a method defined in the rspec gem.  We pass in the name of the component under test and a block that has the examples.
- `let`: Use let to set up a variable that is shared between tests, to DRY up your specs, and to keep your `it` blocks concise.  With `let`, the variable you set in the block is lazily loaded, which means the block is only executed the first time the variable is used.  With `let!`, the block is executed before each example.  Learn more about `let` from the resources linked below
- `it`: Each example is defined with the `it` method.  `it` takes a string that describes the requirement, which reads like an English sentence, and a block that contains the test case.
- `expect`: Expectations are `should` and `should_not` and work together with `matchers` to express an outcome
- `matchers`: Built-in matchers that allow you to test
   - Equivalence 
    ```ruby
    expect(actual).to eq(expected)
    ```
   - Identity 
    ```ruby
    expect(actual).to be(expected)
    ```
   - Comparisons 
    ```ruby
    expect(actual).to be >= expected
    ``` 
   - Types 
    ```ruby
    expect(actual).to be_an_instance_of(expected)
    ```
   - Booleans 
    ```ruby
    expect(actual).to be_truthy
    ```
   - Regular expressions 
    ```ruby
    expect(actual).to match(/expression/)
    ```
   - Errors 
    ```ruby
    expect { ... }.to raise_error
    ```
   - And so much more!  Read about it in the resource linked below.
- `context`: A powerful construct to keep your spec organized when your code does different things based on different states or conditions

### Food for discussion/thought
- Is what we just did TDD or BDD?  Why?
- How can we make this calendar example more BDD?

### Resources
- [require and require relative ruby docs](http://ruby-doc.org/core-2.1.2/Kernel.html)
- [rspec gem documentation](http://rspec.info/documentation/)
- [Starter BDD example, from the rspec docs](http://rspec.info/documentation/3.3/rspec-core/#Get_Started)
- [RSpec expectations, from the rspec docs)(https://github.com/rspec/rspec-expectations)
- [RSpec best practices](http://betterspecs.org/)
- [Great stackoverflow explanation of why `let` is good](http://stackoverflow.com/questions/5359558/when-to-use-rspec-let/5359979#5359979)
