<template>
    <div>
        <base-card>
            <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
            <base-button @click="setSelectedTab('add-resources')" :mode="addResButtonMode">Add Resources</base-button>
        </base-card>
<keep-alive>
        <component :is="selectedTab"></component>
        </keep-alive>
    </div>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResources from './AddResources.vue';

export default {
    components: {
        StoredResources,
        AddResources,
    },
    data() {
        return {
            selectedTab: 'StoredResources',
            storedResources: [
               { id: 'official-guide' , 
               title: 'The Official Guide for Vue.js' ,
                description: 'The official guide for Vue.js' ,
                 link: 'https://vuejs.org/v2/guide/'
                 },
    
               { id: 'google' , 
               title: 'Google' ,
                description: 'Google search engine' ,
                 link: 'https://www.google.com'
                 },
    
               { id: 'youtube' ,
                title: 'YouTube' ,
                 description: 'YouTube video sharing platform' ,
                  link: 'https://www.youtube.com'
                },
            ],
        };
    },
        provide() {
          return {
            resources: this.storedResources,
            addResource: this.addResource,
            deleteResource: this.removeResource
          };
        },
    computed:{
        storedResButtonMode(){
            return this.selectedTab ==='stored-resources'? null : 'flat';
            
        },
        addResButtonMode(){
            return this.selectedTab === 'add-resources'? null : 'flat';
        }
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab;
        },
        addResource(title,description,url) {  
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description:description,
                link: url,
            };
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        },
        removeResource(resourceId){
           const resIndex = this.storedResources.findIndex(res => res.id === resourceId);
           this.storedResources.splice(resIndex,1);
        },
    }
} 
</script>
