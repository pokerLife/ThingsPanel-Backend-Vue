<template>
    <div class="common-video-container">
      <video-player  :src="optionData.src"/>
      <el-dialog class="el-dark-dialog" title="绑定" width="500px"
                 :visible.sync="dialogVisible" :append-to-body="true" :close-on-click-modal="false"
                 :before-close="handleClose">

        <el-form class="el-dark-form" :model="optionData" :rules="formRule">

          <el-form-item label="名称" prop="name">
            <el-input v-model="optionData.name"></el-input>
          </el-form-item>

          <el-form-item label="视频地址" prop="src">
            <el-input v-model="optionData.src"></el-input>
          </el-form-item>
        </el-form>

        <span slot="footer" class="dialog-footer">
          <el-button @click="handleClose">取 消</el-button>
          <el-button type="primary" @click="handleSubmit">确 定</el-button>
        </span>
      </el-dialog>
  </div>
</template>

<script>
import VideoPlayer from "@/components/common/VideoPlayer.vue";
const required = true;
export default {
  name: "CommonVideo",
  components: {
    VideoPlayer
  },
  props: {
    options: {
      type: [Object],
      default: () => { return {} }
    }
  },
  data() {
    return {
      optionData: {
        name: "",
        src: ""
      },
      formRule: {
        "name": [{required, message: "请输入视频名称"}],
        "src": [{required, message: "请输入视频地址"}]
      },
      dialogVisible: false
    }
  },
  methods: {
    /**
     * 打开对话框
     * @param option
     */
    showDialog(option) {
      this.optionData = JSON.parse(JSON.stringify(option));
      // 打开绑定对话框
      this.dialogVisible = true;
    },
    /**
     * 关闭
     */
    handleClose() {
      // 关闭绑定对话框
      this.dialogVisible = false;
    },
    /**
     * 提交绑定
     */
    handleSubmit() {
      this.$emit("submit", this.optionData)
      // 关闭绑定对话框
      this.handleClose();
    }
  }

}
</script>

<style scoped>
.common-video-container {
  width: 100%;
  height: 100%;
}
</style>