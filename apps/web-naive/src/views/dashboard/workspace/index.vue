<script lang="ts" setup>
import type {
  WorkbenchProjectItem,
  WorkbenchQuickNavItem,
  WorkbenchTodoItem,
  WorkbenchTrendItem,
} from '@vben/common-ui';

import { ref } from 'vue';
import { useRouter } from 'vue-router';

import {
  AnalysisChartCard,
  WorkbenchHeader,
  WorkbenchProject,
  WorkbenchQuickNav,
  WorkbenchTodo,
  WorkbenchTrends,
} from '@vben/common-ui';
import { preferences } from '@vben/preferences';
import { useUserStore } from '@vben/stores';
import { openWindow } from '@vben/utils';

import AnalyticsVisitsSource from '../analytics/analytics-visits-source.vue';

const userStore = useUserStore();

// 这是一个示例数据，实际项目中需要根据实际情况进行调整
// url 也可以是内部路由，在 navTo 方法中识别处理，进行内部跳转
// 例如：url: /dashboard/workspace
const projectItems: WorkbenchProjectItem[] = [
  {
    color: '',
    content: "Don't wait for opportunities, create them.",
    date: '2021-04-01',
    group: 'Open Source Group',
    icon: 'carbon:logo-github',
    title: 'Github',
    url: 'https://github.com',
  },
  {
    color: '#3fb27f',
    content: 'Who you are now determines who you will be.',
    date: '2021-04-01',
    group: 'Algorithm Group',
    icon: 'ion:logo-vue',
    title: 'Vue',
    url: 'https://vuejs.org',
  },
  {
    color: '#e18525',
    content: 'No talent is more important than effort.',
    date: '2021-04-01',
    group: 'Slacking at Work',
    icon: 'ion:logo-html5',
    title: 'Html5',
    url: 'https://developer.mozilla.org/en-US/docs/Web/HTML',
  },
  {
    color: '#bf0c2c',
    content: 'Passion and desire can overcome all difficulties.',
    date: '2021-04-01',
    group: 'UI',
    icon: 'ion:logo-angular',
    title: 'Angular',
    url: 'https://angular.io',
  },
  {
    color: '#00d8ff',
    content: 'A healthy body is the cornerstone of achieving goals.',
    date: '2021-04-01',
    group: 'Tech Guru',
    icon: 'bx:bxl-react',
    title: 'React',
    url: 'https://reactjs.org',
  },
  {
    color: '#EBD94E',
    content: 'The path is walked out, not imagined.',
    date: '2021-04-01',
    group: 'Architecture Group',
    icon: 'ion:logo-javascript',
    title: 'Js',
    url: 'https://developer.mozilla.org/en-US/docs/Web/JavaScript',
  },
];

// 同样，这里的 url 也可以使用以 http 开头的外部链接
const quickNavItems: WorkbenchQuickNavItem[] = [
  {
    color: '#1fdaca',
    icon: 'ion:home-outline',
    title: 'Home',
    url: '/',
  },
  {
    color: '#bf0c2c',
    icon: 'ion:grid-outline',
    title: 'Dashboard',
    url: '/dashboard',
  },
  {
    color: '#e18525',
    icon: 'ion:layers-outline',
    title: 'Components',
    url: '/demos/features/icons',
  },
  {
    color: '#3fb27f',
    icon: 'ion:settings-outline',
    title: 'System Management',
    url: '/demos/features/login-expired', // 这里的 URL 是示例，实际项目中需要根据实际情况进行调整
  },
  {
    color: '#4daf1bc9',
    icon: 'ion:key-outline',
    title: 'Permission Management',
    url: '/demos/access/page-control',
  },
  {
    color: '#00d8ff',
    icon: 'ion:bar-chart-outline',
    title: 'Charts',
    url: '/analytics',
  },
];

const todoItems = ref<WorkbenchTodoItem[]>([
  {
    completed: false,
    content: `Review recently submitted frontend code to the Git repository, ensuring code quality and standards.`,
    date: '2024-07-30 11:00:00',
    title: 'Review Frontend Code Submission',
  },
  {
    completed: true,
    content: `Check and optimize system performance, reducing CPU usage.`,
    date: '2024-07-30 11:00:00',
    title: 'System Performance Optimization',
  },
  {
    completed: false,
    content: `Perform system security checks to ensure no security vulnerabilities or unauthorized access. `,
    date: '2024-07-30 11:00:00',
    title: 'Security Check',
  },
  {
    completed: false,
    content: `Update all npm dependencies in the project to ensure the latest versions are used.`,
    date: '2024-07-30 11:00:00',
    title: 'Update Project Dependencies',
  },
  {
    completed: false,
    content: `Fix page UI display issues reported by users, ensuring consistent display across different browsers. `,
    date: '2024-07-30 11:00:00',
    title: 'Fix UI Display Issues',
  },
]);
const trendItems: WorkbenchTrendItem[] = [
  {
    avatar: 'svg:avatar-1',
    content: `Created project <a>Vue</a> in <a>Open Source Group</a>`,
    date: 'Just now',
    title: 'William',
  },
  {
    avatar: 'svg:avatar-2',
    content: `Followed <a>William</a> `,
    date: '1 hour ago',
    title: 'Aven',
  },
  {
    avatar: 'svg:avatar-3',
    content: `Posted a <a>personal update</a> `,
    date: '1 day ago',
    title: 'Chris',
  },
  {
    avatar: 'svg:avatar-4',
    content: `Published an article <a>How to write a Vite plugin</a> `,
    date: '2 days ago',
    title: 'Vben',
  },
  {
    avatar: 'svg:avatar-1',
    content: `Replied to <a>Jack's</a> question <a>How to optimize the project?</a>`,
    date: '3 days ago',
    title: 'Peter',
  },
  {
    avatar: 'svg:avatar-2',
    content: `Closed the question <a>How to run the project</a> `,
    date: '1 week ago',
    title: 'Jack',
  },
  {
    avatar: 'svg:avatar-3',
    content: `Posted a <a>personal update</a> `,
    date: '1 week ago',
    title: 'William',
  },
  {
    avatar: 'svg:avatar-4',
    content: `Pushed code to <a>Github</a>`,
    date: '2021-04-01 20:00',
    title: 'William',
  },
  {
    avatar: 'svg:avatar-4',
    content: `Published an article <a>How to write using Admin Vben</a> `,
    date: '2021-03-01 20:00',
    title: 'Vben',
  },
];

const router = useRouter();

// 这是一个示例方法，实际项目中需要根据实际情况进行调整
// This is a sample method, adjust according to the actual project requirements
function navTo(nav: WorkbenchProjectItem | WorkbenchQuickNavItem) {
  if (nav.url?.startsWith('http')) {
    openWindow(nav.url);
    return;
  }
  if (nav.url?.startsWith('/')) {
    router.push(nav.url).catch((error) => {
      console.error('Navigation failed:', error);
    });
  } else {
    console.warn(`Unknown URL for navigation item: ${nav.title} -> ${nav.url}`);
  }
}
</script>

<template>
  <div class="p-5">
    <WorkbenchHeader
      :avatar="userStore.userInfo?.avatar || preferences.app.defaultAvatar"
    >
      <template #title>
        早安, {{ userStore.userInfo?.realName }}, 开始您一天的工作吧！
      </template>
      <template #description> 今日晴，20℃ - 32℃！ </template>
    </WorkbenchHeader>

    <div class="mt-5 flex flex-col lg:flex-row">
      <div class="mr-4 w-full lg:w-3/5">
        <WorkbenchProject :items="projectItems" title="项目" @click="navTo" />
        <WorkbenchTrends :items="trendItems" class="mt-5" title="最新动态" />
      </div>
      <div class="w-full lg:w-2/5">
        <WorkbenchQuickNav
          :items="quickNavItems"
          class="mt-5 lg:mt-0"
          title="快捷导航"
          @click="navTo"
        />
        <WorkbenchTodo :items="todoItems" class="mt-5" title="待办事项" />
        <AnalysisChartCard class="mt-5" title="访问来源">
          <AnalyticsVisitsSource />
        </AnalysisChartCard>
      </div>
    </div>
  </div>
</template>
