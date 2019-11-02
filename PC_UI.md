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
 
 ```
 3.
 ```
  
 ```
 4.
 ```