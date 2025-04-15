<script setup>
import { callScheduler } from '@/components'
import { ref, nextTick } from 'vue'

const sampleScheduleContactAndUserData = ref([{ 
  "title": "User 1",
  "fullname": "User 1",
  "id": "1",
  "schedule": [{
    "text": "",
    "start": "2025/04/15 09:15",
    "end": "2025/04/15 10:30",
    "data": {
      "description": ""
    }
  }]
}, {
  "title": "User 2",
  "id": "2",
  "schedule": [{
    "text": "",
    "start": "2025/04/15 09:45",
    "end": "2025/04/15 10:50",
    "data": {
      "something": "something"
    }
  }]
}, {
  "title": "User 3",
  "id": "3",
  "schedule": [{
    "text": "",
    "start": "2025/04/15 12:15",
    "end": "2025/04/15 14:30",
    "data": {
      "something": "something"
    }
  }]
}, {
  "title": "User 4",
  "id": 4,
  "schedule": [{
    "text": "",
    "start": "2025/04/15 14:15",
    "end": "2025/04/15 15:30",
    "data": {
      "something": "something"
    }
  }]
}]);
const sampleSetting = ref({
  "startDate": "2025/04/15",
  "endDate": "2025/04/15",
  "unit": 60,
  "borderW": 0,
  "dateDivH": 25,
  "timeDivH": 25,
  "unitDivW": 50,
  "titleDivW": 19,
  "rowH": 35
});

const rowDeleteEvent = (rowIndex, originalId) => {
    sampleScheduleContactAndUserData.value.splice(rowIndex, 1);
    forceRerender();
}

const renderComponent = ref(true);
const forceRerender = async () => {
  // Remove MyComponent from the DOM
  renderComponent.value = false;
  // Wait for the change to get flushed to the DOM
  await nextTick();
  // Add the component back in
  renderComponent.value = true;
};

</script>

<template>
  <div class="centered-container">
    <div class="content-box">
      <h1><b>Vue.js 3 Day Scheduler</b></h1>
      <br/>
      <callScheduler 
        @row-delete-event="rowDeleteEvent"
        :schedule-data="sampleScheduleContactAndUserData"
        :setting="sampleSetting"
        v-if="renderComponent"
      />
    </div>
  </div>  
</template>