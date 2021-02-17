---
sidebar: auto
---

<br>

[← Back to temporal](./temporal.html)

# temporalRepresentation

## Definition

<template>
   <table v-if="this.filterTagging.temporal" id ="property-table">
     <p class="larger-text">{{this.filterTagging.temporal.properties.temporalRepresentation.description}}</p>
  <tr>
    <th>Property</th>
    <th>Expected Type</th>
    <th>Required</th>
    <th>Description</th>
  </tr>
  <tr v-for="item, index in this.filterTagging.temporal.properties.temporalRepresentation.properties" :key="index">
    <td>{{index}}</td>
    <td>{{item.type}}</td>
    <td></td>
    <td>{{item.description}}</td>
  </tr>
</table> 
</template>

<script>
import axios from 'axios'


export default {

    data() {
        return {
          schema: [],
          citation: [],
          endpoints: [],
          filterTagging: [],
          documentationHealth: [],
          relatedResources: [],
          peopleLifecycle: []
        }
    },
    methods: {
        whatsUp(){
          console.log(this.filterTagging)
        }
    },
    computed: {
        data() {
            return this.$page.frontmatter
        }
    },
    created() {
        //returns a promise
        axios.get("https://raw.githubusercontent.com/nblmc/Data-Context/master/schema.json")
            .then(response => {
                this.schema = response.data.properties
                this.citation = response.data.properties.citation.properties
                this.endpoints = response.data.properties.endpoints
                this.filterTagging = response.data.properties.filterTagging.properties
                this.documentationHealth = response.data.properties.documentationHealth.properties
                this.relatedResources = response.data.properties.relatedResources.properties
                this.peopleLifecycle = response.data.properties.peopleLifecycle.properties
            }).catch(err => {
                console.log(err)
            })
    }
}
</script>

<style lang="stylus">

table#property-table
  width:100%

p.larger-text
  font-size 120%

</style>

## Examples

### Singular Expression 

```json
"temporalRepresentation": {
	"encoding": "https://www.w3.org/TR/NOTE-datetime",
	"valueType": "singularExpression",
	"singleDate": "2020"
}
```


### Range 
```json
"temporalRepresentation": {
	"valueType": "temporalRange",
	"encoding": "https://www.w3.org/TR/NOTE-datetime",
	"rangeStart": "1630",
	"endRangeValue": "1995"
}
```