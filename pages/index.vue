<template>
  <h1>Hello, {{ name }}</h1>
  <NButton @click="alert">alert ボタン</NButton>
  <NDataTable
      :data="data"
      :columns="columns"
  />
</template>

<script>
  import { defineComponent } from 'vue'
  import { NTag, NButton, NDataTable } from 'naive-ui'


  export default defineComponent({
    components: {
      NButton,
      NDataTable,
      NTag
    },
    data() {
      return {
        name: 'ググりモグラ',
        columns: [
          {
            title: "No",
            key: "age"
          },
          {
            title: "Title",
            key: "name"
          },
          {
            title: "Tags",
            key: "tags",
            render(row) {
              const tags = row.tags.map((tagKey) => {
                return h(
                  NTag,
                  {
                    style: {
                      marginRight: "6px"
                    },
                    type: "info",
                    bordered: false
                  },
                  {
                    default: () => tagKey
                  }
                );
              });
              return tags;
            }
          }
        ],
        data: [
          {
            key: 0,
            name: 'John Brown',
            age: 32,
            address: 'New York No. 1 Lake Park',
            chinese: 98,
            math: 60,
            english: 70,
            tags: ["nice", "developer"]
          },
          {
            key: 1,
            name: 'Jim Green',
            age: 42,
            address: 'London No. 1 Lake Park',
            chinese: 98,
            math: 66,
            english: 89,
            tags: ["wow"]
          },
          {
            key: 2,
            name: 'Joe Black',
            age: 32,
            address: 'Sidney No. 1 Lake Park',
            chinese: 98,
            math: 66,
            english: 89,
            tags: ["cool", "teacher"]
          },
          {
            key: 3,
            name: 'Jim Red',
            age: 32,
            address: 'London No. 2 Lake Park',
            chinese: 88,
            math: 99,
            english: 89,
            tags: ["wow"]
          },
          {
            key: 3,
            name: 'Jim Red',
            age: 32,
            address: 'London No. 2 Lake Park',
            chinese: 88,
            math: 99,
            english: 89,
            tags: ["wow"]
          }
        ]
      }
    },
    methods: {
      alert() {
        alert('寿司が食べたい')
      }
    },
  })
</script>