<template>
  <div class="main-frame">
    <SideBar @selected-side-nav="handleSideNav" />
    <Content :contentSection="selectedSideNav" />
  </div>
</template>

<script>
export default (await import('vue')).defineComponent({
  data() {
    return {
      selectedSideNav: `Today's Tasks`
    };
  },
  methods: {
    handleSideNav(section) {
      this.selectedSideNav = section;
    }
  }
});
</script>

<style>
.main-frame {
  display: flex;
  justify-content: center;
  top: 50%;
  width: calc(100% - 80px);
  height: calc(100% - 40px);
  border: 5px solid #cce8e7;
  border-radius: 20px;
}
@media screen and (max-width: 1100px) {
  .main-frame {
    display: flex;
    justify-content: center;
    top: 50%;
    border: 5px solid #cce8e7;
    border-radius: 20px;
  }
}
</style>
