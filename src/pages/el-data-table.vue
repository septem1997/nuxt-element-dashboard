<template>
  <div class="container">
    <el-data-table v-bind="tableConfig" ref="table">
      <el-table-column prop="status" label="状态">
        <template scope="scope">
          <span style="color: red;" v-if="scope.row.status === 1">上架</span>
          <span style="color: gray;" v-else-if="scope.row.status === 0"
            >下架</span
          >
        </template>
      </el-table-column>
    </el-data-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableConfig: {
        url: '/components',
        operationAttrs: {
          width: 300,
          fixed: 'right'
        },
        hasEdit: false,
        extraButtons: [
          {
            text: '查看',
            type: 'primary',
            atClick: row => {
              this.$refs.table.onDefaultView(row)
              return Promise.resolve()
            }
          },
          {
            text: '编辑',
            atClick: row => {
              this.$refs.table.onDefaultEdit(row)
              return Promise.resolve()
            }
          },
          {
            text: '下架',
            atClick: row => Promise.resolve(),
            show: row => row.status > 0
          },
          {
            text: '上架',
            atClick: row => Promise.resolve(),
            show: row => !row.status > 0
          }
        ],
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
          }
        ],
        searchForm: [
          {
            $type: 'input',
            $id: 'name',
            label: '组件名称',
            $el: {
              placeholder: '请输入',
              'suffix-icon': 'el-icon-edit'
            }
          },
          {
            $type: 'select',
            $id: 'type',
            label: '分类',
            $options: this.$store.state.typeMap.map((value, index) => ({
              value: index,
              label: value
            })),
            $el: {
              placeholder: '请选择'
            }
          },
          {
            $type: 'select',
            $id: 'status',
            label: '状态',
            $options: this.$store.state.statusMap.map((value, index) => ({
              value: index,
              label: value
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
            label: '组件名称',
            $el: {
              placeholder: '请输入'
            },
            rules: [
              {
                required: true,
                message: '请输入组件名称',
                trigger: 'blur'
              }
            ]
          },
          {
            $id: 'type',
            $type: 'select',
            label: '分类',
            $default: null,
            $el: {
              placeholder: '请选择',
              style: 'width: 100%'
            },
            rules: [
              {
                required: true,
                message: '请选择分类',
                trigger: 'blur'
              }
            ],
            $options: this.$store.state.typeMap.map((value, index) => ({
              label: value,
              value: index + 1
            }))
          },
          {
            $type: 'input',
            $id: 'version',
            label: '版本',
            $el: {
              placeholder: '请输入'
            },
            rules: [
              {
                required: true,
                message: '请输入版本号',
                trigger: 'blur'
              }
            ]
          },
          {
            $id: 'language',
            $type: 'select',
            label: '开发语言',
            $el: {
              placeholder: '请选择',
              style: 'width: 100%'
            },
            rules: [
              {
                required: true,
                message: '请选择语言',
                trigger: 'blur'
              }
            ],
            $options: this.$store.state.languageMap.map((value, index) => ({
              label: value,
              value: index + 1
            }))
          },
          {
            $id: 'updateTime',
            $type: 'date-picker',
            label: '更新时间',
            $el: {
              placeholder: '请选择',
              valueFormat: 'yyyy-MM-dd',
              style: 'width: 100%'
            }
          },
          {
            $id: 'status',
            $type: 'select',
            label: '状态',
            $el: {
              placeholder: '请选择',
              style: 'width: 100%'
            },
            rules: [
              {
                required: true,
                message: '请选择状态',
                trigger: 'blur'
              }
            ],
            $options: this.$store.state.statusMap.map((value, index) => ({
              label: value,
              value: index
            }))
          }
        ]
      }
    }
  },
  methods: {}
}
</script>

<style scoped lang="stylus">
.query
  display flex
</style>
