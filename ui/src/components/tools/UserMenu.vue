<template>
  <div class="user-wrapper">
    <div class="content-box">
      <a href="https://keel.sh/v1/guide/" target="_blank">
        <span class="action">
          <a-icon type="question-circle-o"></a-icon>
        </span>
      </a>
      <!-- <notice-icon class="action"/> -->
      <a-dropdown>
        <span class="action ant-dropdown-link user-dropdown-menu">
          <!-- <a-avatar class="avatar" size="small" :src="avatar()"/> -->
          <a-icon type="dash"></a-icon>
          <!-- <span>{{ nickname() }}</span> -->
        </span>
        <a-menu slot="overlay" class="user-dropdown-menu-wrapper">
          <!-- <a-menu-item key="0">
            <router-link :to="{ name: 'center' }">
              <a-icon type="user"/>
              <span>个人中心</span>
            </router-link>
          </a-menu-item>
          <a-menu-item key="1">
            <router-link :to="{ name: 'settings' }">
              <a-icon type="setting"/>
              <span>账户设置</span>
            </router-link>
          </a-menu-item>
          <a-menu-item key="2" disabled>
            <a-icon type="setting"/>
            <span>测试</span>
          </a-menu-item>
          <a-menu-divider/> -->
          <a-menu-item key="3">
            <a href="javascript:;" @click="handleLogout">
              <a-icon type="logout"/>
              <span>Logout</span>
            </a>
          </a-menu-item>
        </a-menu>
      </a-dropdown>
    </div>
  </div>
</template>

<script>
import NoticeIcon from '@/components/NoticeIcon'
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'UserMenu',
  components: {
    NoticeIcon
  },
  methods: {
    ...mapActions(['LogoutSuccess']),
    ...mapGetters(['nickname', 'avatar']),
    handleLogout () {
      const that = this

      this.$confirm({
        title: 'Logout',
        content: 'Are you sure want to logout ?',
        onOk () {
          return that.$auth.logout({
            makeRequest: true,
            params: {}, // data: {}
            success: function () {
              that.LogoutSuccess({})
            },
            error: function () {},
            redirect: '/login'
            // etc...
          })
        },
        onCancel () {
        }
      })
    }
  }
}
</script>
