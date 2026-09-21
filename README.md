# Pi Config for Coding

## 1. Setup

```sh
# install pi
npm install -g @earendil-works/pi-coding-agent

# clone config
git clone https://github.com/yandy/pi-config.git ~/.pi/agent
```

## 2. Skills Management

### 2.1 Add skill

```sh
npx skills add <package> --skill <skills> -a pi -y
# eg.
npx skills add anthropics/skills --skill pdf docx -a pi -y
```

### 2.2 Update skills

```sh
npx skills update -a pi
```

### 2.3 Remove skills

```sh
npx skills remove <skills> -a pi
```

### 2.4 List skills

```sh
npx skills ls -a pi
```

### 2.5 Current skills

- skill-creator

```sh
# npx skills add anthropics/skills --skill skill-creator -a pi -y
```

- office

```sh
# npx skills add anthropics/skills --skill pdf -a pi -y
```

- ui/ux

```sh
# npx skills add nextlevelbuilder/ui-ux-pro-max-skill --skill ui-ux-pro-max -a pi -y
# npx skills add alchaincyf/huashu-design --skill huashu-design -a pi -y
```

- browser automation

```sh
npm install -g playwright @playwright/cli
playwright install chromium firefox
# npx skills add microsoft/playwright-cli --skill playwright-cli -a pi -y
```

- [context7](https://github.com/upstash/context7)

```sh
npx ctx7 login
# npx ctx7 setup --pi
```
