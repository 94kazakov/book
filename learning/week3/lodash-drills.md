# Lodash Drills

Complete the following Lodash exercises. The goal is to become really good at
functional programming paradigm (e.g., `_.map`, `_.filter`, `_.all`, `_.any` ...etc) and
a number of really useful Lodash methods (e.g., `_.find`, `_.pluck` ... etc).

* enter your solution in the `solution` block
* utilize lodash functions as much as possible
* no `for/while` loop is allowed

Familiarity with programming in this way will not only make you a super productive
programmer but also will pave the way for you to learn MapReduce and MongoDB.

# Examples

{% lodashexercise %}

{% title %}

How many people?

{% data %}

[{name: 'John'}, {name: 'Mary'}, {name: 'Joe'}, {name: 'Ben'}]

{% output %}

4

{% solution %}

return data.length

{% endlodashexercise %}


{% lodashexercise %}

{% title %}

What are the names?

{% data %}

[{name: 'John'}, {name: 'Mary'}, {name: 'Joe'}, {name: 'Ben'}]

{% output %}

['John', 'Mary','Joe','Ben']

{% solution %}

return _.map(data, function(d){
    return d.name
})

{% endlodashexercise %}

# Exercises

{% lodashexercise %}

{% title %}

What names begin with the letter J?

{% data %}

[{name: 'John'}, {name: 'Mary'}, {name: 'Joe'}, {name: 'Ben'}]

{% output %}

['John','Joe']

{% solution %}
names = _.pluck(data, "name")
var result = _.filter(names, function(n){
  if (n[0] == "J"){
    return n
  }
})
return result

{% endlodashexercise %}



{% lodashexercise %}

{% title %}

How many Johns?

{% data %}

[{name: 'John'}, {name: 'John'}, {name: 'John'}, {name: 'Ben'}]

{% output %}

3

{% solution %}
var result = _.pluck(_.filter(data, {name: "John"}), "name")
return result.length

{% endlodashexercise %}




{% lodashexercise %}

{% title %}

What are all the first names?

{% data %}

[{name: 'John Smith'}, {name: 'Mary Kay'}, {name: 'Peter Pan'}, {name: 'Ben Franklin'}]

{% output %}

["John","Mary","Peter","Ben"]

{% solution %}
return _.map(data, function(n){
  return n.name.split(" ")[0]
})
{% endlodashexercise %}







{% lodashexercise %}

{% title %}

What are the first names of Smith?

{% data %}

[{name: 'John Smith'}, {name: 'Mary Smith'}, {name: 'Peter Pan'}, {name: 'Ben Smith'}]

{% output %}

["John","Mary","Ben"]

{% solution %}
var names = _.pluck(data, "name")
var smiths = _.filter(names, function(n){
  return n.indexOf("Smith") > -1
})
return _.map(smiths, function(n){
  return n.split(" ")[0]
})
{% endlodashexercise %}







{% lodashexercise %}

{% title %}

Change the format to lastname, firstname

{% data %}

[{name: 'John Smith'}, {name: 'Mary Kay'}, {name: 'Peter Pan'}]

{% output %}

[{name: 'Smith, John'}, {name: 'Kay, Mary'}, {name: 'Pan, Peter'}]

{% solution %}
var names = _.pluck(data, "name")
var result = _.map(names, function(n){
  var name = n.split(' ')[0]
  var lastName = n.split(' ')[1]
  return {name: lastName + ", " + name}
});
return result
{% endlodashexercise %}



{% lodashexercise %}

{% title %}

How many women?

{% data %}

[{name: 'John Smith', gender: 'm'}, {name: 'Mary Smith', gender: 'f'}, {name: 'Peter Pan', gender: 'm'}, {name: 'Ben Smith', gender: 'm'}]

{% output %}

1

{% solution %}

var names = _.pluck(data, "gender")
var smiths = _.filter(names, function(n){
  return n == "f"
})
return smiths.length
{% endlodashexercise %}







{% lodashexercise %}

{% title %}

How many men whose last name is Smith?

{% data %}

[{name: 'John Smith', gender: 'm'}, {name: 'Mary Smith', gender: 'f'}, {name: 'Peter Pan', gender: 'm'}, {name: 'Ben Smith', gender: 'm'}]

{% output %}

2

{% solution %}
var smiths = _.filter(data, function(n){
  return (n.gender == "m" && n.name.indexOf("Smith") > -1)
})
return smiths.length

{% endlodashexercise %}







{% lodashexercise %}

Are there more men than women?

{% data %}

[{name: 'John Smith', gender: 'm'}, {name: 'Mary Smith', gender: 'f'}, {name: 'Peter Pan', gender: 'm'}, {name: 'Ben Smith', gender: 'm'}]

{% output %}

true

{% solution %}
var women = _.filter(data, function(n){
  return n.gender == "f"
})

var men = _.filter(data, function(n){
  return n.gender == "m"
})

return men.length > women.length
{% endlodashexercise %}







{% lodashexercise %}

{% title %}

What is Peter Pan's gender?

{% data %}

[{name: 'John Smith', gender: 'm'}, {name: 'Mary Smith', gender: 'f'}, {name: 'Peter Pan', gender: 'm'}, {name: 'Ben Smith', gender: 'm'}]

{% output %}

'm'

{% solution %}

var peter = _.filter(data, function(n){
  return n.name == "Peter Pan"
})
return peter[0].gender
{% endlodashexercise %}





{% lodashexercise %}

{% title %}

What is the oldest age?

{% data %}

[{name: 'John Smith', age: 54}, {name: 'Mary Smith', age: 42}, {name: 'Peter Pan', age: 15}, {name: 'Ben Smith', age: 35}]

{% output %}

54

{% solution %}
var result = _.sortBy(data, 'age')
return _.last(result).age
{% endlodashexercise %}






{% lodashexercise %}

{% title %}

Is it true everyone is younger than 60?

{% data %}

[{name: 'John Smith', age: 54}, {name: 'Mary Smith', age: 42}, {name: 'Peter Pan', age: 15}, {name: 'Ben Smith', age: 35}]

{% output %}

true

{% solution %}

// use _.all
var result = _.every(data, function(n){
  return n.age < 60
})
return result

{% endlodashexercise %}




{% lodashexercise %}

{% title %}

Is it true someone is not an adult (younger than 18)?

{% data %}

[{name: 'John Smith', age: 54}, {name: 'Mary Smith', age: 42}, {name: 'Peter Pan', age: 15}, {name: 'Ben Smith', age: 35}]

{% output %}

true

{% solution %}

// use _.some
var result = _.some(data, function(n){
  return n.age < 18
})
return result

{% endlodashexercise %}




{% lodashexercise %}

{% title %}

How many people whose favorites include food?

{% data %}

[{name: 'John Smith', age: 54, favorites: ['food', 'movies']},
 {name: 'Mary Smith', age: 42, favorites: ['food', 'travel']},
 {name: 'Peter Pan', age: 15, favorites: ['minecraft', 'pokemo']},
 {name: 'Ben Smith', age: 35, favorites: ['craft', 'food']}]

{% output %}

3

{% solution %}

var result = _.filter(data, function(n){
  return _.includes(n.favorites, 'food')
})
return result.length

{% endlodashexercise %}





{% lodashexercise %}

{% title %}

Who are over 40 and love travel?

{% data %}

[{name: 'John Smith', age: 54, favorites: ['food', 'movies']},
 {name: 'Mary Smith', age: 42, favorites: ['food', 'travel']},
 {name: 'Peter Pan', age: 15, favorites: ['minecraft', 'pokemo']},
 {name: 'Joe Johnson', age: 46, favorites: ['travel', 'movies']},
 {name: 'Ben Smith', age: 35, favorites: ['craft', 'food']}]

{% output %}

['Mary Smith', 'Joe Johnson']

{% solution %}
result = _.filter(
              _.map(data, function(n){
                if ((n.age > 40) && (_.includes(n.favorites, 'travel'))) {
                  return n.name
                }
              }),
              function(n){
                return n != null
              }
              )
return result

{% endlodashexercise %}




{% lodashexercise %}

{% title %}

Who is the oldest person loving food?

{% data %}

[{name: 'John Smith', age: 54, favorites: ['food', 'movies']},
 {name: 'Mary Smith', age: 42, favorites: ['food', 'travel']},
 {name: 'Peter Pan', age: 15, favorites: ['minecraft', 'pokemo']},
 {name: 'Joe Johnson', age: 46, favorites: ['travel', 'movies']},
 {name: 'Ben Smith', age: 35, favorites: ['craft', 'food']}]

{% output %}

'John Smith'

{% solution %}
loveFood = _.filter(data, function(n){
  if (_.includes(n.favorites, "food")){
    return n
  }
})
var result = _.sortBy(loveFood, 'age')
return result[result.length - 1].name

{% endlodashexercise %}



{% lodashexercise %}

{% title %}

What are all the unique favorites?

{% data %}

[{name: 'John Smith', age: 54, favorites: ['food', 'movies']},
 {name: 'Mary Smith', age: 42, favorites: ['food', 'travel']},
 {name: 'Peter Pan', age: 15, favorites: ['minecraft', 'pokemo']},
 {name: 'Joe Johnson', age: 46, favorites: ['travel', 'movies']},
 {name: 'Ben Smith', age: 35, favorites: ['craft', 'food']}]

{% output %}

[
  "food",
  "movies",
  "travel",
  "minecraft",
  "pokemo",
  "craft"
]

{% solution %}

// hint: use _.pluck, _.uniq, _.flatten in some order
var favs = _.flatten(_.pluck(data, "favorites"))
return _.uniq(favs)

{% endlodashexercise %}



{% lodashexercise %}

{% title %}

What are all the unique last names?

{% data %}

[{name: 'John Smith', age: 54, favorites: ['food', 'movies']},
 {name: 'Mary Smith', age: 42, favorites: ['food', 'travel']},
 {name: 'Peter Pan', age: 15, favorites: ['minecraft', 'pokemo']},
 {name: 'Joe Johnson', age: 46, favorites: ['travel', 'movies']},
 {name: 'Ben Smith', age: 35, favorites: ['craft', 'food']}]

{% output %}

[
  "Smith",
  "Pan",
  "Johnson"
]

{% solution %}

var result = _.map(data, function(n){
  return n.name.split(" ")[1]
})
return _.uniq(result)

{% endlodashexercise %}