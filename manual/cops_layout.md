# Layout

## Layout/AccessModifierIndentation

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Modifiers should be indented as deep as method definitions, or as deep
as the class/module keyword, depending on configuration.

### Example

```ruby
# bad
class Plumbus
private
  def smooth; end
end

# good
class Plumbus
  private
  def smooth; end
end
```
```ruby
# bad
class Plumbus
  private
  def smooth; end
end

# good
class Plumbus
private
  def smooth; end
end
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `indent` | `outdent`, `indent`
IndentationWidth | `<none>` | Integer

### References

* [https://github.com/bbatsov/ruby-style-guide#indent-public-private-protected](https://github.com/bbatsov/ruby-style-guide#indent-public-private-protected)

## Layout/AlignArray

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Here we check if the elements of a multi-line array literal are
aligned.

### Example

```ruby
# bad
a = [1, 2, 3,
  4, 5, 6]
array = ['run',
     'forrest',
     'run']

# good
a = [1, 2, 3,
     4, 5, 6]
a = ['run',
     'forrest',
     'run']
```

### References

* [https://github.com/bbatsov/ruby-style-guide#align-multiline-arrays](https://github.com/bbatsov/ruby-style-guide#align-multiline-arrays)

## Layout/AlignHash

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Check that the keys, separators, and values of a multi-line hash
literal are aligned according to configuration. The configuration
options are:

  - key (left align keys)
  - separator (align hash rockets and colons, right align keys)
  - table (left align keys, hash rockets, and values)

The treatment of hashes passed as the last argument to a method call
can also be configured. The options are:

  - always_inspect
  - always_ignore
  - ignore_implicit (without curly braces)
  - ignore_explicit (with curly braces)

### Example

```ruby
# EnforcedHashRocketStyle: key (default)
# EnforcedColonStyle: key (default)

# good
{
  foo: bar,
  ba: baz
}
{
  :foo => bar,
  :ba => baz
}

# bad
{
  foo: bar,
   ba: baz
}
{
  :foo => bar,
   :ba => baz
}
```
```ruby
# EnforcedHashRocketStyle: separator
# EnforcedColonStyle: separator

#good
{
  foo: bar,
   ba: baz
}
{
  :foo => bar,
   :ba => baz
}

#bad
{
  foo: bar,
  ba: baz
}
{
  :foo => bar,
  :ba => baz
}
{
  :foo => bar,
  :ba  => baz
}
```
```ruby
# EnforcedHashRocketStyle: table
# EnforcedColonStyle: table

#good
{
  foo: bar,
  ba:  baz
}
{
  :foo => bar,
  :ba  => baz
}

#bad
{
  foo: bar,
  ba: baz
}
{
  :foo => bar,
   :ba => baz
}
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedHashRocketStyle | `key` | `key`, `separator`, `table`
EnforcedColonStyle | `key` | `key`, `separator`, `table`
EnforcedLastArgumentHashStyle | `always_inspect` | `always_inspect`, `always_ignore`, `ignore_implicit`, `ignore_explicit`

## Layout/AlignParameters

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Here we check if the parameters on a multi-line method call or
definition are aligned.

### Example

```ruby
# good

foo :bar,
    :baz

# bad

foo :bar,
  :baz
```
```ruby
# good

foo :bar,
  :baz

# bad

foo :bar,
    :baz
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `with_first_parameter` | `with_first_parameter`, `with_fixed_indentation`
IndentationWidth | `<none>` | Integer

### References

* [https://github.com/bbatsov/ruby-style-guide#no-double-indent](https://github.com/bbatsov/ruby-style-guide#no-double-indent)

## Layout/BlockEndNewline

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks whether the end statement of a do..end block
is on its own line.

### Example

```ruby
# bad
blah do |i|
  foo(i) end

# good
blah do |i|
  foo(i)
end

# bad
blah { |i|
  foo(i) }

# good
blah { |i|
  foo(i)
}
```

## Layout/CaseIndentation

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks how the *when*s of a *case* expression
are indented in relation to its *case* or *end* keyword.

It will register a separate offense for each misaligned *when*.

### Example

```ruby
# If Layout/EndAlignment is set to keyword style (default)
# *case* and *end* should always be aligned to same depth,
# and therefore *when* should always be aligned to both -
# regardless of configuration.

# bad for all styles
case n
  when 0
    x * 2
  else
    y / 3
end

# good for all styles
case n
when 0
  x * 2
else
  y / 3
end
```
```ruby
# if EndAlignment is set to other style such as
# start_of_line (as shown below), then *when* alignment
# configuration does have an effect.

# bad
a = case n
when 0
  x * 2
else
  y / 3
end

# good
a = case n
    when 0
      x * 2
    else
      y / 3
end
```
```ruby
# bad
a = case n
    when 0
      x * 2
    else
      y / 3
end

# good
a = case n
when 0
  x * 2
else
  y / 3
end
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `case` | `case`, `end`
IndentOneStep | `false` | Boolean
IndentationWidth | `<none>` | Integer

### References

* [https://github.com/bbatsov/ruby-style-guide#indent-when-to-case](https://github.com/bbatsov/ruby-style-guide#indent-when-to-case)

## Layout/ClassStructure

Enabled by default | Supports autocorrection
--- | ---
Disabled | Yes

Checks if the code style follows the ExpectedOrder configuration:

`Categories` allows us to map macro names into a category.

Consider an example of code style that covers the following order:
- Constants
- Associations (has_one, has_many)
- Attributes (attr_accessor, attr_writer, attr_reader)
- Initializer
- Instance methods
- Protected methods
- Private methods

You can configure the following order:

```yaml
 Layout/ClassStructure:
   Categories:
     module_inclusion:
       - include
       - prepend
       - extend
   ExpectedOrder:
       - module_inclusion
       - constants
       - public_class_methods
       - initializer
       - public_methods
       - protected_methods
       - private_methods

```
Instead of putting all literals in the expected order, is also
possible to group categories of macros.

```yaml
 Layout/ClassStructure:
   Categories:
     association:
       - has_many
       - has_one
     attribute:
       - attr_accessor
       - attr_reader
       - attr_writer
```

### Example

```ruby
# bad: Expect extend be before constant
class Person < ApplicationRecord
  has_many :orders
  ANSWER = 42

  extend SomeModule
  include AnotherModule
end
```
```ruby
class Person
  # extend and include go first
  extend SomeModule
  include AnotherModule

  # inner classes
  CustomError = Class.new(StandardError)

  # constants are next
  SOME_CONSTANT = 20

  # afterwards we have attribute macros
  attr_reader :name

  # followed by other macros (if any)
  validates :name

  # public class methods are next in line
  def self.some_method
  end

  # initialization goes between class methods and instance methods
  def initialize
  end

  # followed by other public instance methods
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

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
Categories | `{"module_inclusion"=>["include", "prepend", "extend"]}` | 
ExpectedOrder | `module_inclusion`, `constants`, `public_class_methods`, `initializer`, `public_methods`, `protected_methods`, `private_methods` | Array

### References

* [https://github.com/bbatsov/ruby-style-guide#consistent-classes](https://github.com/bbatsov/ruby-style-guide#consistent-classes)

## Layout/ClosingParenthesisIndentation

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks the indentation of hanging closing parentheses in
method calls, method definitions, and grouped expressions. A hanging
closing parenthesis means `)` preceded by a line break.

### Example

```ruby
# good: when x is on its own line, indent this way
func(
  x,
  y
)

# good: when x follows opening parenthesis, align parentheses
a = b * (x +
         y
        )

# bad
def func(
  x,
  y
  )
end
```

## Layout/CommentIndentation

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks the indentation of comments.

### Example

```ruby
# bad
  # comment here
def method_name
end

  # comment here
a = 'hello'

# yet another comment
  if true
    true
  end

# good
# comment here
def method_name
end

# comment here
a = 'hello'

# yet another comment
if true
  true
end
```

## Layout/DotPosition

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks the . position in multi-line method calls.

### Example

```ruby
# bad
something.
  mehod

# good
something
  .method
```
```ruby
# bad
something
  .method

# good
something.
  mehod
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `leading` | `leading`, `trailing`

### References

* [https://github.com/bbatsov/ruby-style-guide#consistent-multi-line-chains](https://github.com/bbatsov/ruby-style-guide#consistent-multi-line-chains)

## Layout/ElseAlignment

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks the alignment of else keywords. Normally they should
be aligned with an if/unless/while/until/begin/def keyword, but there
are special cases when they should follow the same rules as the
alignment of end.

### Example

```ruby
# bad
if something
  code
 else
  code
end

# bad
if something
  code
 elsif something
  code
end

# good
if something
  code
else
  code
end
```

## Layout/EmptyLineAfterMagicComment

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks for a newline after the final magic comment.

### Example

```ruby
# good
# frozen_string_literal: true

# Some documentation for Person
class Person
  # Some code
end

# bad
# frozen_string_literal: true
# Some documentation for Person
class Person
  # Some code
end
```

### References

* [https://github.com/bbatsov/ruby-style-guide#separate-magic-comments-from-code](https://github.com/bbatsov/ruby-style-guide#separate-magic-comments-from-code)

## Layout/EmptyLineBetweenDefs

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks whether method definitions are
separated by one empty line.

`NumberOfEmptyLines` can be and integer (e.g. 1 by default) or
an array (e.g. [1, 2]) to specificy a minimum and a maximum of
empty lines.

`AllowAdjacentOneLineDefs` can be used to configure is adjacent
one line methods definitions are an offense

### Example

```ruby
# bad
def a
end
def b
end
```
```ruby
# good
def a
end

def b
end
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
AllowAdjacentOneLineDefs | `false` | Boolean
NumberOfEmptyLines | `1` | Integer

### References

* [https://github.com/bbatsov/ruby-style-guide#empty-lines-between-methods](https://github.com/bbatsov/ruby-style-guide#empty-lines-between-methods)

## Layout/EmptyLines

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks for two or more consecutive blank lines.

### Example

```ruby
# bad - It has two empty lines.
some_method
# one empty line
# two empty lines
some_method

# good
some_method
# one empty line
some_method
```

### References

* [https://github.com/bbatsov/ruby-style-guide#two-or-more-empty-lines](https://github.com/bbatsov/ruby-style-guide#two-or-more-empty-lines)

## Layout/EmptyLinesAroundAccessModifier

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Access modifiers should be surrounded by blank lines.

### Example

```ruby
# bad
class Foo
  def bar; end
  private
  def baz; end
end

# good
class Foo
  def bar; end

  private

  def baz; end
end
```

### References

* [https://github.com/bbatsov/ruby-style-guide#empty-lines-around-access-modifier](https://github.com/bbatsov/ruby-style-guide#empty-lines-around-access-modifier)

## Layout/EmptyLinesAroundBeginBody

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks if empty lines exist around the bodies of begin-end
blocks.

### Example

```ruby
# good

begin
  # ...
end

# bad

begin

  # ...

end
```

### References

* [https://github.com/bbatsov/ruby-style-guide#empty-lines-around-bodies](https://github.com/bbatsov/ruby-style-guide#empty-lines-around-bodies)

## Layout/EmptyLinesAroundBlockBody

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks if empty lines around the bodies of blocks match
the configuration.

### Example

```ruby
# good

foo do |bar|

  # ...

end
```
```ruby
# good

foo do |bar|
  # ...
end
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `no_empty_lines` | `empty_lines`, `no_empty_lines`

### References

* [https://github.com/bbatsov/ruby-style-guide#empty-lines-around-bodies](https://github.com/bbatsov/ruby-style-guide#empty-lines-around-bodies)

## Layout/EmptyLinesAroundClassBody

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks if empty lines around the bodies of classes match
the configuration.

### Example

```ruby
# good

class Foo

  def bar
    # ...
  end

end
```
```ruby
# good

class Foo
  class Bar

    # ...

  end
end
```
```ruby
# good
class Foo

  def bar; end

end
```
```ruby
# good

class Foo
  def bar
    # ...
  end
end
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `no_empty_lines` | `empty_lines`, `empty_lines_except_namespace`, `empty_lines_special`, `no_empty_lines`

### References

* [https://github.com/bbatsov/ruby-style-guide#empty-lines-around-bodies](https://github.com/bbatsov/ruby-style-guide#empty-lines-around-bodies)

## Layout/EmptyLinesAroundExceptionHandlingKeywords

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks if empty lines exist around the bodies of `begin`
sections. This cop doesn't check empty lines at `begin` body
beginning/end and around method definition body.
`Style/EmptyLinesAroundBeginBody` or `Style/EmptyLinesAroundMethodBody`
can be used for this purpose.

### Example

```ruby
# good

begin
  do_something
rescue
  do_something2
else
  do_something3
ensure
  do_something4
end

# good

def foo
  do_something
rescue
  do_something2
end

# bad

begin
  do_something

rescue

  do_something2

else

  do_something3

ensure

  do_something4
end

# bad

def foo
  do_something

rescue

  do_something2
end
```

### References

* [https://github.com/bbatsov/ruby-style-guide#empty-lines-around-bodies](https://github.com/bbatsov/ruby-style-guide#empty-lines-around-bodies)

## Layout/EmptyLinesAroundMethodBody

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks if empty lines exist around the bodies of methods.

### Example

```ruby
# good

def foo
  # ...
end

# bad

def bar

  # ...

end
```

### References

* [https://github.com/bbatsov/ruby-style-guide#empty-lines-around-bodies](https://github.com/bbatsov/ruby-style-guide#empty-lines-around-bodies)

## Layout/EmptyLinesAroundModuleBody

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks if empty lines around the bodies of modules match
the configuration.

### Example

```ruby
# good

module Foo

  def bar
    # ...
  end

end
```
```ruby
# good

module Foo
  module Bar

    # ...

  end
end
```
```ruby
# good
module Foo

  def bar; end

end
```
```ruby
# good

module Foo
  def bar
    # ...
  end
end
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `no_empty_lines` | `empty_lines`, `empty_lines_except_namespace`, `empty_lines_special`, `no_empty_lines`

### References

* [https://github.com/bbatsov/ruby-style-guide#empty-lines-around-bodies](https://github.com/bbatsov/ruby-style-guide#empty-lines-around-bodies)

## Layout/EndOfLine

Enabled by default | Supports autocorrection
--- | ---
Enabled | No

This cop checks for Windows-style line endings in the source code.

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `native` | `native`, `lf`, `crlf`

### References

* [https://github.com/bbatsov/ruby-style-guide#crlf](https://github.com/bbatsov/ruby-style-guide#crlf)

## Layout/ExtraSpacing

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks for extra/unnecessary whitespace.

### Example

```ruby
# good if AllowForAlignment is true
name      = "RuboCop"
# Some comment and an empty line

website  += "/bbatsov/rubocop" unless cond
puts        "rubocop"          if     debug

# bad for any configuration
set_app("RuboCop")
website  = "https://github.com/bbatsov/rubocop"
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
AllowForAlignment | `true` | Boolean
ForceEqualSignAlignment | `false` | Boolean

## Layout/FirstArrayElementLineBreak

Enabled by default | Supports autocorrection
--- | ---
Disabled | Yes

This cop checks for a line break before the first element in a
multi-line array.

### Example

```ruby
# bad
[ :a,
  :b]

# good
[
  :a,
  :b]
```

## Layout/FirstHashElementLineBreak

Enabled by default | Supports autocorrection
--- | ---
Disabled | Yes

This cop checks for a line break before the first element in a
multi-line hash.

### Example

```ruby
# bad
{ a: 1,
  b: 2}

# good
{
  a: 1,
  b: 2 }
```

## Layout/FirstMethodArgumentLineBreak

Enabled by default | Supports autocorrection
--- | ---
Disabled | Yes

This cop checks for a line break before the first argument in a
multi-line method call.

### Example

```ruby
# bad
method(foo, bar,
  baz)

# good
method(
  foo, bar,
  baz)

# ignored
method foo, bar,
  baz
```

## Layout/FirstMethodParameterLineBreak

Enabled by default | Supports autocorrection
--- | ---
Disabled | Yes

This cop checks for a line break before the first parameter in a
multi-line method parameter definition.

### Example

```ruby
# bad
def method(foo, bar,
    baz)
  do_something
end

# good
def method(
    foo, bar,
    baz)
  do_something
end

# ignored
def method foo,
    bar
  do_something
end
```

## Layout/FirstParameterIndentation

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks the indentation of the first parameter in a method call.
Parameters after the first one are checked by Style/AlignParameters, not
by this cop.

### Example

```ruby
# bad
some_method(
first_param,
second_param)

# good
some_method(
  first_param,
second_param)
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `special_for_inner_method_call_in_parentheses` | `consistent`, `special_for_inner_method_call`, `special_for_inner_method_call_in_parentheses`
IndentationWidth | `<none>` | Integer

## Layout/IndentArray

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks the indentation of the first element in an array literal
where the opening bracket and the first element are on separate lines.
The other elements' indentations are handled by the AlignArray cop.

By default, array literals that are arguments in a method call with
parentheses, and where the opening square bracket of the array is on the
same line as the opening parenthesis of the method call, shall have
their first element indented one step (two spaces) more than the
position inside the opening parenthesis.

Other array literals shall have their first element indented one step
more than the start of the line where the opening square bracket is.

This default style is called 'special_inside_parentheses'. Alternative
styles are 'consistent' and 'align_brackets'. Here are examples:

### Example

```ruby
# The `special_inside_parentheses` style enforces that the first
# element in an array literal where the opening bracket and first
# element are on seprate lines is indented one step (two spaces) more
# than the position inside the opening parenthesis.

#bad
array = [
  :value
]
and_in_a_method_call([
  :no_difference
                     ])

#good
array = [
  :value
]
but_in_a_method_call([
                       :its_like_this
                     ])
```
```ruby
# The `consistent` style enforces that the first element in an array
# literal where the opening bracket and the first element are on
# seprate lines is indented the same as an array literal which is not
# defined inside a method call.

#bad
# consistent
array = [
  :value
]
but_in_a_method_call([
                       :its_like_this
])

#good
array = [
  :value
]
and_in_a_method_call([
  :no_difference
])
```
```ruby
# The `align_brackets` style enforces that the opening and closing
# brackets are indented to the same position.

#bad
# align_brackets
and_now_for_something = [
                          :completely_different
]

#good
# align_brackets
and_now_for_something = [
                          :completely_different
                        ]
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `special_inside_parentheses` | `special_inside_parentheses`, `consistent`, `align_brackets`
IndentationWidth | `<none>` | Integer

## Layout/IndentAssignment

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks the indentation of the first line of the
right-hand-side of a multi-line assignment.

The indentation of the remaining lines can be corrected with
other cops such as `IndentationConsistency` and `EndAlignment`.

### Example

```ruby
# bad
value =
if foo
  'bar'
end

# good
value =
  if foo
    'bar'
  end
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
IndentationWidth | `<none>` | Integer

## Layout/IndentHash

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks the indentation of the first key in a hash literal
where the opening brace and the first key are on separate lines. The
other keys' indentations are handled by the AlignHash cop.

By default, Hash literals that are arguments in a method call with
parentheses, and where the opening curly brace of the hash is on the
same line as the opening parenthesis of the method call, shall have
their first key indented one step (two spaces) more than the position
inside the opening parenthesis.

Other hash literals shall have their first key indented one step more
than the start of the line where the opening curly brace is.

This default style is called 'special_inside_parentheses'. Alternative
styles are 'consistent' and 'align_braces'. Here are examples:

    # special_inside_parentheses
    hash = {
      key: :value
    }
    but_in_a_method_call({
                           its_like: :this
                         })
    # consistent
    hash = {
      key: :value
    }
    and_in_a_method_call({
      no: :difference
    })
    # align_braces
    and_now_for_something = {
                              completely: :different
                            }

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `special_inside_parentheses` | `special_inside_parentheses`, `consistent`, `align_braces`
IndentationWidth | `<none>` | Integer

## Layout/IndentHeredoc

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks the indentation of the here document bodies. The bodies
are indented one step.
In Ruby 2.3 or newer, squiggly heredocs (`<<~`) should be used. If you
use the older rubies, you should introduce some library to your project
(e.g. ActiveSupport, Powerpack or Unindent).
Note: When `Metrics/LineLength`'s `AllowHeredoc` is false(not default),
      this cop does not add any offenses for long here documents to
      avoid `Metrics/LineLength`'s offenses.

### Example

```ruby
# bad
<<-RUBY
something
RUBY

# good
# When EnforcedStyle is squiggly, bad code is auto-corrected to the
# following code.
<<~RUBY
  something
RUBY

# good
# When EnforcedStyle is active_support, bad code is auto-corrected to
# the following code.
<<-RUBY.strip_heredoc
  something
RUBY
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `auto_detection` | `auto_detection`, `squiggly`, `active_support`, `powerpack`, `unindent`

### References

* [https://github.com/bbatsov/ruby-style-guide#squiggly-heredocs](https://github.com/bbatsov/ruby-style-guide#squiggly-heredocs)

## Layout/IndentationConsistency

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks for inconsistent indentation.

### Example

```ruby
class A
  def test
    puts 'hello'
     puts 'world'
  end
end
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `normal` | `normal`, `rails`

### References

* [https://github.com/bbatsov/ruby-style-guide#spaces-indentation](https://github.com/bbatsov/ruby-style-guide#spaces-indentation)

## Layout/IndentationWidth

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks for indentation that doesn't use the specified number
of spaces.

See also the IndentationConsistency cop which is the companion to this
one.

### Example

```ruby
# bad
class A
 def test
  puts 'hello'
 end
end

# good
class A
  def test
    puts 'hello'
  end
end
```
```ruby
# bad
module A
class B
  def test
  puts 'hello'
  end
end
end

# good
module A
class B
  def test
    puts 'hello'
  end
end
end
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
Width | `2` | Integer
IgnoredPatterns | `[]` | Array

### References

* [https://github.com/bbatsov/ruby-style-guide#spaces-indentation](https://github.com/bbatsov/ruby-style-guide#spaces-indentation)

## Layout/InitialIndentation

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cops checks for indentation of the first non-blank non-comment
line in a file.

## Layout/LeadingCommentSpace

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks whether comments have a leading space after the
`#` denoting the start of the comment. The leading space is not
required for some RDoc special syntax, like `#++`, `#--`,
`#:nodoc`, `=begin`- and `=end` comments, "shebang" directives,
or rackup options.

### Example

```ruby
# bad
#Some comment

# good
# Some comment
```

### References

* [https://github.com/bbatsov/ruby-style-guide#hash-space](https://github.com/bbatsov/ruby-style-guide#hash-space)

## Layout/MultilineArrayBraceLayout

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks that the closing brace in an array literal is either
on the same line as the last array element, or a new line.

When using the `symmetrical` (default) style:

If an array's opening brace is on the same line as the first element
of the array, then the closing brace should be on the same line as
the last element of the array.

If an array's opening brace is on the line above the first element
of the array, then the closing brace should be on the line below
the last element of the array.

When using the `new_line` style:

The closing brace of a multi-line array literal must be on the line
after the last element of the array.

When using the `same_line` style:

The closing brace of a multi-line array literal must be on the same
line as the last element of the array.

### Example

```ruby
# bad
[ :a,
  :b
]

# bad
[
  :a,
  :b ]

# good
[ :a,
  :b ]

# good
[
  :a,
  :b
]
```
```ruby
# bad
[
  :a,
  :b ]

# bad
[ :a,
  :b ]

# good
[ :a,
  :b
]

# good
[
  :a,
  :b
]
```
```ruby
# bad
[ :a,
  :b
]

# bad
[
  :a,
  :b
]

# good
[
  :a,
  :b ]

# good
[ :a,
  :b ]
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `symmetrical` | `symmetrical`, `new_line`, `same_line`

## Layout/MultilineAssignmentLayout

Enabled by default | Supports autocorrection
--- | ---
Disabled | Yes

This cop checks whether the multiline assignments have a newline
after the assignment operator.

### Example

```ruby
# bad
foo = if expression
  'bar'
end

# good
foo =
  if expression
    'bar'
  end

# good
foo =
  begin
    compute
  rescue => e
    nil
  end
```
```ruby
# good
foo = if expression
  'bar'
end
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `new_line` | `same_line`, `new_line`

### References

* [https://github.com/bbatsov/ruby-style-guide#indent-conditional-assignment](https://github.com/bbatsov/ruby-style-guide#indent-conditional-assignment)

## Layout/MultilineBlockLayout

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks whether the multiline do end blocks have a newline
after the start of the block. Additionally, it checks whether the block
arguments, if any, are on the same line as the start of the block.

### Example

```ruby
# bad
blah do |i| foo(i)
  bar(i)
end

# bad
blah do
  |i| foo(i)
  bar(i)
end

# good
blah do |i|
  foo(i)
  bar(i)
end

# bad
blah { |i| foo(i)
  bar(i)
}

# good
blah { |i|
  foo(i)
  bar(i)
}
```

## Layout/MultilineHashBraceLayout

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks that the closing brace in a hash literal is either
on the same line as the last hash element, or a new line.

When using the `symmetrical` (default) style:

If a hash's opening brace is on the same line as the first element
of the hash, then the closing brace should be on the same line as
the last element of the hash.

If a hash's opening brace is on the line above the first element
of the hash, then the closing brace should be on the line below
the last element of the hash.

When using the `new_line` style:

The closing brace of a multi-line hash literal must be on the line
after the last element of the hash.

When using the `same_line` style:

The closing brace of a multi-line hash literal must be on the same
line as the last element of the hash.

### Example

```ruby
# bad
{ a: 1,
  b: 2
}
# bad
{
  a: 1,
  b: 2 }

# good
{ a: 1,
  b: 2 }

# good
{
  a: 1,
  b: 2
}
```
```ruby
# bad
{
  a: 1,
  b: 2 }

# bad
{ a: 1,
  b: 2 }

# good
{ a: 1,
  b: 2
}

# good
{
  a: 1,
  b: 2
}
```
```ruby
# bad
{ a: 1,
  b: 2
}

# bad
{
  a: 1,
  b: 2
}

# good
{
  a: 1,
  b: 2 }

# good
{ a: 1,
  b: 2 }
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `symmetrical` | `symmetrical`, `new_line`, `same_line`

## Layout/MultilineMethodCallBraceLayout

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks that the closing brace in a method call is either
on the same line as the last method argument, or a new line.

When using the `symmetrical` (default) style:

If a method call's opening brace is on the same line as the first
argument of the call, then the closing brace should be on the same
line as the last argument of the call.

If an method call's opening brace is on the line above the first
argument of the call, then the closing brace should be on the line
below the last argument of the call.

When using the `new_line` style:

The closing brace of a multi-line method call must be on the line
after the last argument of the call.

When using the `same_line` style:

The closing brace of a multi-line method call must be on the same
line as the last argument of the call.

### Example

```ruby
# symmetrical: bad
# new_line: good
# same_line: bad
foo(a,
  b
)

# symmetrical: bad
# new_line: bad
# same_line: good
foo(
  a,
  b)

# symmetrical: good
# new_line: bad
# same_line: good
foo(a,
  b)

# symmetrical: good
# new_line: good
# same_line: bad
foo(
  a,
  b
)
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `symmetrical` | `symmetrical`, `new_line`, `same_line`

## Layout/MultilineMethodCallIndentation

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks the indentation of the method name part in method calls
that span more than one line.

### Example

```ruby
# bad
while myvariable
.b
  # do something
end

# good
while myvariable
      .b
  # do something
end

# good
Thing.a
     .b
     .c
```
```ruby
# good
while myvariable
  .b

  # do something
end
```
```ruby
# good
while myvariable
        .a
        .b

  # do something
end

# good
myvariable = Thing
               .a
               .b
               .c
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `aligned` | `aligned`, `indented`, `indented_relative_to_receiver`
IndentationWidth | `<none>` | Integer

## Layout/MultilineMethodDefinitionBraceLayout

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks that the closing brace in a method definition is either
on the same line as the last method parameter, or a new line.

When using the `symmetrical` (default) style:

If a method definition's opening brace is on the same line as the
first parameter of the definition, then the closing brace should be
on the same line as the last parameter of the definition.

If an method definition's opening brace is on the line above the first
parameter of the definition, then the closing brace should be on the
line below the last parameter of the definition.

When using the `new_line` style:

The closing brace of a multi-line method definition must be on the line
after the last parameter of the definition.

When using the `same_line` style:

The closing brace of a multi-line method definition must be on the same
line as the last parameter of the definition.

### Example

```ruby
# symmetrical: bad
# new_line: good
# same_line: bad
def foo(a,
  b
)
end

# symmetrical: bad
# new_line: bad
# same_line: good
def foo(
  a,
  b)
end

# symmetrical: good
# new_line: bad
# same_line: good
def foo(a,
  b)
end

# symmetrical: good
# new_line: good
# same_line: bad
def foo(
  a,
  b
)
end
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `symmetrical` | `symmetrical`, `new_line`, `same_line`

## Layout/MultilineOperationIndentation

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks the indentation of the right hand side operand in
binary operations that span more than one line.

### Example

```ruby
# bad
if a +
b
  something
end

# good
if a +
   b
  something
end
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `aligned` | `aligned`, `indented`
IndentationWidth | `<none>` | Integer

## Layout/RescueEnsureAlignment

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks whether the rescue and ensure keywords are aligned
properly.

### Example

```ruby
# bad
begin
  something
  rescue
  puts 'error'
end

# good
begin
  something
rescue
  puts 'error'
end
```

## Layout/SpaceAfterColon

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks for colon (:) not followed by some kind of space.
N.B. this cop does not handle spaces after a ternary operator, which are
instead handled by Layout/SpaceAroundOperators.

### Example

```ruby
# bad
def f(a:, b:2); {a:3}; end

# good
def f(a:, b: 2); {a: 3}; end
```

### References

* [https://github.com/bbatsov/ruby-style-guide#spaces-operators](https://github.com/bbatsov/ruby-style-guide#spaces-operators)

## Layout/SpaceAfterComma

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks for comma (,) not followed by some kind of space.

### Example

```ruby
# bad
[1,2]
{ foo:bar,}

# good
[1, 2]
{ foo:bar, }
```

### References

* [https://github.com/bbatsov/ruby-style-guide#spaces-operators](https://github.com/bbatsov/ruby-style-guide#spaces-operators)

## Layout/SpaceAfterMethodName

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks for space between a method name and a left parenthesis in defs.

### Example

```ruby
# bad
def func (x) end
def method= (y) end

# good
def func(x) end
def method=(y) end
```

### References

* [https://github.com/bbatsov/ruby-style-guide#parens-no-spaces](https://github.com/bbatsov/ruby-style-guide#parens-no-spaces)

## Layout/SpaceAfterNot

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks for space after `!`.

### Example

```ruby
# bad
! something

# good
!something
```

### References

* [https://github.com/bbatsov/ruby-style-guide#no-space-bang](https://github.com/bbatsov/ruby-style-guide#no-space-bang)

## Layout/SpaceAfterSemicolon

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks for semicolon (;) not followed by some kind of space.

### Example

```ruby
# bad
x = 1;y = 2

# good
x = 1; y = 2
```

### References

* [https://github.com/bbatsov/ruby-style-guide#spaces-operators](https://github.com/bbatsov/ruby-style-guide#spaces-operators)

## Layout/SpaceAroundBlockParameters

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks the spacing inside and after block parameters pipes.

### Example

```ruby
# bad
{}.each { | x,  y |puts x }
->( x,  y ) { puts x }

# good
{}.each { |x, y| puts x }
->(x, y) { puts x }
```
```ruby
# bad
{}.each { |x,  y| puts x }
->(x,  y) { puts x }

# good
{}.each { | x, y | puts x }
->( x, y ) { puts x }
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyleInsidePipes | `no_space` | `space`, `no_space`

## Layout/SpaceAroundEqualsInParameterDefault

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks that the equals signs in parameter default assignments
have or don't have surrounding space depending on configuration.

### Example

```ruby
# bad
def some_method(arg1=:default, arg2=nil, arg3=[])
  # do something...
end

# good
def some_method(arg1 = :default, arg2 = nil, arg3 = [])
  # do something...
end
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `space` | `space`, `no_space`

### References

* [https://github.com/bbatsov/ruby-style-guide#spaces-around-equals](https://github.com/bbatsov/ruby-style-guide#spaces-around-equals)

## Layout/SpaceAroundKeyword

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks the spacing around the keywords.

### Example

```ruby
# bad
something 'test'do|x|
end

while(something)
end

something = 123if test

# good
something 'test' do |x|
end

while (something)
end

something = 123 if test
```

## Layout/SpaceAroundOperators

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks that operators have space around them, except for **
which should not have surrounding space.

### Example

```ruby
# bad
total = 3*4
"apple"+"juice"
my_number = 38/4
a ** b

# good
total = 3 * 4
"apple" + "juice"
my_number = 38 / 4
a**b
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
AllowForAlignment | `true` | Boolean

### References

* [https://github.com/bbatsov/ruby-style-guide#spaces-operators](https://github.com/bbatsov/ruby-style-guide#spaces-operators)

## Layout/SpaceBeforeBlockBraces

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks that block braces have or don't have a space before the opening
brace depending on configuration.

### Example

```ruby
# bad
foo.map{ |a|
  a.bar.to_s
}

# good
foo.map { |a|
  a.bar.to_s
}
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `space` | `space`, `no_space`
EnforcedStyleForEmptyBraces | `no_space` | `space`, `no_space`

## Layout/SpaceBeforeComma

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks for comma (,) preceded by space.

### Example

```ruby
# bad
[1 , 2 , 3]
a(1 , 2)
each { |a , b| }

# good
[1, 2, 3]
a(1, 2)
each { |a, b| }
```

## Layout/SpaceBeforeComment

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks for missing space between a token and a comment on the
same line.

### Example

```ruby
# bad
1 + 1# this operation does ...

# good
1 + 1 # this operation does ...
```

## Layout/SpaceBeforeFirstArg

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks that exactly one space is used between a method name and the
first argument for method calls without parentheses.

Alternatively, extra spaces can be added to align the argument with
something on a preceding or following line, if the AllowForAlignment
config parameter is true.

### Example

```ruby
# bad
something  x
something   y, z
something'hello'

# good
something x
something y, z
something 'hello'
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
AllowForAlignment | `true` | Boolean

## Layout/SpaceBeforeSemicolon

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks for semicolon (;) preceded by space.

### Example

```ruby
# bad
x = 1 ; y = 2

# good
x = 1; y = 2
```

## Layout/SpaceInLambdaLiteral

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks for spaces between -> and opening parameter
brace in lambda literals.

### Example

```ruby
# bad
a = -> (x, y) { x + y }

# good
a = ->(x, y) { x + y }
```
```ruby
# bad
a = ->(x, y) { x + y }

# good
a = -> (x, y) { x + y }
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `require_no_space` | `require_no_space`, `require_space`

## Layout/SpaceInsideArrayPercentLiteral

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks for unnecessary additional spaces inside array percent literals
(i.e. %i/%w).

### Example

```ruby
# bad
%w(foo  bar  baz)
# good
%i(foo bar baz)
```

## Layout/SpaceInsideBlockBraces

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks that block braces have or don't have surrounding space inside
them on configuration. For blocks taking parameters, it checks that the
left brace has or doesn't have trailing space depending on
configuration.

### Example

```ruby
# The `space` style enforces that block braces have
# surrounding space.

# bad
some_array.each {puts e}

# good
some_array.each { puts e }
```
```ruby
# The `no_space` style enforces that block braces don't
# have surrounding space.

# bad
some_array.each { puts e }

# good
some_array.each {puts e}
```
```ruby
# The `no_space` EnforcedStyleForEmptyBraces style enforces that
# block braces don't have a space in between when empty.

# bad
some_array.each {   }
some_array.each {  }
some_array.each { }

# good
some_array.each {}
```
```ruby
# The `space` EnforcedStyleForEmptyBraces style enforces that
# block braces have at least a spece in between when empty.

# bad
some_array.each {}

# good
some_array.each { }
some_array.each {  }
some_array.each {   }
```
```ruby
# The SpaceBeforeBlockParameters style set to `true` enforces that
# there is a space between `{` and `|`. Overrides `EnforcedStyle`
# if there is a conflict.

# bad
[1, 2, 3].each {|n| n * 2 }

# good
[1, 2, 3].each { |n| n * 2 }
```
```ruby
# The SpaceBeforeBlockParameters style set to `false` enforces that
# there is no space between `{` and `|`. Overrides `EnforcedStyle`
# if there is a conflict.

# bad
[1, 2, 3].each { |n| n * 2 }

# good
[1, 2, 3].each {|n| n * 2 }
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `space` | `space`, `no_space`
EnforcedStyleForEmptyBraces | `no_space` | `space`, `no_space`
SpaceBeforeBlockParameters | `true` | Boolean

## Layout/SpaceInsideBrackets

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks for spaces inside square brackets.

### Example

```ruby
# bad
array = [ 1, 2, 3 ]

# good
array = [1, 2, 3]
```

### References

* [https://github.com/bbatsov/ruby-style-guide#spaces-braces](https://github.com/bbatsov/ruby-style-guide#spaces-braces)

## Layout/SpaceInsideHashLiteralBraces

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks that braces used for hash literals have or don't have
surrounding space depending on configuration.

### Example

```ruby
# The `space` style enforces that hash literals have
# surrounding space.

# bad
h = {a: 1, b: 2}

# good
h = { a: 1, b: 2 }
```
```ruby
# The `no_space` style enforces that hash literals have
# no surrounding space.

# bad
h = { a: 1, b: 2 }

# good
h = {a: 1, b: 2}
```
```ruby
# The `compact` style normally requires a space inside
# hash braces, with the exception that successive left
# braces or right braces are collapsed together in nested hashes.

# bad
h = { a: { b: 2 } }

# good
h = { a: { b: 2 }}
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `space` | `space`, `no_space`, `compact`
EnforcedStyleForEmptyBraces | `no_space` | `space`, `no_space`

### References

* [https://github.com/bbatsov/ruby-style-guide#spaces-operators](https://github.com/bbatsov/ruby-style-guide#spaces-operators)

## Layout/SpaceInsideParens

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks for spaces inside ordinary round parentheses.

### Example

```ruby
# bad
f( 3)
g = (a + 3 )

# good
f(3)
g = (a + 3)
```

### References

* [https://github.com/bbatsov/ruby-style-guide#spaces-braces](https://github.com/bbatsov/ruby-style-guide#spaces-braces)

## Layout/SpaceInsidePercentLiteralDelimiters

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks for unnecessary additional spaces inside the delimiters of
%i/%w/%x literals.

### Example

```ruby
# good
%i(foo bar baz)

# bad
%w( foo bar baz )

# bad
%x(  ls -l )
```

## Layout/SpaceInsideRangeLiteral

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

Checks for spaces inside range literals.

### Example

```ruby
# bad
1 .. 3

# good
1..3

# bad
'a' .. 'z'

# good
'a'..'z'
```

### References

* [https://github.com/bbatsov/ruby-style-guide#no-space-inside-range-literals](https://github.com/bbatsov/ruby-style-guide#no-space-inside-range-literals)

## Layout/SpaceInsideStringInterpolation

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks for whitespace within string interpolations.

### Example

```ruby
# bad
   var = "This is the #{ space } example"

# good
   var = "This is the #{no_space} example"
```
```ruby
# bad
   var = "This is the #{no_space} example"

# good
   var = "This is the #{ space } example"
```

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `no_space` | `space`, `no_space`

### References

* [https://github.com/bbatsov/ruby-style-guide#string-interpolation](https://github.com/bbatsov/ruby-style-guide#string-interpolation)

## Layout/Tab

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop checks for tabs inside the source code.

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
IndentationWidth | `<none>` | Integer

### References

* [https://github.com/bbatsov/ruby-style-guide#spaces-indentation](https://github.com/bbatsov/ruby-style-guide#spaces-indentation)

## Layout/TrailingBlankLines

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop looks for trailing blank lines and a final newline in the
source code.

### Configurable attributes

Name | Default value | Configurable values
--- | --- | ---
EnforcedStyle | `final_newline` | `final_newline`, `final_blank_line`

### References

* [https://github.com/bbatsov/ruby-style-guide#newline-eof](https://github.com/bbatsov/ruby-style-guide#newline-eof)

## Layout/TrailingWhitespace

Enabled by default | Supports autocorrection
--- | ---
Enabled | Yes

This cop looks for trailing whitespace in the source code.

### References

* [https://github.com/bbatsov/ruby-style-guide#no-trailing-whitespace](https://github.com/bbatsov/ruby-style-guide#no-trailing-whitespace)
