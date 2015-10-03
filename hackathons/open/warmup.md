# Warmup

Complete this warmup exercise to get an idea how to put all the different pieces
together to generate an end-to-end data analysis viz report.

<a name="top"/>
<div id="autonav"></div>

{% data src="../fcq/fcq.clean.json" %}
{% enddata %}

{% viz %}

{% title %}

What is the distribution of courses across colleges?

{% solution %}

var clean = _.filter(data, function(n){
    return n.PCT.D != ""
})

var map = _.map(clean, function(n){
  return {dept: n.CrsPBADept, gpa: n.AVG_GRD, professor: n.AvgInstructor, name: _.pluck(n.Instructors, "name")[0]}
})

groups =  _.groupBy(map, function(n){
  return n.name
})


function computeColor(d) {
    if (d == "APPM"){
        return "rgb(179, 28, 58)"
    }
    else {
        return "rgb(182, 184, 184)"
    }
}

viz =  _.map(groups, function(n){
    return {avgGpa: _.sum(n, function(course){
                return course.gpa
            })/n.length,
            avgRating: _.sum(n, function(course){
                return course.professor
            })/n.length,
            dept: n[0].dept,
            color: computeColor(n[0].dept),
            name: n[0].name }
})
console.log(viz)

var result = _.map(viz, function(d){
         // invoke the compiled template function on each viz data
         return template({d: d})
     })
return result.join('\n')

{% template %}

<circle cx="${d.avgRating*100}" 
        cy="${500-d.avgGpa*100}" 
        r = 2
        stroke="${d.color}" 
        stroke-width="3" 
        fill="${d.color}"
        style="opacity:0.4"
        />

{% endviz %}
