<script setup lang="ts">
import { computed, ref } from 'vue'
import {
  NovaEnvironment,
  NovaButton,
  NovaInput,
  NovaColorPicker,
  enUS,
} from '@jiangshengdev/nova-next'

const theme = ref<'light' | 'dark'>('light')
const nickname = ref('Nova 爱好者')
const accentColor = ref('#6366f1')
const presetColors = ['#6366f1', '#0ea5e9', '#10b981', '#f97316', '#f43f5e', '#a855f7']

const currentThemeLabel = computed(() => {
  return theme.value === 'light' ? '浅色' : '深色'
})

const accentChipStyle = computed(() => {
  return {
    background: accentColor.value,
  }
})

const toggleTheme = () => {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}

const resetNickname = () => {
  nickname.value = ''
}
</script>

<template>
  <div class="nova-demo-page">
    <h1>Nova Next 组件 Demo</h1>
    <p class="nova-demo-subtitle">
      下方示例通过 <code>@jiangshengdev/nova-next</code> 的 NovaEnvironment
      注入主题，并包含按钮与输入框。
    </p>

    <NovaEnvironment :theme="theme" :language="enUS">
      <section class="nova-demo-card">
        <h2>互动区</h2>
        <label class="nova-demo-label" for="demo-nickname">昵称</label>
        <div class="nova-demo-input">
          <NovaInput id="demo-nickname" v-model="nickname" placeholder="输入一个喜欢的称呼" />
        </div>

        <div class="nova-demo-actions">
          <NovaButton primary @click="toggleTheme">
            切换主题（当前：{{ currentThemeLabel }}）
          </NovaButton>
          <NovaButton :disabled="!nickname" @click="resetNickname">清空昵称</NovaButton>
        </div>
      </section>

      <section class="nova-demo-card">
        <h2>主题强调色</h2>
        <p class="nova-demo-hint">通过 NovaColorPicker 自定义强调色，并实时展示结果。</p>

        <div class="nova-demo-color-picker">
          <NovaColorPicker v-model="accentColor" :alpha="true" :preset="presetColors" />
        </div>

        <div class="nova-demo-accent-preview">
          <div class="nova-demo-accent-chip" :style="accentChipStyle" />
          <div>
            <p class="nova-demo-accent-label">当前值</p>
            <code>{{ accentColor }}</code>
          </div>
        </div>
      </section>
    </NovaEnvironment>
  </div>
</template>

<style scoped>
.nova-demo-page {
  max-width: 720px;
  margin: 2rem auto;
  padding: 0 1rem 2rem;
}

.nova-demo-subtitle {
  margin-top: 0.5rem;
  color: #6b7280;
  font-size: 0.95rem;
}

.nova-demo-card {
  margin-top: 1.5rem;
  padding: 1.5rem;
  border-radius: 16px;
  border: 1px solid #e5e7eb;
  background: #ffffff;
  box-shadow: 0 20px 45px rgba(15, 23, 42, 0.08);
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.nova-demo-label {
  font-weight: 600;
  font-size: 0.9rem;
}

.nova-demo-input {
  align-self: flex-start;
}

.nova-demo-hint {
  margin: -0.25rem 0 0.5rem;
  color: #6b7280;
  font-size: 0.9rem;
}

.nova-demo-actions {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.nova-demo-color-picker {
  align-self: flex-start;
}

.nova-demo-accent-preview {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1rem;
  border-radius: 12px;
  border: 1px dashed rgba(99, 102, 241, 0.4);
  background: rgba(99, 102, 241, 0.08);
}

.nova-demo-accent-chip {
  width: 48px;
  height: 48px;
  border-radius: 12px;
  border: 2px solid rgba(255, 255, 255, 0.6);
  box-shadow: 0 10px 20px rgba(15, 23, 42, 0.16);
}

.nova-demo-accent-label {
  margin: 0;
  color: #4b5563;
  font-size: 0.85rem;
}

@media (prefers-color-scheme: dark) {
  .nova-demo-card {
    border-color: #374151;
    background: #111827;
  }

  .nova-demo-subtitle {
    color: #9ca3af;
  }

  .nova-demo-hint {
    color: #9ca3af;
  }

  .nova-demo-accent-preview {
    border-color: rgba(129, 140, 248, 0.5);
    background: rgba(79, 70, 229, 0.16);
  }

  .nova-demo-accent-label {
    color: #e5e7eb;
  }
}
</style>
