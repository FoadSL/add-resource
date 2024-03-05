<template>
  <BaseCard>
    <BaseButton
      @click="setSelectedTab('StoredResources')"
      :mode="storedResourcesBtnMode"
      >Stored Resources</BaseButton
    >
    <BaseButton
      :mode="addResourceBtnMode"
      @click="setSelectedTab('AddResource')"
      >Add Resource</BaseButton
    >
  </BaseCard>
  <KeepAlive>
    <component :is="selectedTab"></component>
  </KeepAlive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  // props: ['resources'],
  components: {
    StoredResources,
    AddResource,
  },

  data() {
    return {
      selectedTab: 'StoredResources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official-Guide',
          description: 'The official Vue.js documentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://google.com',
        },
      ],
    };
  },
  computed: {
    storedResourcesBtnMode() {
      return this.selectedTab === 'StoredResources' ? 'null' : 'flat';
    },
    addResourceBtnMode() {
      return this.selectedTab === 'AddResource' ? 'null' : 'flat';
    },
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.deleteResource,
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, desc, link) {
      const newResource = {
        id: new Date().toISOString(),
        title,
        description: desc,
        link,
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = 'StoredResources';
    },
    deleteResource(resId) {
      const resIndex = this.storedResources.findIndex(
        (res) => res.id === resId
      );
      this.storedResources.splice(resIndex, 1);
    },
  },
};
</script>
