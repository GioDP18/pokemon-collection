<template>
  <div class="whole">
    <div class="transparent">

      <!-- Head -->
      <div class="header">
        <h3 class="text-white">Top 3 Pokémon</h3>
        <q-btn-dropdown class="dd-buton" color="" label="Today">
          <q-list>
            <q-item clickable v-close-popup @click="onItemClick">
              <q-item-section>
                <q-item-label>Today</q-item-label>
              </q-item-section>
            </q-item>

            <q-item clickable v-close-popup @click="onItemClick">
              <q-item-section>
                <q-item-label>Yesterday</q-item-label>
              </q-item-section>
            </q-item>

            <q-item clickable v-close-popup @click="onItemClick">
              <q-item-section>
                <q-item-label>All</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>
      </div>

      <!-- Cards -->
      <div class="cards">
        <q-card class="my-card text-white">
          <q-card-section>
            <div class="text-h6">Our Changing Planet</div>
            <div class="text-subtitle2">by John Doe</div>
          </q-card-section>

          <q-card-section>
            {{ lorem }}
          </q-card-section>
        </q-card>
        <q-card class="my-card text-white">
          <q-card-section>
            <div class="text-h6">Our Changing Planet</div>
            <div class="text-subtitle2">by John Doe</div>
          </q-card-section>

          <q-card-section>
            {{ lorem }}
          </q-card-section>
        </q-card>
        <q-card class="my-card text-white">
          <q-card-section>
            <div class="text-h6">Our Changing Planet</div>
            <div class="text-subtitle2">by John Doe</div>
          </q-card-section>

          <q-card-section>
            {{ lorem }}
          </q-card-section>
        </q-card>
      </div>

      <!-- Table -->
      <div class="table-section">
        <table id="dailyTimeLog" class="table table-striped table-hover" width="100%;">
          <thead>
            <tr>
              <th>Date</th>
              <th>Arrival</th>
              <th>Departure</th>
              <th>Late</th>
              <th>Number of Hours Worked</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <th>vvsdv</th>
              <th>vwedsdv</th>
              <th>vweescd</th>
              <th>vsesdvd</th>
              <th>sdvsdvsd</th>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import 'datatables.net-vue3';
import 'datatables.net-bs5';

onMounted(async () => {
  initializeDataTables();
});

const initializeDataTables = () => {
  $(document).ready(function () {
    $('#dailyTimeLog').DataTable();
  });
}
</script>

<style lang="scss" scoped>
.whole {
  background-image: url('/images/pokemon.png');
  height: 13rem;
}

.transparent {
  height: 100vh;
  width: 75%;
  margin: auto;
  background-color: rgba(0, 0, 0, 0.5);
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header .dd-buton {
  background-color: #B64BFF;
  height: 2rem
}

.cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.my-card {
  width: 20rem;
  height: 15rem;
  border-radius: 8px;
}

.table-section {
  margin-top: 1rem;
}

.table-section .table {
  height: 400px;
  width: 100%;
  border-radius: 8px;
}
</style>
