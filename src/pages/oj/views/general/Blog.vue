<template>
  <Row type="flex" justify="space-around">
    <Col :span="22">
      <div>
        <p>Test area</p>
      </div>
      <Blogcontext class="announcement"></Blogcontext>
    </Col>
  </Row>
</template>

<script>
import api from "@oj/api";
import time from "@/utils/time";
import Blogcontext from "./Blogcontext.vue";
import { CONTEST_STATUS } from "@/utils/constants";

export default {
  name: "home",
  components: {
    Blogcontext
  },
  data() {
    return {
      contests: [],
      index: 0
    };
  },
  mounted() {
    let params = { status: CONTEST_STATUS.NOT_START };
    api.getContestList(0, 5, params).then(res => {
      this.contests = res.data.data.results;
    });
  },
  methods: {
    getDuration(startTime, endTime) {
      return time.duration(startTime, endTime);
    },
    goContest() {
      this.$router.push({
        name: "contest-details",
        params: { contestID: this.contests[this.index].id }
      });
    }
  }
};
</script>

<style lang="less" scoped>
.contest {
  &-title {
    font-style: italic;
    font-size: 21px;
  }
  &-content {
    padding: 0 70px 40px 70px;
    &-description {
      margin-top: 25px;
    }
  }
}

.announcement {
  margin-top: 20px;
}
</style>