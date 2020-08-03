<template>
  <div class="time-content row">
    <!-- 时间类 -->
    <div class="input-common" style="margin:0 10px">
      <el-select
        :popper-append-to-body="false"
        @change="selectChange"
        v-model="postData.timeType"
        placeholder="类"
      >
        <el-option
          v-for="item in dateList"
          :key="item.label"
          :label="item.label"
          :value="item.value"
        ></el-option>
      </el-select>
    </div>
    <!-- 开始结束时间 -->
    <div class="input-common dateRange flex-box">
      <el-date-picker
        v-if="pouponPost.format"
        class="date-picker"
        :value-format="pouponPost.valueFormat"
        :format="pouponPost.format"
        @change="dayChange"
        v-model="postData.time"
        :type="pouponPost.type"
        placeholder="开始时间"
      ></el-date-picker>
      <span style="color:#dfdfdf;margin:0 5px;line-height:32px">一</span>
      <el-date-picker
        v-if="pouponPost.format"
        class="date-picker"
        :value-format="pouponPost.valueFormat"
        :format="pouponPost.format"
        @change="dayChange"
        v-model="postData.time"
        :type="pouponPost.type"
        placeholder="结束时间"
      ></el-date-picker>
    </div>
  </div>
</template>

<script>
import { getDay } from "@/assets/js/formatDate";
export default {
  name: "timeContent",
  data() {
    return {
      dateList: [
        {
          value: "s",
          label: "时",
        },
        {
          value: "d",
          label: "日",
        },
        {
          value: "m",
          label: "月",
        },
        {
          value: "y",
          label: "年",
        },
      ],
      pouponPost: {
        type: "datetime",
        valueFormat: "yyyyMMddHHmmss",
        format: "yyyy-MM-dd HH:mm:ss",
      },
      pouponPostList: {
        s: {
          type: "datetime",
          valueFormat: "yyyyMMddHHmmss",
          format: "yyyy-MM-dd HH:mm:ss",
        },
        d: {
          type: "date",
          valueFormat: "yyyyMMdd",
          format: "yyyy-MM-dd",
        },
        m: {
          type: "month",
          valueFormat: "yyyyMM",
          format: "yyyy-MM",
        },
        y: {
          type: "year",
          valueFormat: "yyyy",
          format: "yyyy年",
        },
      },
      postData: {
        time: "",
        timeType: "",
      },
    };
  },
  methods: {
    // 日期改变
    dayChange(val) {
      //   this.$emit("changePostVal", { name: "time", val: val });
    },
    // 日期类型改变
    selectChange(val) {
      //   var dinl = getDay(0);
      //   if (val == "d") {
      //     dinl = getDay(-1);
      //   } else if (val == "m") {
      //     dinl = dinl.slice(0, 6);
      //   } else if (val == "y") {
      //     dinl = dinl.slice(0, 4);
      //   }
      //   this.$emit("changePostVal", {
      //     name: "time",
      //     val: dinl,
      //   });
      this.pouponPost = this.pouponPostList[val];
    },
  },
};
</script>

<style scoped lang="scss">
.time-content {
    // width: 50%;
   
  // 修改selecte格式
  .input-common {
    // margin-left: 15px;
    /deep/ .el-select .el-input__inner {
      width: 65px;
    }
    /deep/ .el-input__inner {
      height: 32px;
      line-height: 32px;
      background-color: #fff;
      border-radius: 4px;
      border: 1px solid #dfdfdf;
      color: #323232;
    }
    /deep/ .el-input__icon {
      line-height: 32px;
      color: #323232;
    }
    /deep/ .el-icon-time {
      display: none;
    }
    /deep/ .el-input--suffix .el-input__inner {
      padding: 0 15px;
    }

    /deep/ .el-icon-date {
      display: none;
    }
  }
  // 日期格式
  /deep/ .date .el-input--suffix .el-input__inner {
    width: 150px;
  }
  /deep/ .el-picker-panel {
    color: #323232;
    border: 1px solid #dfdfdf;
  }
  /deep/ .el-date-editor.el-input,  /deep/ .el-date-editor.el-input__inner{
    //   min-width: 180px;
      max-width: 225px;
      width: 45%;
  }
}
</style>
