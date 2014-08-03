# The Ruby Style Guide

## Source Code Layout

* <a name="spaces-indentation"></a>
  Use two **spaces** per indentation level (aka soft tabs). No hard tabs.
<sup>[[link](#spaces-indentation)]</sup>

  ```Ruby
  # standard
  def some_method
    do_something
  end

  # non-standard - four spaces
  def some_method
      do_something
  end
  ```

* <a name="no-semicolon"></a>
  Avoid `;` to separate statements and expressions. Use one expression per line.
<sup>[[link](#no-semicolon)]</sup>

  ```Ruby
  # standard
  puts 'foobar'

  puts 'foo'
  puts 'bar'

  # non-standard
  puts 'foobar'; # superfluous semicolon

  puts 'foo'; puts 'bar' # two expressions on the same line
  ```

* <a name="single-line-classes"></a>
  Class definitions should be laid out in a standard fashion even if they have no body.
<sup>[[link](#single-line-classes)]</sup>

  ```Ruby
  # standard
  class FooError < StandardError
  end

  # non-standard
  class FooError < StandardError; end

  # non-standard
  FooError = Class.new(StandardError)
  ```

* <a name="no-single-line-methods"></a>
  Avoid putting method definitions and the body on a single line.
<sup>[[link](#no-single-line-methods)]</sup>

  ```Ruby
  # standard
  def some_method
    body
  end

  # non-standard
  def too_much; something; something_else; end

  # non-standard - notice that the first ; is required
  def no_braces_method; body end

  # non-standard - notice that the second ; is optional
  def no_braces_method; body; end

  # non-standard - valid syntax, but no ; makes it kind of hard to read
  def some_method() body end
  ```

  # non-standard
  def no_op; end
  ```

* <a name="spaces-operators"></a>
  Use spaces around operators, after commas, colons and semicolons, around `{`
  and before `}`.
<sup>[[link](#spaces-operators)]</sup>

  ```Ruby
  sum = 1 + 2
  a, b = 1, 2
  [1, 2, 3].each { |e| puts e }
  class FooError < StandardError; end
  ```

  The only exception, regarding operators, is the exponent operator:

  ```Ruby
  # standard
  e = M * c**2

  # non-standard
  e = M * c ** 2
  ```

  Treat `{` and `}` consistently.

  ```Ruby
  # standard - space after { and before }
  { one: 1, two: 2 }

  # non-standard - no space after { and before }
  {one: 1, two: 2}
  ```

  As far as embedded expressions go, omit spaces.

  ```Ruby
  # standard - no spaces
  "string#{expr}"

  # non-standard
  "string#{ expr }"
  ```

* <a name="no-spaces-braces"></a>
  No spaces after `(`, `[` or before `]`, `)`.
<sup>[[link](#no-spaces-braces)]</sup>

  ```Ruby
  some(arg).other
  [1, 2, 3].size
  ```

* <a name="no-space-bang"></a>
  No space after `!`.
<sup>[[link](#no-space-bang)]</sup>

  ```Ruby
  # standard
  !something

  # non-standard
  ! something
  ```

* <a name="empty-lines-between-methods"></a>
  Use empty lines between method definitions and also to break up a method
  into logical paragraphs internally.
<sup>[[link](#empty-lines-between-methods)]</sup>

  ```Ruby
  def some_method
    data = initialize(options)

    data.manipulate!

    data.result
  end

  def some_method
    result
  end
  ```

* <a name="indent-when-to-case"></a>
  Indent `when` as deep as `case`. Space out the when clauses as separate paragraphs.

  Note that the use of a case statement could point to a problem in your design.
<sup>[[link](#indent-when-to-case)]</sup>

  ```Ruby
  # standard
  case

  when song.name == 'Misty'
    puts 'Not again!'

  when song.duration > 120
    puts 'Too long!'

  when Time.now.hour > 21
    puts "It's too late"

  else
    song.play
  end

  # non-standard
  case
    when song.name == 'Misty'
      puts 'Not again!'
    when song.duration > 120
      puts 'Too long!'
    when Time.now.hour > 21
      puts "It's too late"
    else
      song.play
  end
  ```

* <a name="indent-conditional-assignment"></a>
  When assigning the result of a conditional expression to a variable,
  do not try to lay out the code to make it "easier to read". Here, spending time
  on making the code "look good" is a sign that you have a design problem.

  Using this idiom suggests you are writing a procedural script rather than
  thinking of your problem functionally, so be wary of code that does this. The conditional
  should be extracted as its own method.
<sup>[[link](#indent-conditional-assignment)]</sup>

  ```Ruby
  # standard
  result = if some_cond
    calc_something
  else
    calc_something_else
  end

  # standard
  result =
    if some_cond
      calc_something
    else
      calc_something_else
    end

  # non-standard - if you want to do this, you should have extracted a method by now
  result = if some_cond
             calc_something
           else
             calc_something_else
           end

  ```

* <a name="no-trailing-params-comma"></a>
  Avoid comma after the last parameter in a method call, especially when the
  parameters are not on separate lines.
<sup>[[link](#no-trailing-params-comma)]</sup>

  ```Ruby
  # standard
  some_method(size, count, color)

  # non-standard
  some_method(
               size,
               count,
               color,
             )

  # non-standard
  some_method(size, count, color, )

  ```

* <a name="spaces-around-equals"></a>
  Avoid spaces around the `=` operator when assigning default values to method
  parameters:
<sup>[[link](#spaces-around-equals)]</sup>

  ```Ruby
  # standard
  def some_method(arg1=:default, arg2=nil, arg3=[])
    # do something...
  end

  # non-standard
  def some_method(arg1 = :default, arg2 = nil, arg3 = [])
    # do something...
  end
  ```

* <a name="no-trailing-backslash"></a>
  Avoid line continuation `\`.
<sup>[[link](#no-trailing-backslash)]</sup>

  ```Ruby
  # non-standard
  result = 1 \
           - 2

  long_string = 'First part of the long string' \
                ' and second part of the long string'

  ```

* <a name="consistent-multi-line-chains"></a>
    Avoid multi-line method chaining styles. You should have extracted some methods by then
<sup>[[link](#consistent-multi-line-chains)]</sup>

    ```Ruby
    # non-standard
    one.two.three.
      four

    one.two.three
      .four
    ```

* <a name="no-double-indent"></a>
    Single-indent the parameters of a method call if they span more than one
    line. Fancier formatting is harder to maintain and method shouldn't be accepting more than 3 arguments anyway.
<sup>[[link](#no-double-indent)]</sup>

  ```Ruby
  # standard
  def send_mail(source)
    Mailer.deliver(
      to: 'bob@example.com',
      from: 'us@example.com',
      subject: 'Important message',
      body: source.text
    )
  end

  # standard
  def send_mail(source)
    Mailer.deliver(to: 'bob@example.com', from: 'us@example.com', subject: 'Important message', body: source.text)
  end

  # non-standard
  def send_mail(source)
    Mailer.deliver(
        to: 'bob@example.com',
        from: 'us@example.com',
        subject: 'Important message',
        body: source.text)
  end

  # non-standard
  def send_mail(source)
    Mailer.deliver(to: 'bob@example.com',
                   from: 'us@example.com',
                   subject: 'Important message',
                   body: source.text)
  end

  ```

* <a name="align-multiline-arrays"></a>
  Align the elements of array literals spanning multiple lines.
<sup>[[link](#align-multiline-arrays)]</sup>

  ```Ruby
  # standard
  menu_item = [
    'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
    'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam'
  ]

  menu_item =
  [
    'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
    'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam'
  ]

  # non-standard
  menu_item =
    ['Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
     'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam']

  # non-standard
  menu_item = ['Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
    'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam']
  ```

* <a name="underscores-in-numerics"></a>
  Add underscores to large numeric literals to improve their readability.
<sup>[[link](#underscores-in-numerics)]</sup>

  ```Ruby
  # standard - much easier to parse for the human brain
  num = 1_000_000

  # non-standard - how many 0s are there?
  num = 1000000
  ```

* <a name="no-trailing-whitespace"></a>
  Avoid trailing whitespace.
<sup>[[link](#no-trailing-whitespace)]</sup>

* <a name="newline-eof"></a>
  End each file with a newline.
<sup>[[link](#newline-eof)]</sup>

## Syntax

* <a name="method-parens"></a>
    Use `def` with parentheses when there are arguments. Omit the
    parentheses when the method doesn't accept any arguments.
<sup>[[link](#method-parens)]</sup>

  ```Ruby
  # standard
  def some_method
   # body omitted
  end

  # standard
  def some_method_with_arguments(arg1, arg2)
   # body omitted
  end

  # non-standard
  def some_method()
    # body omitted
  end

   # non-standard
   def some_method_with_arguments arg1, arg2
     # body omitted
   end
   ```

* <a name="no-for-loops"></a>
    Never use `for`, unless you know exactly why. Most of the time iterators
    should be used instead. `for` is implemented in terms of `each` (so
    you're adding a level of indirection), but with a twist - `for`
    doesn't introduce a new scope (unlike `each`) and variables defined
    in its block will be visible outside it.
<sup>[[link](#no-for-loops)]</sup>

  ```Ruby
  arr = [1, 2, 3]

  # standard
  arr.each { |elem| puts elem }

  # elem is not accessible outside each's block
  elem # => NameError: undefined local variable or method `elem'
  ```
  # non-standard
  for elem in arr do
    puts elem
  end

  # note that elem is accessible outside of the for loop
  elem # => 3

* <a name="no-then"></a>
  Never use `then` for multi-line `if/unless`.
<sup>[[link](#no-then)]</sup>

  ```Ruby
  # standard
  if some_condition
    # body omitted
  end

  # non-standard
  if some_condition then
    # body omitted
  end
  ```

* <a name="same-line-condition"></a>
  Always put the condition on the same line as the `if`/`unless` in a
  multi-line conditional.
<sup>[[link](#same-line-condition)]</sup>

  ```Ruby
  # standard
  if some_condition
    do_something
    do_something_else
  end

  # non-standard
  if
    some_condition
    do_something
    do_something_else
  end
  ```

* <a name="ternary-operator"></a>
  Favor the ternary operator(`?:`) over `if/then/else/end` constructs.
  It's more common and obviously more concise.
<sup>[[link](#ternary-operator)]</sup>

  ```Ruby
  # standard
  result = some_condition ? something : something_else

  # non-standard
  result = if some_condition then something else something_else end
  ```

* <a name="no-nested-ternary"></a>
  Use one expression per branch in a ternary operator. This
  also means that ternary operators must not be nested. Prefer
  `if/else` constructs in these cases.
<sup>[[link](#no-nested-ternary)]</sup>

  ```Ruby
  # standard
  if some_condition
    nested_condition ? nested_something : nested_something_else
  else
    something_else
  end

  # non-standard
  some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else
  ```

* <a name="no-semicolon-ifs"></a>
  Never use `if x; ...`. Use the ternary operator instead.
<sup>[[link](#no-semicolon-ifs)]</sup>

* <a name="use-if-case-returns"></a>
  Leverage the fact that `if` and `case` are expressions which return a
  result.
<sup>[[link](#use-if-case-returns)]</sup>

  ```Ruby
  # standard
  result =
    if condition
      x
    else
      y
    end

  # non-standard
  if condition
    result = x
  else
    result = y
  end
  ```

* <a name="bang-not-not"></a>
  Use `!` instead of `not`.
<sup>[[link](#bang-not-not)]</sup>

  ```Ruby
  # standard
  x = !something

  # non-standard - braces are required because of op precedence
  x = (not something)
  ```

* <a name="no-multiline-ternary"></a>
  Avoid multi-line `?:` (the ternary operator); use `if/unless` instead.
<sup>[[link](#no-multiline-ternary)]</sup>

* <a name="if-as-a-modifier"></a>
  Favor modifier `if/unless` usage when you have a single-line body. Another
  good alternative is the usage of control flow `and/or`.
<sup>[[link](#if-as-a-modifier)]</sup>

  ```Ruby
  # standard
  do_something if some_condition

  # standard
  some_condition and do_something

  # non-standard
  if some_condition
    do_something
  end
  ```

* <a name="unless-for-negatives"></a>
  Favor `unless` over `if` for negative conditions (or control flow `||`).
<sup>[[link](#unless-for-negatives)]</sup>

  ```Ruby
  # standard
  do_something unless some_condition

  # standard
  some_condition or do_something

  # non-standard
  do_something if !some_condition

  # non-standard
  do_something if not some_condition
  ```

* <a name="no-else-with-unless"></a>
  Avoid `unless` with `else`. Trty rewriting these with the positive case first.
<sup>[[link](#no-else-with-unless)]</sup>

  ```Ruby
  # standard
  if success?
    puts 'success'
  else
    puts 'failure'
  end

  # non-standard
  unless success?
    puts 'failure'
  else
    puts 'success'
  end
  ```

* <a name="no-parens-if"></a>
  Don't use parentheses around the condition of an `if/unless/while/until`.
<sup>[[link](#no-parens-if)]</sup>

  ```Ruby
  # standard
  if x > 10
    # body omitted
  end

  # non-standard
  if (x > 10)
    # body omitted
  end
  ```

* <a name="no-dsl-parens"></a>
  Omit parentheses around parameters for methods that are part of an internal
  DSL (e.g. Rake, Rails, RSpec), methods that have "keyword" status in Ruby
  (e.g. `attr_reader`, `puts`) and attribute access methods. Use parentheses
  around the arguments of all other method invocations.
<sup>[[link](#no-dsl-parens)]</sup>

  ```Ruby
  class Person
    attr_reader :name, :age

    # omitted
  end

  temperance = Person.new('Temperance', 30)
  temperance.name

  puts temperance.age

  x = Math.sin(y)
  array.delete(e)

  bowling.score.should == 0
  ```

* <a name="no-braces-opts-hash"></a>
  Omit the outer braces around an implicit options hash.
<sup>[[link](#no-braces-opts-hash)]</sup>

  ```Ruby
  # standard
  user.set(name: 'John', age: 45, permissions: { read: true })

  # non-standard
  user.set({ name: 'John', age: 45, permissions: { read: true } })
  ```

* <a name="no-dsl-decorating"></a>
  Omit both the outer braces and parentheses for methods that are part of an
  internal DSL.
<sup>[[link](#no-dsl-decorating)]</sup>

  ```Ruby
  class Person < ActiveRecord::Base
    # standard
    validates :name, presence: true, length: { within: 1..10 }

    # non-standard
    validates(:name, { presence: true, length: { within: 1..10 } })
  end
  ```

* <a name="no-args-no-parens"></a>
  Omit parentheses for method calls with no arguments.
<sup>[[link](#no-args-no-parens)]</sup>

  ```Ruby
  # standard
  Kernel.exit!
  2.even?
  fork
  'test'.upcase

  # non-standard
  Kernel.exit!()
  2.even?()
  fork()
  'test'.upcase()
  ```

* <a name="single-line-blocks"></a>
  Prefer `{...}` over `do...end` for single-line blocks.  Avoid using `{...}`
  for multi-line blocks (multiline chaining is always ugly). Always use
  `do...end` for "control flow" and "method definitions" (e.g. in Rakefiles and
  certain DSLs).  Avoid `do...end` when chaining.
<sup>[[link](#single-line-blocks)]</sup>

  ```Ruby
  names = ['Bozhidar', 'Steve', 'Sarah']

  # standard
  names.each { |name| puts name }

  # non-standard
  names.each do |name|
    puts name
  end

  # standard
  names.select { |name| name.start_with?('S') }.map { |name| name.upcase }

  # non-standard
  names.select do |name|
    name.start_with?('S')
  end.map { |name| name.upcase }
  ```

* <a name="lambda-multi-line"></a>
  Use the new lambda literal syntax for single line body blocks. Use the
  `lambda` method for multi-line blocks.
<sup>[[link](#lambda-multi-line)]</sup>

  ```Ruby
  # standard
  l = ->(a, b) { a + b }
  l.call(1, 2)

  l = lambda do |a, b|
    tmp = a * 7
    tmp * b / 50
  end

  # non-standard
  l = ->(a, b) do
    tmp = a * 7
    tmp * b / 50
  end

  # non-standard
  l = lambda { |a, b| a + b }
  l.call(1, 2)
  ```

* <a name="proc"></a>
  Prefer `proc` over `Proc.new`.
<sup>[[link](#proc)]</sup>

  ```Ruby
  # standard
  p = proc { |n| puts n }

  # non-standard
  p = Proc.new { |n| puts n }
  ```

* <a name="proc-call"></a>
  Prefer `proc.call()` over `proc[]` or `proc.()` for both lambdas and procs.
<sup>[[link](#proc-call)]</sup>

  ```Ruby
  # standard
  l = ->(v) { puts v }
  l.call(1)

  # non-standard
  l = ->(v) { puts v }
  l[1]

  # non-standard
  l = ->(v) { puts v }
  l.(1)
  ```

* <a name="underscore-unused-vars"></a>
  Prefix with `_` unused block parameters and local variables.
<sup>[[link](#underscore-unused-vars)]</sup>

  ```Ruby
  # standard
  result = hash.map { |_, v| v + 1 }

  # standard
  result = hash.map { |_k, v| v + 1 }

  # non-standard
  result = hash.map { |k, v| v + 1 }
  ```

* <a name="no-explicit-return"></a>
  Avoid `return` where not required for flow of control.
<sup>[[link](#no-explicit-return)]</sup>

  ```Ruby
  # standard
  def some_method(some_arr)
    some_arr.size
  end

  # non-standard
  def some_method(some_arr)
    return some_arr.size
  end
  ```

* <a name="no-self-unless-required"></a>
  Avoid `self` where not required.
<sup>[[link](#no-self-unless-required)]</sup>

  ```Ruby
  # standard
  def ready?
    if last_reviewed_at > last_updated_at
      worker.update(content, options)
      self.status = :in_progress
    end
    status == :verified
  end

  # non-standard
  def ready?
    if self.last_reviewed_at > self.last_updated_at
      self.worker.update(self.content, self.options)
      self.status = :in_progress
    end
    self.status == :verified
  end
  ```

* <a name="safe-assignment-in-condition"></a>
  Don't use the return value of `=` (an assignment) in conditional expressions
  unless the assignment is wrapped in parentheses. This is a fairly popular
  idiom among Rubyists that's sometimes referred to as *safe assignment in
  condition*.
<sup>[[link](#safe-assignment-in-condition)]</sup>

  ```Ruby
  # non-standard (+ a warning)
  if v = array.grep(/foo/)
    do_something(v)
    ...
  end

  # standard (MRI would still complain, but RuboCop won't)
  if (v = array.grep(/foo/))
    do_something(v)
    ...
  end

  # standard
  v = array.grep(/foo/)
  if v
    do_something(v)
    ...
  end
  ```

* <a name="self-assignment"></a>
  Use shorthand self assignment operators whenever applicable.
<sup>[[link](#self-assignment)]</sup>

  ```Ruby
  # standard
  x += y
  x *= y
  x **= y
  x /= y
  x ||= y
  x &&= y

  # non-standard
  x = x + y
  x = x * y
  x = x**y
  x = x / y
  x = x || y
  x = x && y
  ```

* <a name="double-pipe-for-uninit"></a>
  Use `||=` to initialize variables only if they're not already initialized.
<sup>[[link](#double-pipe-for-uninit)]</sup>

  ```Ruby
  # standard
  name ||= 'Bozhidar'

  # non-standard
  name = name ? name : 'Bozhidar'

  # non-standard
  name = 'Bozhidar' unless name
  ```

* <a name="double-amper-preprocess"></a>
  Use `&&=` to preprocess variables that may or may not exist.
<sup>[[link](#double-amper-preprocess)]</sup>

  ```Ruby
  # standard
  something &&= something.downcase

  # standard
  something = something && something.downcase

  # standard
  something = something.downcase if something

  # non-standard
  if something
    something = something.downcase
  end

  # non-standard
  something = something ? nil : something.downcase
  ```

* <a name="no-case-equality"></a>
  Avoid explicit use of the case equality operator `===`.
<sup>[[link](#no-case-equality)]</sup>

  ```Ruby
  # standard
  something.is_a?(Array)
  (1..100).include?(7)
  some_string =~ /something/

  # non-standard
  Array === something
  (1..100) === 7
  /something/ === some_string
  ```

* <a name="no-cryptic-perlisms"></a>
  Do not use Perl-style special variables (like `$:`, `$;`, etc. ).
<sup>[[link](#no-cryptic-perlisms)]</sup>

  ```Ruby
  # standard
  require 'English'
  $LOAD_PATH.unshift File.dirname(__FILE__)

  # non-standard
  $:.unshift File.dirname(__FILE__)
  ```

* <a name="parens-no-spaces"></a>
  Never put a space between a method name and the opening parenthesis.
<sup>[[link](#parens-no-spaces)]</sup>

  ```Ruby
  # standard
  f(3 + 2) + 1

  # non-standard
  f (3 + 2) + 1
  ```

* <a name="parens-as-args"></a>
  If the first argument to a method begins with an open parenthesis, always
  use parentheses in the method invocation. For example, write `f((3 + 2) + 1)`.
<sup>[[link](#parens-as-args)]</sup>

* <a name="global-stdout"></a>
  Use `$stdout/$stderr/$stdin` instead of `STDOUT/STDERR/STDIN`.
  `STDOUT/STDERR/STDIN` are constants, and while you can actually reassign
  (possibly to redirect some stream) constants in Ruby, you'll get an
  interpreter warning if you do so.
<sup>[[link](#global-stdout)]</sup>

* <a name="array-join"></a>
  Favor the use of `Array#join` over `Array#*` with
<sup>[[link](#array-join)]</sup>
  a string argument.

  ```Ruby
  # standard
  %w(one two three).join(', ')
  # => 'one, two, three'

  # non-standard
  %w(one two three) * ', '
  # => 'one, two, three'
  ```

* <a name="splat-arrays"></a>
  Use `[*var]` or `Array()` instead of explicit `Array` check, when dealing
  with a variable you want to treat as an Array, but you're not certain it's an
  array.
<sup>[[link](#splat-arrays)]</sup>

  ```Ruby
  # standard
  [*paths].each { |path| do_something(path) }

  # non-standard
  paths = [paths] unless paths.is_a? Array
  paths.each { |path| do_something(path) }

  # non-standard (and a bit more readable)
  Array(paths).each { |path| do_something(path) }
  ```

* <a name="ranges-or-between"></a>
  Use ranges or `Comparable#between?` instead of comparison logic.
<sup>[[link](#ranges-or-between)]</sup>

  ```Ruby
  # standard
  do_something if (1000..2000).include?(x)

  # standard
  do_something if x.between?(1000, 2000)

  # non-standard
  do_something if x >= 1000 && x <= 2000
  ```

* <a name="predicate-methods"></a>
  Favor the use of predicate methods to explicit comparisons with `==`.
  Numeric comparisons are OK.
<sup>[[link](#predicate-methods)]</sup>

  ```Ruby
  # standard
  if x.even?
  end

  if x.odd?
  end

  if x.nil?
  end

  if x.zero?
  end

  if x == 0
  end

  # non-standard
  if x % 2 == 0
  end

  if x % 2 == 1
  end

  if x == nil
  end
  ```

* <a name="no-non-nil-checks"></a>
  Don't do explicit non-`nil` checks unless you're dealing with boolean
  values.
<sup>[[link](#no-non-nil-checks)]</sup>

  ```ruby
  # standard
  do_something if something

  # standard
  def value_set?
    @some_boolean.present?
  end

  # non-standard
  do_something if !something.nil?
  do_something if something != nil
  ```

* <a name="no-nested-conditionals"></a>
  Avoid use of nested conditionals for flow of control.
<sup>[[link](#no-nested-conditionals)]</sup>

  Prefer a guard clause when you can assert invalid data.

  ```Ruby
  # standard
  def compute_thing(thing)
    return unless thing[:foo]
    update_with_bar(thing[:foo])
    return re_compute(thing) unless thing[:foo][:bar]
    partial_compute(thing)
  end

  # non-standard
  def compute_thing(thing)
    if thing[:foo]
      update_with_bar(thing)
      if thing[:foo][:bar]
        partial_compute(thing)
      else
        re_compute(thing)
      end
    end
  end

  ```

  Prefer `next` in loops instead of conditional blocks.

  ```Ruby
  # standard
  [0, 1, 2, 3].each do |item|
    next unless item > 1
    puts item
  end

  # non-standard
  [0, 1, 2, 3].each do |item|
    if item > 1
      puts item
    end
  end
  ```

## Naming

* <a name="snake-case-symbols-methods-vars"></a>
  Use `snake_case` for symbols, methods and variables.
<sup>[[link](#snake-case-symbols-methods-vars)]</sup>

  ```Ruby
  # standard
  :some_symbol

  def some_method
    ...
  end

  # non-standard
  :'some symbol'
  :SomeSymbol
  :someSymbol

  someVar = 5

  def someMethod
    ...
  end

  def SomeMethod
   ...
  end
  ```

* <a name="camelcase-classes"></a>
  Use `CamelCase` for classes and modules.  (Keep acronyms like HTTP, RFC, XML
  uppercase.)
<sup>[[link](#camelcase-classes)]</sup>

  ```Ruby
  # standard
  class SomeClass
    ...
  end

  class SomeXML
    ...
  end

  # non-standard
  class Someclass
    ...
  end

  class Some_Class
    ...
  end

  class SomeXml
    ...
  end
  ```

* <a name="snake-case-files"></a>
  Use `snake_case` for naming files, e.g. `hello_world.rb`.
<sup>[[link](#snake-case-files)]</sup>

* <a name="snake-case-dirs"></a>
  Use `snake_case` for naming directories, e.g.
  `lib/hello_world/hello_world.rb`.
<sup>[[link](#snake-case-dirs)]</sup>

* <a name="one-class-per-file"></a>
  Aim to have just a single class/module per source file. Name the file name
  as the class/module, but replacing CamelCase with snake_case.
<sup>[[link](#one-class-per-file)]</sup>

* <a name="screaming-snake-case"></a>
  Use `SCREAMING_SNAKE_CASE` for other constants.
<sup>[[link](#screaming-snake-case)]</sup>

  ```Ruby
  # standard
  SOME_CONST = 5

  # non-standard
  SomeConst = 5
  ```

* <a name="bool-methods-qmark"></a>
  The names of predicate methods should
  end in a question mark.  (i.e. `Array#empty?`). Methods that don't return a
  boolean, shouldn't end in a question mark.
<sup>[[link](#bool-methods-qmark)]</sup>

* <a name="dangerous-method-bang"></a>
  The names of potentially *dangerous* methods (i.e. methods that modify
  `self` or the arguments, `exit!` (doesn't run the finalizers like `exit`
  does), etc.) should end with an exclamation mark if there exists a safe
  version of that *dangerous* method.
<sup>[[link](#dangerous-method-bang)]</sup>

  ```Ruby
  # standard
  class Person
    def update
    end
  end

  # standard
  class Person
    def update!
    end

    def update
    end
  end

  # non-standard - there is no matching 'safe' method
  class Person
    def update!
    end
  end
  ```

* <a name="safe-because-unsafe"></a>
  Define the non-bang (safe) method in terms of the bang (dangerous) one if
  possible.
<sup>[[link](#safe-because-unsafe)]</sup>

  ```Ruby
  class Array
    def flatten_once!
      res = []

      each do |e|
        [*e].each { |f| res << f }
      end

      replace(res)
    end

    def flatten_once
      dup.flatten_once!
    end
  end
  ```

* <a name="reduce-blocks"></a>
  When using `reduce` with short blocks, name the arguments `|a, e|`
  (accumulator, element).
<sup>[[link](#reduce-blocks)]</sup>

* <a name="other-arg"></a>
  When defining binary operators, name the argument `other`(`<<` and `[]` are
  exceptions to the rule, since their semantics are different).
<sup>[[link](#other-arg)]</sup>

  ```Ruby
  def +(other)
    # body omitted
  end
  ```

* <a name="map-fine-select-reduce-size"></a>
  Prefer `map` over `collect`, `detect` over `find`, `select` over `find_all`,
  and `size` over `length`. Use `reduce` over `inject` if the result is a single
  object, use `inject` if the result is an enumeration.
<sup>[[link](#map-fine-select-reduce-size)]</sup>

* <a name="count-vs-size"></a>
  Don't use `count` as a substitute for `size`. For `Enumerable` objects other
  than `Array` it will iterate the entire collection in order to determine its
  size.
<sup>[[link](#count-vs-size)]</sup>

  ```Ruby
  # standard
  some_hash.size

  # non-standard
  some_hash.count
  ```

* <a name="flat-map"></a>
  Use `flat_map` instead of `map` + `flatten`.  This does not apply for arrays
  with a depth greater than 2, i.e.  if `users.first.songs == ['a', ['b','c']]`,
  then use `map + flatten` rather than `flat_map`.  `flat_map` flattens the
  array by 1, whereas `flatten` flattens it all the way.
<sup>[[link](#flat-map)]</sup>

  ```Ruby
  # standard
  all_songs = users.flat_map(&:songs).uniq

  # non-standard
  all_songs = users.map(&:songs).flatten.uniq
  ```

* <a name="reverse-each"></a>
  Use `reverse_each` instead of `reverse.each`.
<sup>[[link](#reverse-each)]</sup>

  ```Ruby
  # standard
  array.reverse_each { ... }

  # non-standard
  array.reverse.each { ... }
  ```

## Comments

* <a name="no-comments"></a>
  Write self-documenting code and ignore the rest of this section.
<sup>[[link](#no-comments)]</sup>

* <a name="hash-space"></a>
  Use one space between the leading `#` character of the comment and the text
  of the comment.
<sup>[[link](#hash-space)]</sup>

* <a name="english-syntax"></a>
  Comments longer than a word are capitalized and use punctuation. Use [one
  space](http://en.wikipedia.org/wiki/Sentence_spacing) after periods.
<sup>[[link](#english-syntax)]</sup>

* <a name="no-superfluous-comments"></a>
  No superfluous comments!
<sup>[[link](#no-superfluous-comments)]</sup>

  ```Ruby
  # non-standard
  counter += 1 # Increments counter by one.
  ```

* <a name="comment-upkeep"></a>
  Keep existing comments up-to-date. An outdated comment is worse than no
  comment at all.
<sup>[[link](#comment-upkeep)]</sup>

* <a name="refactor-dont-comment"></a>
  Avoid writing comments to explain bad code. Refactor the code to make it
  self-explanatory. (Do or do not - there is no try. --Yoda)
<sup>[[link](#refactor-dont-comment)]</sup>

### Comment Annotations

* <a name="annotate-above"></a>
  Annotations should usually be written on the line immediately above the
  relevant code.
<sup>[[link](#annotate-above)]</sup>

* <a name="annotate-keywords"></a>
  The annotation keyword is followed by a colon and a space, then a note
  describing the problem.
<sup>[[link](#annotate-keywords)]</sup>

* <a name="indent-annotations"></a>
  If multiple lines are required to describe the problem, subsequent lines
  should not be indented.
<sup>[[link](#indent-annotations)]</sup>

  ```Ruby
  def bar
    # FIXME: This has crashed occasionally since v3.2.1. It may
    # be related to the BarBazUtil upgrade.
    baz(:quux)
  end
  ```

* <a name="rare-eol-annotations"></a>
  In cases where the problem is so obvious that any documentation would be
  redundant, annotations may be left at the end of the offending line with no
  note. This usage should be the exception and not the rule.
<sup>[[link](#rare-eol-annotations)]</sup>

  ```Ruby
  def bar
    sleep 100 # OPTIMIZE
  end
  ```

* <a name="todo"></a>
  Use `TODO` to note missing features or functionality that should be added at
  a later date.
<sup>[[link](#todo)]</sup>

* <a name="fixme"></a>
  Use `FIXME` to note broken code that needs to be fixed.
<sup>[[link](#fixme)]</sup>

* <a name="optimize"></a>
  Use `OPTIMIZE` to note slow or inefficient code that may cause performance
  problems.
<sup>[[link](#optimize)]</sup>

* <a name="hack"></a>
  Use `HACK` to note code smells where questionable coding practices were used
  and should be refactored away.
<sup>[[link](#hack)]</sup>

* <a name="review"></a>
  Use `REVIEW` to note anything that should be looked at to confirm it is
  working as intended. For example: `REVIEW: Are we sure this is how the client
  does X currently?`
<sup>[[link](#review)]</sup>

* <a name="document-annotations"></a>
  Use other custom annotation keywords if it feels appropriate, but be sure to
  document them in your project's `README` or similar.
<sup>[[link](#document-annotations)]</sup>

## Classes & Modules

* <a name="consistent-classes"></a>
  Use a consistent structure in your class definitions.
<sup>[[link](#consistent-classes)]</sup>

  ```Ruby
  class Person
    # extend and include go first
    extend SomeModule
    include AnotherModule

    # inner classes
    CustomErrorKlass = Class.new(StandardError)

    # constants are next
    SOME_CONSTANT = 20

    # afterwards we have attribute macros
    attr_reader :name

    # followed by other macros (if any)
    validates :name

    # public class methods are next in line
    class << self
      def some_method
      end
    end

    # followed by public instance methods
    def some_method
    end

    # protected and private methods are grouped near the end
    protected

    def some_protected_method
    end

    private

    def some_private_method
    end
  end
  ```

* <a name="modules-vs-classes"></a>
  Prefer modules to classes with only class methods. Classes should be used
  only when it makes sense to create instances out of them.
<sup>[[link](#modules-vs-classes)]</sup>

  ```Ruby
  # standard
  module SomeClass
    module_function

    def some_method
      # body omitted
    end

    def some_other_method
    end
  end

  # non-standard
  class SomeClass
    def self.some_method
      # body omitted
    end

    def self.some_other_method
    end
  end
  ```

* <a name="namespaces"></a>
  Declare module namespaces separately.
<sup>[[link](#namespaces)]</sup>

  ```Ruby
  # standard
  module Namespace
    class SomeClass
      # body omitted
    end
  end

  # non-standard
  class Namespace::SomeClass
    # body omitted
  end
  ```

* <a name="module-function"></a>
  Favor the use of `module_function` over `extend self` when you want to turn
  a module's instance methods into class methods.
<sup>[[link](#module-function)]</sup>

  ```Ruby
  # standard
  module Utilities
    module_function

    def parse_something(string)
      # do stuff here
    end

    def other_utility_method(number, string)
      # do some more stuff
    end
  end

  # non-standard
  module Utilities
    extend self

    def parse_something(string)
      # do stuff here
    end

    def other_utility_method(number, string)
      # do some more stuff
    end
  end
  ```

* <a name="attr_family"></a>
  Use the `attr` family of functions to define trivial accessors or mutators.
<sup>[[link](#attr_family)]</sup>

  ```Ruby
  # non-standard
  class Person
    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end

    def first_name
      @first_name
    end

    def last_name
      @last_name
    end
  end

  # standard
  class Person
    attr_reader :first_name, :last_name

    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end
  end
  ```

* <a name="define-to-s"></a>
  Always supply a proper `to_s` method for classes that represent domain
  objects.
<sup>[[link](#define-to-s)]</sup>

  ```Ruby
  class Person
    attr_accessor :first_name, :last_name

    def initialize(first_name, last_name)
      self.first_name = first_name
      self.last_name = last_name
    end

    def to_s
      "#{first_name} #{last_name}"
    end
  end
  ```

* <a name="duck-typing"></a>
  Prefer [duck-typing](http://en.wikipedia.org/wiki/Duck_typing) over
  inheritance, assuming there are no common implementations of methods.
<sup>[[link](#duck-typing)]</sup>

  ```Ruby
  # standard
  class Duck
    def speak
      puts 'Quack! Quack'
    end
  end

  class Dog
    def speak
      puts 'Bau! Bau!'
    end
  end

  # non-standard
  class Animal
    # abstract method
    def speak
    end
  end

  class Duck < Animal
    def speak
      puts 'Quack! Quack'
    end
  end

  class Dog < Animal
    def speak
      puts 'Bau! Bau!'
    end
  end
  ```

* <a name="no-class-vars"></a>
  Avoid the usage of class (`@@`) variables.
<sup>[[link](#no-class-vars)]</sup>

  ```Ruby
  class Parent
    @@class_var = 'parent'

    def self.print_class_var
      puts @@class_var
    end
  end

  class Child < Parent
    @@class_var = 'child'
  end

  Parent.print_class_var # => will print "child"
  ```

* <a name="visibility"></a>
  Assign proper visibility levels to methods (`private`, `protected`) in
  accordance with their intended usage.
<sup>[[link](#visibility)]</sup>

* <a name="indent-public-private-protected"></a>
  Indent the `public`, `protected`, and `private` methods as much the method
  definitions they apply to. Leave one blank line above the visibility modifier
  and one blank line below in order to emphasize that it applies to all methods
  below it.
<sup>[[link](#indent-public-private-protected)]</sup>

  ```Ruby
  class SomeClass
    def public_method
      # ...
    end

    private

    def private_method
      # ...
    end

    def another_private_method
      # ...
    end
  end
  ```

* <a name="def-self-singletons"></a>
  Use `class << self` to define singleton methods.
<sup>[[link](#def-self-singletons)]</sup>

  ```Ruby
  class TestClass
    # standard
    class << self
      def first_method
        # body omitted
      end

      def second_method_etc
        # body omitted
      end
    end

    # non-standard
    def self.some_other_method
      # body omitted
    end

    # non-standard
    def TestClass.some_method
      # body omitted
    end
  end
  ```

## Exceptions

* <a name="fail-method"></a>
  Signal exceptions using the `fail` method. Use `raise` only when catching an
  exception and re-raising it (because here you're not failing, but explicitly
  and purposefully raising an exception).
<sup>[[link](#fail-method)]</sup>

  ```Ruby
  begin
    fail 'Oops'
  rescue => error
    raise if error.message != 'Oops'
  end
  ```

* <a name="no-explicit-runtimeerror"></a>
  Don't specify `RuntimeError` explicitly in the two argument version of
  `fail/raise`.
<sup>[[link](#no-explicit-runtimeerror)]</sup>

  ```Ruby
  # standard
  fail 'message'

  # non-standard
  fail RuntimeError, 'message'
  ```

* <a name="exception-class-messages"></a>
  Prefer supplying an exception class and a message as two separate arguments
  to `fail/raise`, instead of an exception instance.
<sup>[[link](#exception-class-messages)]</sup>

  ```Ruby
  # standard
  fail SomeException, 'message'

  # non-standard
  fail SomeException.new('message')
  ```

* <a name="no-return-ensure"></a>
  Never return from an `ensure` block.
<sup>[[link](#no-return-ensure)]</sup>

  ```Ruby
  def foo
    begin
      fail
    ensure
      return 'very bad idea'
    end
  end
  ```

* <a name="begin-implicit"></a>
  Use *implicit begin blocks* where possible.
<sup>[[link](#begin-implicit)]</sup>

  ```Ruby
  # standard
  def foo
    # main logic goes here
  rescue
    # failure handling goes here
  end

  # non-standard
  def foo
    begin
      # main logic goes here
    rescue
      # failure handling goes here
    end
  end
  ```

* <a name="contingency-methods"></a>
  Mitigate the proliferation of `begin` blocks by using contingency methods
<sup>[[link](#contingency-methods)]</sup>

  ```Ruby
  # standard
  def with_io_error_handling
     yield
  rescue IOError
    # handle IOError
  end

  with_io_error_handling { something_that_might_fail }

  with_io_error_handling { something_else_that_might_fail }

  # non-standard
  begin
    something_that_might_fail
  rescue IOError
    # handle IOError
  end

  begin
    something_else_that_might_fail
  rescue IOError
    # handle IOError
  end
  ```

* <a name="dont-hide-exceptions"></a>
  Don't suppress exceptions.
<sup>[[link](#dont-hide-exceptions)]</sup>

  ```Ruby
  # non-standard
  do_something rescue nil

  # non-standard
  begin
    # an exception occurs here
  rescue SomeError
    # the rescue clause does absolutely nothing
  end
  ```

* <a name="no-rescue-modifiers"></a>
  Always specify an exception type in the rescue clause.
<sup>[[link](#no-rescue-modifiers)]</sup>

  ```Ruby
  # standard
  def foo
    read_file
  rescue Errno::ENOENT => e
    handle_error(e)
  end
  ```

* <a name="no-exceptional-flows"></a>
  Don't use exceptions for flow of control.
<sup>[[link](#no-exceptional-flows)]</sup>

  ```Ruby
  # standard
  if d.zero?
    puts 'Cannot divide by 0!'
  else
    n / d
  end

  # non-standard
  begin
    n / d
  rescue ZeroDivisionError
    puts 'Cannot divide by 0!'
  end
  ```

* <a name="file-close"></a>
  Release external resources obtained by your program in an ensure block.
<sup>[[link](#file-close)]</sup>

  ```Ruby
  f = File.open('testfile')
  begin
    # .. process
  rescue
    # .. handle error
  ensure
    f.close if f
  end
  ```

* <a name="standard-exceptions"></a>
  Favor the use of exceptions for the standard library over introducing new
  exception classes.
<sup>[[link](#standard-exceptions)]</sup>

## Collections

* <a name="literal-array-hash"></a>
  Prefer literal array and hash creation notation (unless you need to pass
  parameters to their constructors, that is).
<sup>[[link](#literal-array-hash)]</sup>

  ```Ruby
  # standard
  arr = []
  hash = {}

  # non-standard
  arr = Array.new
  hash = Hash.new
  ```

* <a name="percent-w"></a>
  Prefer `%w` to the literal array syntax when you need an array of words.  Apply this
  rule only to arrays with two or more elements.
<sup>[[link](#percent-w)]</sup>

  ```Ruby
  # standard
  states = %w(draft open closed)

  # non-standard
  states = ['draft', 'open', 'closed']
  ```

* <a name="percent-i"></a>
  Prefer `%i` to the literal array syntax when you need an array of symbols
  (and you don't need to maintain Ruby 1.9 compatibility). Apply this rule only
  to arrays with two or more elements.
<sup>[[link](#percent-i)]</sup>

  ```Ruby
  # standard
  states = %i(draft open closed)

  # non-standard
  states = [:draft, :open, :closed]
  ```

* <a name="no-trailing-array-commas"></a>
  Avoid comma after the last item of an `Array` or `Hash` literal, especially
  when the items are not on separate lines.
<sup>[[link](#no-trailing-array-commas)]</sup>

  ```Ruby
  # standard
  values = [1001, 2020, 3333]

  # non-standard
  values = [1001, 2020, 3333, ]
  ```

* <a name="first-and-last"></a>
  When accessing the first or last element from an array, prefer `first` or
  `last` over `[0]` or `[-1]`.
<sup>[[link](#first-and-last)]</sup>

* <a name="set-vs-array"></a>
  Use `Set` instead of `Array` when dealing with unique elements.
<sup>[[link](#set-vs-array)]</sup>

* <a name="symbols-as-keys"></a>
  Prefer symbols instead of strings as hash keys.
<sup>[[link](#symbols-as-keys)]</sup>

  ```Ruby
  # standard
  hash = { one: 1, two: 2, three: 3 }

  # non-standard
  hash = { 'one' => 1, 'two' => 2, 'three' => 3 }
  ```

* <a name="no-mutable-keys"></a>
  Avoid the use of mutable objects as hash keys.
<sup>[[link](#no-mutable-keys)]</sup>

* <a name="hash-literals"></a>
  Use hash rockets consistently.
<sup>[[link](#hash-literals)]</sup>

  ```Ruby
  # standard
  hash = { :one => 1, :two => 2, :three => 3 }

  # non-standard
  hash = { one: 1, two: 2, three: 3 }
  ```

* <a name="hash-key"></a>
  Use `Hash#key?` instead of `Hash#has_key?` and `Hash#value?` instead of
  `Hash#has_value?`. As noted
  [here](http://blade.nagaokaut.ac.jp/cgi-bin/scat.rb/ruby/ruby-core/43765) by
  Matz, the longer forms are considered deprecated.
<sup>[[link](#hash-key)]</sup>

  ```Ruby
  # standard
  hash.key?(:test)
  hash.value?(value)

  # non-standard
  hash.has_key?(:test)
  hash.has_value?(value)
  ```

* <a name="hash-fetch"></a>
  Use `Hash#fetch` when dealing with hash keys that should be present.
<sup>[[link](#hash-fetch)]</sup>

  ```Ruby
  heroes = { :batman => 'Bruce Wayne', :superman => 'Clark Kent' }

  # standard
  heroes.fetch(:supermann) # raises a KeyError making the problem obvious

  # non-standard
  heroes[:batman] # => "Bruce Wayne"
  heroes[:supermann] # => nil
  ```

* <a name="hash-fetch-defaults"></a>
  Introduce default values for hash keys via `Hash#fetch` as opposed to using
  custom logic.
<sup>[[link](#hash-fetch-defaults)]</sup>

  ```Ruby
  # standard
  batman.fetch(:is_evil, true) # => false
  ```

* <a name="use-hash-blocks"></a>
  Prefer the use of the block instead of the default value in `Hash#fetch`.
<sup>[[link](#use-hash-blocks)]</sup>

  ```Ruby
  # standard
  batman.fetch(:powers) { get_batman_powers }

  # non-standard
  batman.fetch(:powers, get_batman_powers)
  ```

* <a name="hash-values-at"></a>
  Use `Hash#values_at` when you need to retrieve several values consecutively
  from a hash.
<sup>[[link](#hash-values-at)]</sup>

  ```Ruby
  # standard
  email, username = data.values_at('email', 'nickname')

  # non-standard
  email = data['email']
  nickname = data['nickname']
  ```

* <a name="ordered-hashes"></a>
  Rely on the fact that as of Ruby 1.9 hashes are ordered.
<sup>[[link](#ordered-hashes)]</sup>

* <a name="no-modifying-collections"></a>
  Never modify a collection while traversing it.
<sup>[[link](#no-modifying-collections)]</sup>

## Strings

* <a name="string-interpolation"></a>
  Prefer string interpolation instead of string
  concatenation:
<sup>[[link](#string-interpolation)]</sup>

  ```Ruby
  # standard
  email_with_name = "#{user.name} <#{user.email}>"

  # non-standard
  email_with_name = user.name + ' <' + user.email + '>'
  ```

* <a name="consistent-string-literals"></a>
  Use single quotes by default
<sup>[[link](#consistent-string-literals)]</sup>

  ```Ruby
  # standard
  name = 'Bozhidar'

  # non-standard
  name = "Bozhidar"
  ```

## Regular Expressions

* <a name="no-regexp-for-plaintext"></a>
  Don't use regular expressions if you just need plain text search in string:
  `string['text']`
<sup>[[link](#no-regexp-for-plaintext)]</sup>

* <a name="regexp-string-index"></a>
  For simple constructions you can use regexp directly through string index.
<sup>[[link](#regexp-string-index)]</sup>

  ```Ruby
  match = string[/regexp/]             # get content of matched regexp
  first_group = string[/text(grp)/, 1] # get content of captured group
  string[/text (grp)/, 1] = 'replace'  # string => 'text replace'
  ```

* <a name="non-capturing-regexp"></a>
  Use non-capturing groups when you don't use captured result of parentheses.
<sup>[[link](#non-capturing-regexp)]</sup>

  ```Ruby
  /(?:first|second)/ # standard
  /(first|second)/   # non-standard
  ```

* <a name="no-perl-regexp-last-matchers"></a>
  Don't use the cryptic Perl-legacy variables denoting last regexp group
  matches (`$1`, `$2`, etc). Use `Regexp.last_match[n]` instead.
<sup>[[link](#no-perl-regexp-last-matchers)]</sup>

  ```Ruby
  /(regexp)/ =~ string
  ...

  # standard
  process Regexp.last_match[1]

  # non-standard
  process $1

  ```

* <a name="no-numbered-regexes"></a>
  Avoid using numbered groups as it can be hard to track what they contain.
  Named groups can be used instead.
<sup>[[link](#no-numbered-regexes)]</sup>

  ```Ruby
  # standard
  /(?<meaningful_var>regexp)/ =~ string
  ...
  process meaningful_var

  # non-standard
  /(regexp)/ =~ string
  ...
  process Regexp.last_match[1]
  ```

* <a name="limit-escapes"></a>
  Character classes have only a few special characters you should care about:
  `^`, `-`, `\`, `]`, so don't escape `.` or brackets in `[]`.
<sup>[[link](#limit-escapes)]</sup>

* <a name="caret-and-dollar-regexp"></a>
  Be careful with `^` and `$` as they match start/end of line, not string
  endings.  If you want to match the whole string use: `\A` and `\z` (not to be
  confused with `\Z` which is the equivalent of `/\n?\z/`).
<sup>[[link](#caret-and-dollar-regexp)]</sup>

  ```Ruby
  string = "some injection\nusername"
  string[/^username$/]   # matches
  string[/\Ausername\z/] # doesn't match
  ```

* <a name="comment-regexes"></a>
  Use `x` modifier for complex regexps. This makes them more readable and you
  can add some useful comments. Just be careful as spaces are ignored.
<sup>[[link](#comment-regexes)]</sup>

  ```Ruby
  regexp = /
    start         # some text
    \s            # white space char
    (group)       # first group
    (?:alt1|alt2) # some alternation
    end
  /x
  ```

* <a name="gsub-blocks"></a>
  For complex replacements `sub`/`gsub` can be used with block or hash.
<sup>[[link](#gsub-blocks)]</sup>

## Percent Literals

* <a name="percent-q-shorthand"></a>
  Use `%()`(it's a shorthand for `%Q`) for single-line strings which require
  both interpolation and embedded double-quotes. For multi-line strings, prefer
  heredocs.
<sup>[[link](#percent-q-shorthand)]</sup>

  ```Ruby
  # standard (requires interpolation, has quotes, single line)
  %(<tr><td class="name">#{name}</td>)

  # non-standard (no interpolation needed)
  %(<div class="text">Some text</div>)
  # should be '<div class="text">Some text</div>'

  # non-standard (no double-quotes)
  %(This is #{quality} style)
  # should be "This is #{quality} style"

  # non-standard (multiple lines)
  %(<div>\n<span class="big">#{exclamation}</span>\n</div>)
  # should be a heredoc.
  ```

* <a name="percent-q"></a>
  Avoid `%q` unless you have a string with both `'` and `"` in it. Regular
  string literals are more readable and should be preferred unless a lot of
  characters would have to be escaped in them.
<sup>[[link](#percent-q)]</sup>

  ```Ruby
  # standard
  name = 'Bruce Wayne'
  time = "8 o'clock"
  question = '"What did you say?"'

  # non-standard
  name = %q(Bruce Wayne)
  time = %q(8 o'clock)
  question = %q("What did you say?")
  ```

* <a name="percent-r"></a>
  Use `%r` only for regular expressions matching *more than* one '/'
  character.
<sup>[[link](#percent-r)]</sup>

  ```Ruby
  # standard
  %r(^/blog/2011/(.*)$)

  # non-standard
  %r(\s+)

  # non-standard
  %r(^/(.*)$)
  # should be /^\/(.*)$/
  ```

* <a name="percent-x"></a>
  Avoid the use of `%x` unless you're going to invoke a command with
  backquotes in it(which is rather unlikely).
<sup>[[link](#percent-x)]</sup>

  ```Ruby
  # standard
  date = `date`
  echo = %x(echo `date`)

  # non-standard
  date = %x(date)
  ```

* <a name="percent-s"></a>
  Avoid the use of `%s`. It seems that the community has decided `:"some
  string"` is the preferred way to create a symbol with spaces in it.
<sup>[[link](#percent-s)]</sup>

* <a name="percent-literal-braces"></a>
  Prefer `()` as delimiters for all `%` literals, except `%r`. Since braces
  often appear inside regular expressions in many scenarios a less common
  character like `{` might be a better choice for a delimiter, depending on the
  regexp's content.
<sup>[[link](#percent-literal-braces)]</sup>

  ```Ruby
  # standard
  %w(one two three)
  %q("Test's king!", John said.)

  # non-standard
  %w[one two three]
  %q{"Test's king!", John said.}
  ```

## Misc (and stil important)

* <a name="functional-code"></a>
  Code in a functional way, avoiding mutation when that makes sense.
<sup>[[link](#functional-code)]</sup>

* <a name="short-methods"></a>
  Avoid methods longer than 1 line of code inside the def end block.
<sup>[[link](#short-methods)]</sup>

* <a name="no-optional-hash-params"></a>
  Avoid hashes as optional parameters.
<sup>[[link](#no-optional-hash-params)]</sup>

* <a name="too-many-params"></a>
  Avoid parameter lists longer than three parameters.
<sup>[[link](#too-many-params)]</sup>

* <a name="instance-vars"></a>
  Use module instance variables instead of global variables.
<sup>[[link](#instance-vars)]</sup>

  ```Ruby
  # standard
  module Foo
    class << self
      attr_accessor :bar
    end
  end

  Foo.bar = 1

  # non-standard
  $foo_bar = 1
  ```

* <a name="alias-method"></a>
  Avoid `alias` when `alias_method` will do.
<sup>[[link](#alias-method)]</sup>

* <a name="optionparser"></a>
  Use `OptionParser` for parsing complex command line options and `ruby -s`
  for trivial command line options.
<sup>[[link](#optionparser)]</sup>

* <a name="time-now"></a>
  Prefer `Time.now` over `Time.new` when retrieving the current system time.
<sup>[[link](#time-now)]</sup>

* <a name="no-arg-mutations"></a>
  Do not mutate arguments unless that is the purpose of the method.
<sup>[[link](#no-arg-mutations)]</sup>

* <a name="three-is-the-number-thou-shalt-count"></a>
  Avoid more than three levels of block nesting.
<sup>[[link](#three-is-the-number-thou-shalt-count)]</sup>
