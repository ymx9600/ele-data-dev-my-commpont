<!-- ele-data-table 封装一个类似demo做相同组件的事情 -->
 <template>
  <el-data-table v-bind="$data" >
     <el-table-column label="操作">
      <template slot-scope="scope">
        <div class="operate">
        <el-button
          size="small"
          type="primary"
          @click="handleSel(scope.$index, scope.row)">查看</el-button>
        <el-button
          size="small"
          @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
          <el-button
          size="small"
          @click="handleDelete(scope.$index, scope.row)">删除</el-button>
          </div>
      </template>
      
    </el-table-column>
  </el-data-table>
</template>

<script>
export default {
  data() {
    return {
          url:'https://easy-mock.com/mock/5d58e11f56d091465f8b19bf/example/query#!method=get',
          // url:'/example/user',
           tableAttrs: {
            cellClassName: function(obj) {
              let index=6;
              return obj.row.status!='normal' && (obj.columnIndex==index)  ? 'status':'';
            }
            
          },
          columns: [
            {prop:'check',  type: 'selection'},
            {prop: 'cmptName',label: '组件名称'},
            {prop: 'sortName',label: '分类' },
            {prop: 'version', label: '版本'},
            {prop: 'devLanguage', label: '开发语言'},
            {prop: 'lstUpdate', label: '最后更新时间',
              formatter: (row)=>{
                   return row.lstUpdate.split('.').join('-');
              }
            },
            {  prop: 'status', label: '状态',
            
            formatter: row => (row.status === 'normal' ? '下架' : '上架')         
            },
          ],
              hasOperation:false,

          searchForm: [
            {
              type: 'input',id: 'name', label: '组件名称',
              el: { placeholder: '请输入'}
            },
            {
                type: 'select',id: 'sortName', label: '分类',
                el: { placeholder: '请选择'}
            },
            {
                type: 'select',id: 'status', label: '状态',
                el: { placeholder: '请选择'}
            },
          ],
          form: [{
            type: 'input',  id: 'name',  label: '新增组件名称',
            el: {
              placeholder: '请输入新增组件名称',
            },
            rules: [{
              required: true,
              message: '请输入新增组件名称',
              trigger: 'blur',
              // transform: v => v && v.trim()
                  transform:(v)=>{
                    //新增组件名称 提交组件名称
                    console.log( v)
                  }

            }],
            

          }], 


      }    
  },

  methods: {
    handleSel(index,row)
    {
    console.log("查看")
    },
    handleEdit(index,row)
    {
       console.log("编辑")
    },
    handleDelete(index,row)
    {
      console.log("上架下架")

    },
  },
  
}

</script>

<style lang="less">
.operate{
  width:210px;
}
.status{
  color:green;
}

</style>