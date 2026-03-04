---
{"dg-publish":true,"permalink":"/knowledge/test-doubles/"}
---

## What are Doubles

“Double” is a generic term for objects that look or behave like objects our code depends on. They are a fundamental part of unit testing.

## The Types of Doubles

There are the following types / specifications of doubles: Dummies, Spies, Stubs, Fakes and Mocks.

### Dummy

The purpose of a dummy is just to satisfy constructors. If you want to test a method which's object requires a dependency in the constructor that isn't used in the tested method, you pass in a dummy. 

```rb
# order_processor.rb
class OrderProcessor
  def initialize(logger)
    @logger = logger
  end

  def greet()
    "Hello!"
  end
  # ...
end

# order_processor_spec.rb
require 'rspec'

RSpec.describe OrderProcessor do
  describe '#greet' do
    it 'returns a greeting message' do
      dummy_logger = double('Logger') 
      processor = OrderProcessor.new(dummy_logger)
      
      expect(processor.greet()).to eq('Hello!')
    end
  end
end
```

### Stub

A stub always returns the same value on a function call.

```rb
# example.rb
class Greeter
  def initialize(name_source)
    @name_source = name_source
  end

  def greet
    "Hello, #{@name_source.name}!"
  end
end

# example_spec.rb
require "rspec"
require_relative "tiny_example"

RSpec.describe Greeter do
  it "greets using the fake name source" do
    fake_name_source = double("NameSource", name: "Alice")
    greeter = Greeter.new(fake_name_source)

    expect(greeter.greet).to eq("Hello, Alice!")
  end
end
```

### Fake

When testing something that uses an external data source, that source can be replaced with a fake. Fakes can be used in unit and integration tests.

```rb
# example.rb
class Greeter
  def initialize(database)
    @database = database
  end

  def greet(user_id)
    user_name = @database.find_user_name(user_id)
    "Hello, #{user_name}!"
  end
end

# fake_database.rb
class FakeDatabase
  def initialize
    @users = {
      1 => "Alice",
      2 => "Bob",
      3 => "Charlie"
    }
  end

  def find_user_name(user_id)
    @users[user_id] || "Guest"
  end
end

example_spec.rb

# example_spec.rb
require "rspec"
require_relative "example"
require_relative "fake_database"

RSpec.describe Greeter do
  it "greets the user using a fake database" do
    fake_db = FakeDatabase.new
    greeter = Greeter.new(fake_db)

    expect(greeter.greet(1)).to eq("Hello, Alice!")
    expect(greeter.greet(2)).to eq("Hello, Bob!")
  end
end
```

### Spy

Spies are here to observe how the tested component interacts with another object. For example, if, how often or with what parameters a given method gets called. Spies can also be wrapped around real objects and just listen to the interactions with it.

```rb
# my_class.rb
class MyClass
  def greet(user)
    user.say_hello("Hello!")
  end
end

# my_class_spec.rb
require "rspec"

RSpec.describe MyClass do
  it "calls say_hello on the user" do
    user = double("User").as_null_object

    my_class = MyClass.new
    my_class.greet(user)

    expect(user).to have_received(:say_hello).with("Hello!")
  end
end
```

There are also partial spies. A partial spy wraps around a real object and listens to a specific method call.

```rb
user = User.new
allow(user).to receive(:say_hello).and_call_original
spy_user = spy(user)
```

### Mock

A mock is a double that contains predefined expectations.

```rb
# user_notifier_spec.rb
require 'rspec'

class UserNotifier
  def initialize(mailer)
    @mailer = mailer
  end

  def notify(user)
    @mailer.send_email(user, "Welcome!")
  end
end

RSpec.describe UserNotifier do
  it "sends a welcome email" do
    mailer_mock = double("Mailer")
    allow(mailer_mock).to receive(:send_email)

    notifier = UserNotifier.new(mailer_mock)
    notifier.notify("alice@example.com")

    expect(mailer_mock)
    .to have_received(:send_email)
    .with("alice@example.com", "Welcome!")
  end
end
```
 
 In other testing frameworks, the expectations are actually written inside the mock class.
 