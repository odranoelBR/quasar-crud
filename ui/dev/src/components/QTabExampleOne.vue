<template>
  <div>
    <q-tabs
      v-model="tab"
      align="justify"
      narrow-indicator
      class="bg-grey-2 text-teal"
    >
      <q-tab
        class="text-purple"
        name="example"
        label="Example"
      />
      <q-tab
        class="text-orange"
        name="template"
        label="Template"
      />
      <q-tab
        class="text-teal"
        name="script"
        label="Script"
      />
    </q-tabs>

    <q-tab-panels
      keep-alive
      v-model="tab"
      animated
      transition-prev="scale"
      transition-next="scale"
    >
      <q-tab-panel
        name="example"
        ref="panel"
      >
        <crud
          :columns.sync="columns"
          :http="axios"
          :list-index="list => list.data"
          :pagination.sync="pagination"
          @request="request"
          :filter="filter"
          api="api/users"
          title="Emails"
          row-key="id"
        >
          <template v-slot:top-right>
            <q-input
              borderless
              dense
              debounce="300"
              v-model="filter"
              placeholder="Search"
            >
              <template v-slot:append>
                <q-icon name="search" />
              </template>
            </q-input>
          </template>
        </crud>
      </q-tab-panel>

      <q-tab-panel name="template">
        <highlightjs
          language="htmlbars"
          :code="code"
        />
      </q-tab-panel>

      <q-tab-panel name="script">
        <highlightjs
          language="javascript"
          :code="columnsString"
        />
      </q-tab-panel>
    </q-tab-panels>
  </div>
</template>

<script>
import Crud from '../../../src/components/Crud'
import axios from 'axios'

export default {
  components: {
    Crud
  },
  created () {
    this.axios = axios.create({ baseURL: 'https://reqres.in/' })
  },
  methods: {
    request (props) {
      console.log(props)
    }
  },
  data: () => ({
    pagination: {
      sortBy: 'desc',
      descending: false,
      page: 1,
      rowsPerPage: 3,
      rowsNumber: 10
    },
    filter: null,
    tab: 'example',
    axios: null,
    code: `<crud
 :columns.sync="columns"
 :http="axios"
 :list-index="list => list.data"
 api="api/users"
 title="Emails"
 row-key="id"
/>`,
    columns: [
      {
        name: 'first_name',
        required: true,
        label: 'Name',
        align: 'left',
        field: 'first_name',
        qComponent: 'QInput',
        value: '',
        size: '6',
        rules: [val => val && val.length > 0 || 'Please type something'],
        showCreate: true,
        showUpdate: true
      },
      {
        name: 'email',
        required: true,
        label: 'Email',
        align: 'center',
        field: 'email',
        qComponent: 'QInput',
        value: '',
        size: '6',
        showCreate: true,
        showUpdate: true
      }
    ]
  }),
  computed: {
    columnsString () {
      let columns = JSON.parse(JSON.stringify(this.columns))
      columns[0].rules = '[val => val && val.length > 0 || "Please type something"]'
      return 'columns: ' + JSON.stringify(columns, null, 2)
    }
  }
}
</script >

<style lang="sass" scoped>
.q-tab-panel
  padding: 0px
</style>