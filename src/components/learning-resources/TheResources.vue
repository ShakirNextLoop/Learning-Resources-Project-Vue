<template>
  <base-card>
    <base-button @click="setTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
    <base-button @click="setTab('add-resource')" :mode="addResButtonMode">Add Resources</base-button>
  </base-card>

  <component :is="selectedTab"></component>
</template>

<script>
import StoredResources from './StoredResources.vue'
import AddResource from './AddResource.vue'

export default {
    components:{
        StoredResources,
        AddResource
    },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources :[
                {
                    id: "official",
                    title: "Official Guide",
                    description: "The official guide Vue js",
                    link: "https://vuejs.org"
                },
                {
                    id: "google",
                    title: "Google",
                    description: "Google Search",
                    link: "https://google.com"
                }
            ]
    };
  },
  computed:{
      storedResButtonMode(){
          return this.selectedTab=='stored-resources'?null:'flat'
      },
      addResButtonMode(){
          return this.selectedTab=='add-resource'?null:'flat'

      }
  },
  provide(){
      return {
          resources:this.storedResources,
          addResource:this.addResource
      }
  },
  methods: {
    setTab(tab) {
        this.selectedTab=tab
    },
    addResource(title,desc,link){
        const newRes={
            id:new Date().toISOString(),
            title:title,
            description:desc,
            link:link

        }
        this.storedResources.unshift(newRes)
        this.selectedTab="stored-resources"
    }
  },
};
</script>