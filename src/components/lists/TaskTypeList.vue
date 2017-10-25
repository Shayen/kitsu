<template>
<div class="data-list">
  <table class="table">
    <thead>
      <tr>
        <th class="name">{{ $t('task_types.fields.name') }}</th>
        <th class="priority">{{ $t('task_types.fields.priority') }}</th>
        <th class="dedicated">{{ $t('task_types.fields.dedicated_to') }}</th>
        <th class="actions"></th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="entry in entries">
        <task-type-name class="name" :entry="entry"></task-type-name>
        <td class="priority">{{ entry.priority }}</td>
        <td class="dedicated">{{ renderForShots(entry) }}</td>
        <row-actions
          :entry-id="entry.id"
          :edit-route="{
            name: 'edit-production',
            params: {production_id: entry.id}
          }"
          :delete-route="{
            name: 'delete-production',
            params: {production_id: entry.id}
          }"
        >
        </row-actions>
      </tr>
    </tbody>
  </table>

  <div class="has-text-centered" v-if="isLoading">
    <img src="../../assets/spinner.svg">
  </div>
  <div class="has-text-centered" v-if="isError">
    <span class="tag is-danger">An error occured while loading data</span>
  </div>

  <p class="has-text-centered nb-task-types">
    {{ entries.length }} {{ $tc('task_types.number', entries.length) }}
  </p>

</div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
import RowActions from '../widgets/RowActions'
import TaskTypeName from '../cells/TaskTypeName'

export default {
  name: 'task-type-list',
  props: [
    'entries',
    'isLoading',
    'isError'
  ],
  data () {
    return {}
  },
  components: {
    RowActions,
    TaskTypeName
  },
  computed: {
    ...mapGetters([
    ])
  },
  methods: {
    ...mapActions([
    ]),
    renderForShots (entry) {
      if (entry.for_shots) {
        return this.$tc('shots.title')
      } else {
        return this.$tc('assets.title')
      }
    }
  }
}
</script>

<style scoped>
.name {
  width: 200px;
  min-width: 200px;
}

.priority {
  width: 80px;
  min-width: 80px;
  font-weight: normal;
}

.dedicated {
  width: 100px;
  min-width: 100px;
  font-weight: normal;
}

.actions {
  min-width: 100px;
}

.color {
  width: 100px;
}
</style>