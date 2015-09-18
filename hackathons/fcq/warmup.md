{% data src="fcq.clean.json" %}
{% enddata %}

# Warmup

Next, complete the following warmup exercises as a team.

## How many unique subject codes?

{% lodash %}
return _.uniq(_.pluck(data, "Subject")).length
{% endlodash %}

They are {{ result }} unique subject codes.

## How many computer science (CSCI) courses?

{% lodash %}
cs = _.filter(data, function(n){
    return n.Subject == "CSCI"
})
return cs.length
{% endlodash %}

They are {{ result }} computer science courses.

## What is the distribution of the courses across subject codes?

{% lodash %}
// TODO: replace with code that computes the actual result
// {"HIST": 78,"HONR": 20,"HUMN": 17,"IAFS": 20,"IPHY": 134}
subjects =  _.groupBy(data, function(n){
    return n.Subject
})

return _.mapValues(subjects, function(n){
  return n.length  
})

{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What subset of these subject codes have more than 100 courses?

{% lodash %}
// TODO: replace with code that computes the actual result
var grps = _.groupBy(data, 'Subject')
var ret = _.pick(_.mapValues(grps, function(d){
    return d.length
}), function(x){
    return x > 100
})

subjects =  _.groupBy(data, "Subject")
map =  _.mapValues(subjects, function(n){
  return n.length  
})
return _.pick(map, function(n){
    return n > 100
})
{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What subset of these subject codes have more than 5000 total enrollments?

{% lodash %}
//return {"IPHY": 5507,"MATH": 8725,"PHIL": 5672,"PHYS": 8099,"PSCI": 5491}
groups = _.groupBy(data, "Subject")
map = _.mapValues(groups, function(n){
  return _.sum(_.pluck(n, "N.ENROLL" )) 
})
return _.pick(map, function(n){
    return n > 5000
})
{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What are the course numbers of the courses Tom (PEI HSIU) Yeh taught?

{% lodash %}
//return ['4830','4830']
var groups = _.groupBy(data, function(n){
    return _.includes(_.pluck(n.Instructors, "name"), "YEH, PEI HSIU")
})

map =  _.mapValues(groups, function(n){
  return n.length 
})

return map
//return _.pluck(groups.true, "CourseTitle")
{% endlodash %}

They are {{result | json}}.
