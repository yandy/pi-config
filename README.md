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
npx skills add <package> --skill <skills> -a universal -y
# eg.
npx skills add anthropics/skills --skill pdf docx -a universal -y
```

### 2.2 Update skills

```sh
npx skills update <skills> -p -y
```

### 2.3 Remove skills

```sh
npx skills remove <skills> -a universal
```

### 2.4 List skills

```sh
npx skills ls -a universal
```

### 2.5 Current skills

- office

```sh
# npx skills add anthropics/skills --skill pdf -a universal -y
```

- browser automation

```sh
npm install -g playwright @playwright/cli
playwright install chromium firefox
# npx skills add microsoft/playwright-cli --skill playwright-cli -a universal -y
```

- [context7](https://github.com/upstash/context7)

```sh
npx ctx7 login
# npx skills add upstash/context7 --skill find-docs -a universal -y
```

- [mediagen-cli](https://github.com/yandy/mediagen-cli)

```sh
# npx skills add yandy/mediagen-cli -a universal -y
```
