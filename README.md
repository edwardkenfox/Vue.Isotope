# Vue.Isotope
Vue directive for lists allowing [isotope](http://isotope.metafizzy.co/) layout filtering and sorting.


##Motivation

Create a directive that allows to use vue with isotope filter & sort magical layouts.
The underlying 

##Demo

![demo gif](https://raw.githubusercontent.com/David-Desmaisons/Vue.Isotope/master/example1.gif)

Basic:

https://jsfiddle.net/dede89/y6c8rpyu/

Complete:

https://jsfiddle.net/dede89/g6c0vzm2/

Isotope elements demo with vue template:

![demo gif](https://raw.githubusercontent.com/David-Desmaisons/Vue.Isotope/master/example2.gif)
https://jsfiddle.net/dede89/14nd6g0q/

##Features

* Full support of [Isotope](http://isotope.metafizzy.co/) options via options parameters
* Reactive directive that dislpays change in case in case of property impacting sorting or filtering
* Provides filter and sort based on ViewModel information

##API:
###Options
* All value are similar as isotope options expect for:
* id value: the unique name of the isotope component
* Filter definition:
  Implement filter by passing an option with a getFilterData object that exposes filter option. Vue.Isotope will call these 
  functions with the element to filter as parameter and this set as the underlying vm.
  
      		getFilterData:{
      			isEven: function(itemElem){
      				return itemElem.id % 2 === 0;
      			},
      			isOdd: function(itemElem){
      				return itemElem.id % 2 !== 0;
      			},
      			filterByText: function(itemElem){
        			return itemElem.name.toLowerCase().includes(this.filterText.toLowerCase());
        		}
        	}
        	
  
* Sort definition:
  Implement sort by passing as option a getSortData object that exposes filter option. Vue.Isotope will call these 
  functions with the element to filter as parameter and this set as the underlying vm. If a string is passed instead of a function, sorting
  will use the corresponding property.
  
  			getSortData: {
        		id: "id",
        		name: function(itemElem){
        			return itemElem.name.toLowerCase();     
        		}
        	}
        	
###Filtering and sorting:
  To filter or sort call isotopeSort or isotopeFilter on the VierwModel (Vue.Isotope will add this function to the ViewModel).
  These functions call two arguments: option and id. The first is the sorting or filtering key as defined in getSortData or 
  getFilterData respectivelly. The second is the id of the underlying isotope component defined as the "id" property of the
  option arguments. If only one isotope component is displayed this value can be omitted.
  
      this.isotopeFilter(key, id);
      
  Another useful method is isotopeShutle(id) to dispaly a random order.
  
      this.isotopeShuttle(id);
  
##Usage

Use it exactly as v-for directive, passing optional parameters using 'options' parameter.

  ``` html
  <div v-isotope="element in list1">
    <p>{{element.name}}</p>
  </div>
   ```

- #### For `<script>` Include

  Just include `vue.istope.js` after Vue and lodash(>=3).
  
## License
  
  [MIT](https://github.com/David-Desmaisons/Vue.isotope/blob/master/LICENSE)