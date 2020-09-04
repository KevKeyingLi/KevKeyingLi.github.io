# Mastering Web Developer Interview Code
## Intro
https://github.com/planetoftheweb/masteringcode

## Questions
### How do you use the data- attribute in HTML?
https://github.com/planetoftheweb/masteringcode/tree/EP023b

Data Attribute: The data attribute is a powerful way of adding meaning to your HTML tags without disrupting the structure of your HTML.
* data-: you prefix your custom name with the key word data as well as a dash, so you can create your own pieces of data within an HTML tag
* accessible in CSS: accessible through CSS using brackets once it's in the HTML
    - attr(data-\*): to use the data-\* value for css
    - [data-\*='blabla']: as selector
* accessible in JS using dataset: the value in these data attributes can also be accessed through JavaScript using a special parameter called data set, and then the name of the attribute using dot notation.
    - element.dataset will contain all the data-attributes
    - if you're using more than one dash in the name, then you camel case the name, just like you would with any other CSS style. data-aaa-bbb will become item.dataset.aaaBbb

### Are you comfortable using jQuery?
#### What is jQuery
* JS library
* more compatible x-browsers
* new feature support

#### Popular Features
* DOM management
    - javascript provides querySelector, querySelectorAll. Modelled after jQuery
    - 
    - jQuery provides more functionalities for access/modify DOM
* AJAX
    - fetch api
    - promises
* chaining: chaining methods, so that the result of one action will be accessible and passed along to the next sequence of events. Now learning to chain is essential to mastering jQuery.

https://github.com/planetoftheweb/masteringcode/tree/EP029b

$(function(){}) to define IIFE, 
$('selector') to select
$('selector').on('click', function(){}) for event handling: same as addEventHandler
$.ajax({
    method: '',
    url: '',
    dataType: 'json'//optional
})

$.ajax({...}).done(function(data){
    //...
})
chaining

$.each(array, function(key, val) {
    ...
})


JQuery could have a lot of names for the same thing. 
## Tasks

## Interviews with Working Professionals
