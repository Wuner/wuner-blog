<template>
  <Layout>
    <el-button @click="$router.go(-1)" type="text" icon="el-icon-d-arrow-left">
      返回
    </el-button>
    <el-card shadow="never" style="min-height: 400px">
      <div slot="header">
        <el-row>
          <el-col :span="12">
            <span>{{ $page.repos.name }}</span>
          </el-col>
          <el-col :span="12">
            <div style="text-align: right">
              <el-button
                @click="$share()"
                style="padding: 3px 0"
                type="text"
                icon="el-icon-share"
                >分享
              </el-button>
              <el-button
                @click="goGithub($page.repos.html_url)"
                style="padding: 3px 0"
                type="text"
                icon="el-icon-back"
                >前往GitHub
              </el-button>
              <el-button
                @click="more"
                style="padding: 3px 0"
                type="text"
                icon="el-icon-more-outline"
                >更多项目
              </el-button>
            </div>
          </el-col>
        </el-row>
      </div>
      <div style="font-size: 0.9rem; line-height: 1.5; color: #606c71">
        发布 {{ $page.repos.created_at | dateFilter }} <br />
        更新 {{ $page.repos.updated_at | dateFilter }}
      </div>
      <div
        style="
          font-size: 1.1rem;
          line-height: 1.5;
          color: #303133;
          padding: 20px 0px 0px 0px;
        "
      >
        {{ $page.repos.description }}
      </div>
      <div
        style="
          font-size: 1.1rem;
          color: #303133;
          padding: 15px 0px 15px 0px;
          border-bottom: 1px solid #e4e7ed;
        "
      >
        <el-row>
          <el-col :span="16" style="padding-top: 5px">
            <el-tooltip
              effect="dark"
              :content="'star ' + $page.repos.stargazers_count"
              placement="bottom"
            >
              <i class="el-icon-star-off" style="margin: 0px 5px 0px 0px"></i>
            </el-tooltip>
            {{ $page.repos.stargazers_count }}
            <el-tooltip
              effect="dark"
              :content="'watch ' + $page.repos.watchers_count"
              placement="bottom"
            >
              <i class="el-icon-view" style="margin: 0px 5px 0px 15px"></i>
            </el-tooltip>
            {{ $page.repos.watchers_count }}
            <el-tooltip
              effect="dark"
              :content="'fork ' + $page.repos.forks_count"
              placement="bottom"
            >
              <i class="el-icon-bell" style="margin: 0px 5px 0px 15px"></i>
            </el-tooltip>
            {{ $page.repos.forks_count }}
          </el-col>
          <el-col :span="8" style="text-align: right">
            <!--            <el-tag-->
            <!--              size="small"-->
            <!--              type="danger"-->
            <!--              v-if="$page.repos.license.spdx_id"-->
            <!--              >{{ $page.repos.license.spdx_id }}-->
            <!--            </el-tag>-->
            <el-tag size="small" type="success">{{
              $page.repos.language
            }}</el-tag>
          </el-col>
        </el-row>
      </div>
      <div
        v-html="$page.repos.content"
        v-if="$page.repos.content"
        class="markdown-body"
        style="padding-top: 20px"
      ></div>
      <div
        v-if="!$page.repos.content"
        style="padding: 20px 0px 20px 0px; text-align: center"
      >
        <font style="font-size: 30px; color: #dddddd">
          <b>还没有介绍 (╯°Д°)╯︵ ┻━┻</b>
        </font>
      </div>
    </el-card>
  </Layout>
</template>
<page-query>
query($id: ID!) {
  repos(id: $id){
    id,
    name,
    html_url,
    stargazers_count,
    watchers_count,
    forks_count,
    language,
    created_at,
    updated_at,
    description
  }
}
</page-query>
<script>
export default {
  metaInfo: {
    title: '开源项目',
  },
  methods: {
    goGithub(url) {
      window.open(url);
    },
    more() {
      this.$router.push('/source');
    },
  },
};
</script>
