{% data src="fcq.clean.json" %}
{% enddata %}

# Report

As a class, we brainstormed and came up with a long list of further questions we
can ask based on the FCQ data. Out of these questions, our team chose to tackle on
the following questions. Each member on our team is reponsible for one question.


##Is there correlation between professor quality ratings to the grade distribution of the classes they teach?

##What major is most rewarding? (rew = (AVE4000> - AVE)/(some normalizer))

# Which classes(with specific professors) damaged the most students (sort by:D + DF + F + WDRAW rating)?
by (Denis Kazakov)

{% lodash %}
var clean = _.filter(data, function(n){
	return n.PCT.D != ""
})

var map = _.map(clean, function(n){
  return {course: n.CourseTitle, ratio: n.PCT.C + n.PCT.D + n.PCT.F, name: _.pluck(n.Instructors, "name")}
})

return _.sortBy(map, function(n){
  return n.ratio
}).reverse()
{% endlodash %}

<table>
{% for n in result %}
    <tr>
        <td>{{n.course}}</td>
        <td>{{n.ratio}}</td>
        <td>{{n.name}}</td>
    </tr>
{% endfor %}
</table>


# (Question 2) by (Name)

{% lodash %}
return "[answer]"
{% endlodash %}


# (Question 3) by (Name)

{% lodash %}
return "[answer]"
{% endlodash %}

# (Question 4) by (Name)

{% lodash %}
return "[answer]"
{% endlodash %}

# (Question 5) by (Name)

{% lodash %}
return "[answer]"
{% endlodash %}
