{% data src="../fcq/fcq.clean.json" %}
{% enddata %}
# Report

Use only Javascript and SVG to produce a data analysis / visualization report.

# Authors

This report is prepared by
* [Kari Santos](https://github.com/karisantos)
* [Heather Witte](https://github.com/hswitte)
* [Zachary Lamb](https://github.com/ZachLamb)
* [Fadhil Suhendi](https://github.com/fadhilfath)
* [Denis Kazakov](https://github.com/94kazakov)

<a name="top"/>
<div id="autonav"></div>

# Activity type vs GPA? 

Use the warmup exercise as the template to produce an answer here.

# Instructor grade vs GPA (different color for colleges)?

{% lodash %}
var clean = _.filter(data, function(n){
	return n.PCT.D != ""
})

var map = _.map(clean, function(n){
  return {dept: n.CrsPBADept, gpa: n.AVG_GRD, professor: n.AvgInstructor, name: _.pluck(n.Instructors, "name")[0]}
})

groups =  _.groupBy(map, function(n){
  return n.name
})

return _.map(groups, function(n){
	return {avgGpa: _.sum(n, function(course){
				return course.gpa
			})/n.length,
			avgRating: _.sum(n, function(course){
				return course.professor
			})/n.length,
			dept: n[0].dept,
			name: n[0].name }
})

{% endlodash %}

<table>
{% for n in result %}
    <tr>
        <td>{{n.name}}</td>
        <td>{{n.dept}}</td>
        <td>{{n.avgGpa}}</td>
        <td>{{n.avgRating}}</td>
    </tr>
{% endfor %}
</table>




# What are top hardest courses in college? 

Use the warmup exercise as the template to produce an answer here. Remove this
question if you work as a unit of two.
