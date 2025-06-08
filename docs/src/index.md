---
# https://vitepress.dev/reference/default-theme-home-page
layout: home
sidebar: false

hero:
  name: Vben Admin
  text: Enterprise Management System Framework
  tagline: Completely upgraded, ready to use, simple and efficient
  image:
    src: https://unpkg.com/@vbenjs/static-source@0.1.7/source/logo-v1.webp
    alt: Vben Admin
  actions:
    - theme: brand
      text: Quick Start ->
      link: /guide/introduction/quick-start
    - theme: alt
      text: Online Preview
      link: https://vben.pro
    - theme: alt
      text: View on GitHub
      link: https://github.com/elgaml/vue-vben-admin
    - theme: alt
      text: DeepWiki Documentation
      link: https://deepwiki.com/elgaml/vue-vben-admin

features:
  - icon: 🚀
    title: Latest Technology Stack
    details: Based on Vue3, Pinia, Vue Router, TypeScript, and other latest technology stacks.
    link: /guide/introduction/quick-start
    linkText: Quick Start
  - icon: 🦄
    title: Rich Configuration
    details: Enterprise-level mid-backend frontend solution, providing rich components and templates with N preference setting combinations.
    link: /guide/essentials/configuration
    linkText: Configuration Documentation
  - icon: 🎨
    title: Theme Customization
    details: Through simple configuration, various theme switches can be implemented to meet personalized needs.
    link: /guide/essentials/theme
    linkText: Theme Documentation
  - icon: 🌐
    title: Internationalization
    details: Built-in internationalization solution, supports multiple language switching, meets internationalization needs.
    link: /guide/in-depth/locale
    linkText: Internationalization Documentation
  - icon: 🔐
    title: Permission Management
    details: Built-in permission management solution, supports multiple permission control methods, meets various permission needs.
    link: /guide/in-depth/access
    linkText: Permission Documentation
  - title: Vite
    icon:
      src: /logos/vite.svg
    details: Modern front-end build tool, quick cold start, instant hot update.
    link: https://vitejs.dev/
    linkText: Official Site
  - title: Shadcn UI
    icon:
      src: /logos/shadcn-ui.svg
    details: Core based on Shadcn UI + Tailwindcss, business can support any UI framework.
    link: https://www.shadcn-vue.com/
    linkText: Official Site
  - title: Turbo Repo
    icon:
      src: /logos/turborepo.svg
    details: Standard and standardized large warehouse architecture, using pnpm + monorepo + turbo engineering management mode, providing enterprise-level development specifications.
    link: https://turbo.build/
    linkText: Official Site
  - title: Nitro Mock Server
    icon:
      src: /logos/nitro.svg
    details: Built-in Nitro Mock service, making your mock service more powerful.
    link: https://nitro.unjs.io/
    linkText: Official Site
---

<!-- <script setup>
import {
  VPTeamPage,
  VPTeamPageTitle,
  VPTeamMembers,
  VPTeamPageSection
} from 'vitepress/theme';

const members = [
  {
    avatar: 'https://avatars.githubusercontent.com/u/28132598?v=4',
    name: 'Vben',
    title: 'Creator',
    desc: 'Author of Vben Admin and related ecosystem, responsible for overall project development.',
    links: [
      { icon: 'github', link: 'https://github.com/anncwb' },
    ]
  },
]
</script>

<VPTeamPage>
  <VPTeamPageTitle>
    <template #title>
      Core Member Introduction
    </template>
  </VPTeamPageTitle>
  <VPTeamMembers
    :members="members"
  />
</VPTeamPage> -->

<VbenContributors />
