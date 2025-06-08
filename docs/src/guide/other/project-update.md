# Project Update

## Why Can't It Be Updated Like an NPM Package?

Because the project is a complete project template, not a plugin or installation package, it cannot be updated like a plugin. After you use the code, you will need to perform secondary development based on business requirements, and you need to manually merge updates.

## What Do I Need to Do?

The project uses `Monorepo` for management and has extracted some core code, such as `packages/@core` and `packages/effects`. As long as the business code has not modified these parts, you can directly pull the latest code and merge it into your branch, only needing to handle a few conflicts. The remaining folders will only have minor adjustments that won't affect the business code.

::: tip Recommended
It is recommended to follow the repository updates and actively merge changes. Do not accumulate too many changes for a long time, as this will lead to excessive merge conflicts and increase the difficulty of merging.

## Use Git to Update Code

1. Clone the code

```bash
git clone https://github.com/elgaml/vue-vben-admin.git
```

2. Add your company's git source address

```bash
# up is the source name, you can set it as you like
# gitUrl is the latest open source code
git remote add up gitUrl;
```

3. Submit code to your company's git

```bash
# Submit code to your company
# main is the branch name, modify as needed
git push up main

# 同步公司的代码
# main为分支名 需要自行根据情况修改
git pull up main
```

4. 如何同步开源最新代码

```bash
git pull origin main
```

::: tip 提示

同步代码的时候会出现冲突。只需要把冲突解决即可

:::
