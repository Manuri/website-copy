New concepts: Array query methods (+ chaining methods), instantiating a class, getter method or `attr_reader`.

### Minimal solution for approval

```ruby

class HighScores
  def initialize(scores)
    @scores = scores
  end

  def scores
    @scores
  end

  def personal_best
    scores.max
  end

  def latest
    scores.last
  end

  def personal_top
    scores.sort.reverse.take(3) 
  end

  def report
    difference = "#{personal_best - latest} short of" unless personal_best == latest

    "Your latest score was #{latest}. That's #{difference} your personal best!".squeeze(' ')
  end
end

```
### Reasonable variants
 - Using a getter method `scores`, not `attr_reader`: That's okay at this point in the track, no need to suggest `attr_reader`.
 - Variants in composing the string in `report`, as long as it's not a complicated if/else statement (see Talking Points).

### General notes
- The Instructions point to a beginner friendly explanation of instantiating a class: 
http://ruby-for-beginners.rubymonstas.org/writing_classes/initializers.html
and to the rubydocs Array. 
- Beginners create the attribute reader, but may call the instance variable instead of the getter. 
This link gives a nice introduction of getters and setters, and the naming convention in Ruby:
[launchschool: accessor_methods](https://launchschool.com/books/oo_ruby/read/classes_and_objects_part1#accessormethods).
It's recommended to link to this or your favorite explanation, instead of typing the solution for them.
- `sort.reverse` is not very performant, but at this point in the track it's more important that students explore the 
standard libraries (and work with method chaining) than that they know how to optimize.

### Talking points
- [`Array#max`](https://ruby-doc.org/core/Array.html#method-i-max) takes an argument; `scores.max(3)` works.
- Most submissions retrieve the `personal_top` values with the `Array#[]` method, which is harder to read than the convenience methods that Ruby offers: `Array#take(3)` or `Array#first(3)` win in readability. And `Array#max(3)` doesn't even need the sorting-and-reverting steps. 
- The `report` method asks for a conditionally composed string. It's meant to think about the trade-off 'duplication' vs 'readability'. Recommendation: approve any solution unless it's a supercomplicated if/else statement. 
- Consider `String#squeeze(' ')` to avoid hard-to-spot spacing with string interpolation. 

### Mentor Research
- [String](https://ruby-doc.org/core-2.5.3/String.html): `String#<< / String.concat` vs. `String#+`? 
Concatenation mutates the string instance in-place, `String#+` creates new string objects.
Ruby 2.3 will freeze string literals by default.

### Changelog
- Version 2 changed method names "highest" -> "personal_best", "top" -> "personal_top"
