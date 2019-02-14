<template>
  <div class="container">
    <el-data-table v-bind="tableConfig"></el-data-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableConfig: {
        url: '/components',
        columns: [
          {
            type: 'selection'
          },
          {
            prop: 'name',
            label: '组件名称'
          },
          {
            prop: 'type',
            label: '分类',
            formatter: row => this.$store.state.typeMap[row.type]
          },
          {
            prop: 'version',
            label: '版本',
            formatter: row => row.version.toFixed(3)
          },
          {
            prop: 'language',
            label: '开发语言',
            formatter: row => this.$store.state.languageMap[row.language]
          },
          {
            prop: 'updateTime',
            label: '更新时间',
            formatter: row => row.updateTime.substring(0, 10)
          },
          {
            prop: 'status',
            label: '状态',
            formatter: row => this.$store.state.statusMap[row.status]
          }
        ],
        searchForm: [
          {
            $type: 'input',
            $id: 'name',
            label: '组件名称',
            $el: {
              placeholder: '请输入',
              icon: 'menu'
            }
          },
          {
            $type: 'select',
            $id: 'type',
            label: '类型',
            $options: ['前端组件', '后端组件'].map((val, index) => ({
              label: val,
              value: index + 1
            })),
            $el: {
              placeholder: '请选择'
            }
          },
          {
            $type: 'select',
            $id: 'status',
            label: '状态',
            $options: ['下架', '上架'].map((val, index) => ({
              label: val,
              value: index
            })),
            $el: {
              placeholder: '请选择'
            }
          }
        ],
        form: [
          {
            $type: 'input',
            $id: 'name',
            label: '用户名',
            $el: {
              placeholder: '请输入'
            },
            rules: [
              {
                required: true,
                message: '请输入用户名',
                trigger: 'blur'
              }
            ]
          }
        ]
      }
    }
  },
  methods: {
    onSubmit() {
      console.log(this.$refs)
    },
    resetForm() {
      this.$refs.query.resetFields()
    },
    onDelete() {},
    add() {}
  }
}
</script>

<style scoped lang="stylus">
.query
  display flex
</style>
