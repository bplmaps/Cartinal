---
---

<br>

[← Back to coreCitation](./coreCitation.html) 

# accessCondition

<template>
    <div v-if="this.coreCitation.accessCondition" id = "container">
      <p class="larger-text">{{this.coreCitation.accessCondition.description}}</p>
      <p >Expected Type: <strong>{{this.coreCitation.accessCondition.type}}</strong></p>
    </div>
</template>

<script>
import axios from 'axios'


export default {

    data() {
        return {
          schema: [],
          coreCitation: [],
          dataEndpoints: [],
          subjectTagging: [],
          dataBiography: [],
          resourceConstellation: [],
          dataLifecycle: [],
        }
    },
    methods: {
        whatsUp(){
          console.log(this.coreCitation)
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
                this.coreCitation = response.data.properties.coreCitation.properties
                this.dataEndpoints = response.data.properties.dataEndpoints
                this.subjectTagging = response.data.properties.subjectTagging.properties
                this.dataBiography = response.data.properties.dataBiography.properties
                this.resourceConstellation = response.data.properties.resourceConstellation.properties
                this.dataLifecycle = response.data.properties.dataLifecycle.properties
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

## Example 

``` json
"accessCondition": "This item is in the public domain. There are no restrictions on use."
```