<template>
  <div class="sidebar">
    <div class="sidenav-title">
      <div class="sidenav-title-icon">
        <Icon name="ic:outline-account-circle" size="4rem" />
      </div>
      <div class="sidenav-title-name">
        <h4>JUST DO IT</h4>
        <h3>Guest</h3>
      </div>
    </div>
    <div class="sidenav-item">
      <ul class="sidenav-item-wrapper">
        <div
          @click="toggleCollapsed(todayTasks), selectSideNav(todayTasks)"
          class="sidenav-item-title"
        >
          <Icon name="ic:baseline-edit-note" size="1.5rem" />
          <h4>Today's tasks</h4>
          <Icon
            :name="
              collapsed === todayTasks
                ? 'ic:outline-keyboard-arrow-up'
                : 'ic:baseline-keyboard-arrow-down'
            "
            size="1.5rem"
          />
        </div>
        <div v-if="collapsed === todayTasks && sideNav === todayTasks" class="sidenav-item-list">
          <li>
            <Icon name="ic:baseline-circle" size="0.8rem" color="red" />
            <p>Work</p>
          </li>
          <li>
            <Icon name="ic:baseline-circle" size="0.8rem" color="green" />
            <p>Personal</p>
          </li>
          <li>
            <Icon name="ic:baseline-circle" size="0.8rem" color="blue" />
            <p>Comunity</p>
          </li>
        </div>
      </ul>
    </div>
    <div class="sidenav-item">
      <ul class="sidenav-item-wrapper">
        <div
          @click="
            toggleCollapsed(scheduledTasks), selectSideNav(scheduledTasks)
          "
          class="sidenav-item-title"
        >
          <Icon name="ic:baseline-assignment" size="1.5rem" />
          <h4>Scheduled tasks</h4>
          <Icon
            :name="
              collapsed === scheduledTasks
                ? 'ic:outline-keyboard-arrow-up'
                : 'ic:baseline-keyboard-arrow-down'
            "
            size="1.5rem"
          />
        </div>
        <div v-if="collapsed === scheduledTasks && sideNav === scheduledTasks" class="sidenav-item-list">
          <li>
            <Icon name="ic:baseline-circle" size="0.8rem" color="red" />
            <p>Work</p>
          </li>
          <li>
            <Icon name="ic:baseline-circle" size="0.8rem" color="green" />
            <p>Personal</p>
          </li>
          <li>
            <Icon name="ic:baseline-circle" size="0.8rem" color="blue" />
            <p>Comunity</p>
          </li>
        </div>
      </ul>
    </div>
    <div class="sidenav-item">
      <div @click="toggleCollapsed(settings), selectSideNav(settings)" class="sidenav-item-title">
        <Icon name="ic:baseline-settings" size="1.5rem" />
        <h4>Settings</h4>
      </div>
    </div>
  </div>
</template>

<script>
export default(await import('vue')).defineComponent({
  data() {
    return {
      collapsed: true,
      todayTasks: `Today's Tasks`,
      scheduledTasks: 'Scheduled Tasks',
      settings: 'Settings',
      sideNav: ''
    };
  },
  methods: {
    toggleCollapsed(section) {
      this.sideNav = section
      this.collapsed = this.collapsed === section ? null : section;
      console.log(this.sideNav);
    },
    selectSideNav(section) {
      this.$emit('selectedSideNav', section)
    }
  },
  emits: {
    selectedSideNav: null
  }
});
</script>

<style>
ul li {
  list-style: none;
  display: flex;
  flex-wrap: nowrap;
  align-items: center;
  gap: 10px;
  margin-left: 30px;
}
.sidebar {
  background-color: #cce8e7;
  color: #324b4b;
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.sidenav-title {
  margin-bottom: 50px;
  display: flex;
  flex-wrap: nowrap;
  align-items: center;
  gap: 5px;
}
.sidenav-title-name {
  display: flex;
  flex-direction: column;
  gap: 5px;
}
.sidenav-title-name h3 {
  color: rgb(0, 155, 155);
}
.sidenav-item {
  padding-left: 10px;
  display: flex;
  flex-wrap: nowrap;
}
.sidenav-item:first-child {
  align-self: self-start;
}
.sidenav-item-wrapper {
  padding-right: 5px;
  display: flex;
  flex: 1;
  flex-direction: column;
  gap: 10px;
}
.sidenav-item-title {
  display: flex;
  flex-wrap: nowrap;
  align-items: center;
  justify-content: space-between;
  gap: 7px;
}
.sidenav-item-title h4 {
  flex: 1;
}
.sidenav-item-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
</style>
