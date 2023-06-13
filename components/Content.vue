<template>
  <div class="content">
    <div class="row">
      <h1 class="title">{{ contentSection }}</h1>
    </div>
    <div class="row">
      <ScheduledTasks v-if="contentSection === 'Scheduled Tasks'" />
      <SettingsContent v-else-if="contentSection === 'Settings'" />
      <TodayTasks v-else />
    </div>
  </div>
</template>

<script>
import ScheduledTasks from './ScheduledTasks.vue';
import SettingsContent from './SettingsContent.vue';
import TodayTasks from './TodayTasks.vue';

export default (await import('vue')).defineComponent({
    props: {
        contentSection: String
    },
    components: { ScheduledTasks, TodayTasks, SettingsContent }
});
</script>

<style>
.content {
  color: #cce8e7;
  font-size: 1rem;
  font-weight: 10;
  height: 100%;
  background-color: #324b4b;
  padding: 16px 16px;
  border-radius: 20px;
  display: flex;
  flex: 1;
  flex-direction: column;
}
.row:first-child {
  padding-bottom: 20px;
}
.row:last-child {
  display: flex;
  justify-content: space-around;
  flex-direction: column;
  flex: 10;
}
</style>
