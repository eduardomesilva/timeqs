<template>
  <div class="common-layout">
    <el-container>
      <el-aside>
        <el-menu
          default-active="1"
          class="el-menu-vertical-demo"
          :collapse="isCollapse"
          @open="handleOpen"
          @close="handleClose"
          :vue-router="true"
        >
          <el-menu-item index="1" @click="redirect('jogadores')">
            <el-icon>
              <i class='fa fa-flag'></i>
            </el-icon>
              <span>Pontuar</span>
          </el-menu-item>
          <!-- //TODO: Colocar ícons -->
          <el-menu-item index="2" @click="redirect('teams')">
            <el-icon><i class="fa fa-question-circle"></i></el-icon>
            <span>Montar times</span>
          </el-menu-item>
          <el-menu-item index="3" @click="redirect('listPlayers')">
            <el-icon><i class="fa fa-question-circle"></i></el-icon>
            <span>Jogadores</span>
          </el-menu-item>
          <el-menu-item index="4"  @click="redirect('addPlayer')">
            <el-icon><i class="fa fa-question-circle"></i></el-icon>
            <span>Adicionar Jogadores</span>
          </el-menu-item>
        </el-menu>
      </el-aside>
      <el-main>
        <RouterView />
      </el-main>
    </el-container>
  </div>
</template>

<script lang="ts">
import { store } from './stores'
import {handleStorageMutation} from './services/storage'

export default {
  name: 'timeqs',
  store,
  data() {
    return {
      isCollapse: false,
    }
  },
  computed:{
    timeName(){
      return this.$route.params.timeName
    }
  },
  methods: {
    redirect(route: string){
      console.log(route)
      this.$router.push({name: route, params: this.$route.params});
    }
  },
  mounted() {
    store().$subscribe(handleStorageMutation, {deep: true})
  }
}
</script>


<style>
@import '@/assets/base.css';

body{
  font-family: 'Helvetica Neue', Helvetica, 'PingFang SC', 'Hiragino Sans GB',
  'Microsoft YaHei', '微软雅黑', Arial, sans-serif;
}

</style>
