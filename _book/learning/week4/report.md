{% data src="../../hackathons/fcq/fcq.clean.json" %}
{% enddata %}

# Report

As a team, answer all the questions the team's members submitted on our
[course forum](https://github.com/bigdatahci2015/forum/issues/14). Each
team member is responsible for one question. But everyone should work together
to come up with a good solution. Your answer should consist of Lodash code
and a brief writeup. Utilize `_.map`, `_.filter`, `_.group` ...etc. Do not
use any for loop.

It is important for everyone to understand all the solutions and make sure you
will be able to independently reproduce these solutions when asked to do so.
Coming up, we will incorporate variations of these questions into a future hackathon
 and you are expected to be capable of reproducing and adapting your solutions.

# What department has the lowest average GPA? by Nicole Woytarowicz

{% lodash %}
var subjects = _.groupBy(data, 'Subject')
var departments = _.pick(_.mapValues(subjects, function(d){
return (_.sum(_.pluck(d, "AVG_GRD")))/(d.length)
}), function(x){
return x > 0
})

var worst = _.min(departments)

return {Department: (_.invert(departments))[worst], Average_GPA: worst}
{% endlodash %}
{{result | json}}

# Which classes(with specific professors) damaged the most students (sort by:C + D + F rating)? by Denis Kazakov

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


# What department should I take classes in if I want to boost my GPA? by Caleb Hsu

{% lodash %}
var subjects = _.groupBy(data, 'Subject_Label')

var avgA = _.mapValues(subjects, function(s) {
return _.sum(_.pluck(s, 'PCT.A')) / s.length
})

var highest =  _.last(_.sortBy(_.pairs(avgA), function(d) {
return d[1]
}))

return highest[0]
{% endlodash %}

I should take classes in the {{result}} department if I want to boost my GPA.

# Which classes have the maximum Hours spent (16+) per week? by Parker Illig

{% lodash %}
var result = _.groupBy(data, function(d){
var dept = d.Subject
var num = d.Course
var combine = dept +  " " + num    
return combine
})
var classes = _.mapValues(result, function(d){
var wk = _.first(_.pluck(d, 'Workload.Hrs_Wk'))
return _.includes(wk, '16+')
})
return _.pick(classes, function(x){
return x==true
})
{% endlodash %}

Here's a table for the results
<table>
{% for key, value in result %}
<tr>
<td>{{key}}</td>
</tr>
{% endfor %}
</table>

What classes have very different workloads compared to credit hours? by John Cronk

{% lodash %}
return _.filter(data, function(course) {
    var thresh = 3
    return ((course.Workload.Raw - course.Hours > thresh) ||
    (course.Workload.Raw - course.Hours < -1*thresh) &&
    course.Workload.Raw > 0)
})
{% endlodash %}


<table>
{% for n in result %}
    <tr>
        <td>{{n.Subject}}</td>
        <td>{{n.Course}}</td>
        <td>{{n.Hours}}</td>
        <td>{{n.Workload.Raw}}</td>
    </tr>
{% endfor %}
</table>