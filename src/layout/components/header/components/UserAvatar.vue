<template>
  <n-dropdown :options="options" @select="handleSelect">
    <div class="avatar">
      <img :src="userStore.avatar" />
      <span>{{ userStore.name }}</span>
    </div>
  </n-dropdown>
</template>

<script setup>
import { router } from '@/router'
import { useUserStore } from '@/store/modules/user'
import { IconExit } from '@/components/AppIcons'
import { renderIcon } from '@/utils/icon'

const userStore = useUserStore()

const options = [
  {
    label: '退出登录',
    key: 'logout',
    icon: renderIcon(IconExit, { size: '14px' }),
  },
]

function handleSelect(key) {
  if (key === 'logout') {
    $dialog.confirm({
      content: '确认退出？',
      confirm() {
        userStore.logout()
        $message.success('已退出登录')
        router.push({ path: '/login' })
      },
    })
  }
}
</script>

<style lang="scss" scoped>
.avatar {
  display: flex;
  align-items: center;
  cursor: pointer;
  img {
    width: 100%;
    width: 35px;
    height: 35px;
    border-radius: 50%;
    margin-right: 10px;
  }
}
</style>
