# Analysis

{% import './data.html' as data %}

After completing the warmup exercises, your task is to do four more slightly
more challenges analyses.

## How many students like sushi as their favorite food?

{% lodash %}
var comments = _.pluck(data.comments, "body");
var sushiComments = _.filter(comments, function(n){
		return _.includes(n, "ushi")
	});
return sushiComments.length
{% endlodash %}

The answer is {{result}}.

## Who are the students liking Python the most?

{% lodash %}
var comments = _.pluck(data.comments, "body");
var pythonComments = _.filter(comments, function(n){
		return _.includes(n, "ython")
	});

names = _.map(pythonComments, function(n){
	var parsed = n.toLowerCase().split('\r\n')
	name = parsed[0].split(': ')[1]
	return name
});
return names
{% endlodash %}

Their names are {{result}}.

## Are there more Javascript lovers or Java lovers?

{% lodash %}
var comments = _.pluck(data.comments, "body");
var javaComments = _.filter(comments, function(n){
		return _.includes(n.toLowerCase(), "java")
	});
var javascript = _.filter(javaComments, function(n){
		return _.includes(n.toLowerCase(), "script")
	});
var java = _.reject(javaComments, function(n){
		return _.includes(n.toLowerCase(), "script")
	});

console.log(java.length)
console.log(javascript.length)
if (javascript.length > java.length){
	return "Javascript"
} else {
	return "Java"
}
{% endlodash %}

The answer is {{result}}.

## Who like the same food as `kjblakemore`?

{% lodash %}
var comments = _.pluck(data.comments, "body")
var foodName = _.filter(comments, function(n) {
	return _.includes(n.toLowerCase(), "kjblakemore")
});
console.log(foodName)
{% endlodash %}

Their names are {{result}}.
