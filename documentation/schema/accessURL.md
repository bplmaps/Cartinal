---
---

<br>

[← Back to Schema Home](./)

# accessURL

<template>
    <div id = "container">
      <p class="larger-text">Direct access resource link</p>
      <p >Expected Type: <strong>String</strong></p>
    </div>
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
          peopleLifecycle: [],
        }
    },
    methods: {
        whatsUp(){
          console.log(this.citation)
        }
    },
    computed: {
        data() {
            return this.$page.frontmatter
        }
    },
    created() {
        //returns a promise
        axios.get("https://raw.githubusercontent.com/bplmaps/data-description-schema/master/schema.json")
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

## Example use

``` json
"accessURL": "https://s3.us-east-2.wasabisys.com/public-geospatial/dkhm2yy1r/endpoints/ToJoin2018.csv"
```

``` json
"accessURL": "https://github.com/nblmc/massachusetts-municipal-boundaries/blob/main/processor.ipynb"
```