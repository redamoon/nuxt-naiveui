<template>
  <NConfigProvider :theme-overrides="themeOverrides">
    <h1>Hello, {{ name }}</h1>
    <NButton @click="alert" type="primary">alert ボタン</NButton>
    <NDataTable
      :data="data"
      :columns="columns"
    />
    <h2>Expand rows</h2>
    <NDataTable
      :data="data"
      :columns="columnsExpand"
    />
  </NConfigProvider>
</template>

<script>
  import { defineComponent } from 'vue'
  import { NConfigProvider, NTag, NButton, NDataTable } from 'naive-ui'



  export default defineComponent({
    components: {
      NButton,
      NDataTable,
      NTag,
      NConfigProvider
    },
    setup() {
      // テーマの変更はsetupで行う
      // FYI : https://github.com/tusen-ai/naive-ui/issues/649
      const themeOverrides = {
        common: {
          primaryColor: '#07B53B',
          primaryColorHover: '#04942f',
          fontSize: '100px'
        },
        Button: {
          primaryColor: '#07B53B',
          textColor: '#CCC'
        },
        Select: {
          peers: {
            InternalSelection: {
              textColor: '#FF0000'
            }
          }
        }
      }
      return { themeOverrides };
    },
    data() {
      return {
        name: 'Redamoon',
        columnsExpand: [
          {
            title: "No",
            key: "age"
          },
          {
            title: "Title",
            key: "name"
          },
          {
            type: "expand",
            // expandable 設定の拡張
            expandable: (rowData) => rowData?.expandData && rowData.expandData !== '',
            renderExpand: (rowData) => {
              return `${rowData.expandData}`;
            }
          }
        ],
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
                    type: "primary",
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
            tags: ["wow"],
            expandData: ''
          },
          {
            key: 2,
            name: 'Joe Black',
            age: 32,
            address: 'Sidney No. 1 Lake Park',
            chinese: 98,
            math: 66,
            english: 89,
            tags: ["cool", "teacher"],
            expandData: '開閉時2'
          },
          {
            key: 3,
            name: 'Jim Red',
            age: 32,
            address: 'London No. 2 Lake Park',
            chinese: 88,
            math: 99,
            english: 89,
            tags: ["wow"],
            expandData: '開閉時3'
          },
          {
            key: 4,
            name: 'Jim Red',
            age: 32,
            address: 'London No. 2 Lake Park',
            chinese: 88,
            math: 99,
            english: 89,
            tags: ["wow"],
            expandData: '開閉時4'
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
