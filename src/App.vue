<template>
  


<div id="app">
  <h1 style="text-align: center;">Kegiatan</h1> 
  <table style="width: 60%; margin: 0 auto;">
    <thead>
      <tr>
        <th>Kegiatan</th>
        <th>Status</th>
        <th>Tindakan</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="activity in activities" :key="activity.id" :class="{ completed: activity.selesai }"> 
        <td>
          <span :class="{ 'completed-text': activity.selesai }">{{ activity.name }}</span> 
        </td>
        <td>
          <span>{{ activity.selesai ? 'Telah Selesai' : 'Belum Selesai' }}</span>
          <input type="checkbox" v-model="activity.selesai">
        </td>
        <td>
          <button @click="cancelActivity(activity.id)">Batalkan</button>
        </td>
      </tr>
    </tbody>
  </table>

  <form @submit.prevent="addActivity" style="text-align: center; margin-top: 20px;">
    <input type="text" v-model="newActivity" placeholder="Tambahkan kegiatan">
    <button type="submit">Tambahkan</button>
  </form>
</div>
</template>

<script>
  const { ref } = Vue;

  const activities = ref([
    { id: 1, name: 'Senam', selesai: false },
  ]);

  const newActivity = ref('');

  function addActivity() {
    if (newActivity.value.trim() !== '') {
      activities.value.push({ id: Date.now(), name: newActivity.value, selesai: false });
      newActivity.value = '';
    }
  }

  function cancelActivity(id) {
    const index = activities.value.findIndex(activity => activity.id === id);
    if (index !== -1) {
      activities.value.splice(index, 1);
    }
  }

  Vue.createApp({
    setup() {
      return { activities, newActivity, addActivity, cancelActivity };
    }
  }).mount('#app');
</script>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f2f2f2;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.completed-text {
  text-decoration: line-through;
}

button {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #0056b3;
}

input[type="text"] {
  padding: 8px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

button[type="submit"] {
  background-color: #28a745;
}

button[type="submit"]:hover {
  background-color: #218838;
}

</style>

