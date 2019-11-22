 ### PC端UI框架使用常见问题

> Mint-ui

 ```js
 Loadmore--使用mint-ui上拉加载下拉刷新出现部分数据被遮盖情况
 解决方法: autoFill="false" 无效果 -可在循环层加height ---解决
 ```
> iview https://www.iviewui.com/components/upload

 ```html
    iview 上传图片或视频
       accept:文件类型 1:图片--"image/*"   2:视频--"video/*"
	<FormItem label="课程封面" prop="coverPicture" v-model="form.coverPicture">//show-upload-list是否显示图片列表--form.coverPicture绑定值
        <Upload action="链接" accept="image/*" ref="upload" v-model="form.coverPicture" :on-success="success" :show-upload-list="isUpload">
          <Button icon="ios-cloud-upload-outline" >上传图片</Button>
          <div style="width:296px;height:200px;background:#ccc;margin-top:15px;">
            <img style="width:296px;height:200px" :src="form.coverPicture" v-if="form.coverPicture"/>
             <template  v-if="!form.coverPicture">进度条
               <i-circle v-if="uploading.length" :percent="uploading[0].percentage">
                <span class="demo-Circle-inner" style="font-size:24px">{{(uploading[0].percentage).toFixed(0)}}%</span>
               </i-circle>
            </template>
          </div>
        </Upload>
      </FormItem>
	   mounted () {//初始化进度条
	      this.uploading = this.$refs.upload.fileList//进度条
	    },
		methods:{
			success (e, f, g) {//上传成功
			 this.$set(this.form, 'coverPicture', e.RetUrl)
			this.$refs.formValidate.validateField('coverPicture')
		   },
	  }
 ```
 > iview内置css操作

 ```css
 1.table表格去边框
 /deep/.small-table .ivu-table-cell {
   padding: 0px;
 }
 /deep/.ivu-table .demo-table-info-row td {
   font-size: 13px;
   font-family: PingFang SC;
   font-weight: 800;
   background: #fff;
   color: rgba(0, 113, 206, 1);
 }
 /deep/.ivu-card-body {
   padding: 0;
 }
 /deep/ .ivu-table-wrapper {
   border: none;
 }
 /deep/ .ivu-table:before {
   content: "";
   width: 100%;
   height: 0px;
   position: absolute;
   left: 0;
   bottom: 0;
   z-index: 1;
 }
 /deep/.ivu-table:after {
   content: "";
   width: 0px;
   height: 100%;
   position: absolute;
   top: 0;
   right: 0;
   z-index: 3;
 }
 /deep/.ivu-table td {
   border-bottom: none !important;
 }
 /deep/.ivu-row {
   border: none !important;
 }
 /deep/.ivu-table-wrapper {
   border: none !important;
 }
 /deep/.ivu-table-header th {
   // color:#FFD3B4;
   font-weight: bold;
   background-color: #fff;
   border: none;
 }
 
 
2. tab去边框
/deep/.ivu-tabs-bar {
  margin-top: 20px;
  border-bottom: none;
  display: flex;
  justify-content: center;
}


3. table去滚动条
  .ivu-table-overflowX::-webkit-scrollbar {display: none;}
 
 ```
  
>iview 打包不显示问题修复

 ```js
    找到 build 目录下 webpack.prod.conf.js 文件，
    rules: utils.styleLoaders({
    sourceMap: config.build.productionSourceMap,
    extract: ture,
    usePostCSS: true
    })
  把extract改成false即可
 ```