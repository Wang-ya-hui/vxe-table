<template>
  <div>
    <p>使用 vxe-excel 渲染 Excel 表格</p>
    <p>快捷键：方向键、Tab 键、Esc 键、F2 键、Del、Back 键、Ctrl 复制粘贴</p>

    <vxe-excel
      max-height="600"
      :columns="columns"
      :data.sync="tableData">
    </vxe-excel>

    <p>调用代码</p>

    <pre>
      <code class="xml">{{ demoCodes[0] }}</code>
      <code class="javascript">{{ demoCodes[1] }}</code>
    </pre>
  </div>
</template>

<script>
import hljs from 'highlight.js'

export default {
  data () {
    let columns = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P']
    return {
      columns: [
        {
          type: 'index',
          width: 50,
          fixed: 'left',
          align: 'center',
          headerAlign: 'center'
        }
      ].concat(columns.map(name => {
        return {
          prop: name.toLowerCase(),
          label: name,
          width: 76,
          headerAlign: 'center',
          editRender: {
            name: 'cell'
          }
        }
      })),
      tableData: Array.from(new Array(20)).map(() => {
        let item = {}
        columns.forEach(name => {
          item[name.toLowerCase()] = ''
        })
        return item
      }),
      demoCodes: [
        `
        <vxe-excel
          max-height="600"
          :data.sync="tableData">
        </vxe-excel
        `,
        `
        export default {
          data () {
            return {
              tableData: []
            }
          }
        }
        `
      ]
    }
  },
  mounted () {
    this.$el.querySelectorAll('pre code').forEach((block) => {
      hljs.highlightBlock(block)
    })
  }
}
</script>
