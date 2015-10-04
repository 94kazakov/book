{% import '../../hackathons/classmates/data.html' as data %}

# Report

There are {{ data.comments.length }} students who gave a self-introduction. As a
class, we brainstormed and came up with a long list of further questions we can
ask based on this data. Our team chose to tackle on the following:

#Who is not a computer science major? 
{% lodash %}
var comments = _.pluck(data.comments, "body")
csComments = _.reject(comments, function(n){
	return ((_.includes(n.toLowerCase(), "computer science") || (_.includes(n.toLowerCase(), "cs"))))
});

return _.map(csComments, function(n){
	var parsed = n.split('\r\n')
	name = parsed[0].split(': ')[1]
	return name
});
{% endlodash %}
{{result}} are not computer science major. 

#How many people responded before the first day of class (August 24th)?
{% lodash %}
var dates = _.pluck(data.comments, "created_at")
var commitTimes = _.map(dates, function(n){
	var date = n.split('T')[0]
	return date.split('-')[2]
});

//object with counts
var mapOfDates = _.countBy(commitTimes, function(n){
	return n	
});
console.log(mapOfDates)

//count of how many responded before 24th
before = _.filter(commitTimes, function(n){
	return n<24
});
//return mapOfDates
return before.length
{% endlodash %}
{{result}} have responded before first class date.




#How many people are applied math major? Who are they? 	
{% lodash %}
var comments = _.pluck(data.comments, "body")
appmComments = _.filter(comments, function(n){
	return (_.includes(n.toLowerCase(), "applied math"))
});

return _.map(appmComments, function(n){
	var parsed = n.split('\r\n')
	name = parsed[0].split(': ')[1]
	return name
});
{% endlodash %}
We have {{result.length}} Applied Math students. {{result}} are Applied Math major. 


#Of people that responded on 24th, how many people responded after class began? 
{% lodash %}
var dates = _.pluck(data.comments, "created_at")
dateFilter = _.filter(dates, function(n){
	return _.includes(n, "2015-08-24")
})

var commitTimes = _.map(dateFilter, function(n){
	var date = n.split('T')[1]
	return date.split(':')[0]
});

timeFilter = _.filter(commitTimes, function(n){
	return n>16
});

return timeFilter
{% endlodash %}
{{result.length}} Responded after the class start time on 24th of August. 
