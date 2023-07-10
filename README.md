# Modified from Rusty!nk

[![Build & test](https://github.com/callmedar/callmedar.github.io/actions/workflows/build_test.yml/badge.svg)](https://github.com/callmedar/callmedar.github.io/actions/workflows/build_test.yml)
[![Publish to Pages](https://github.com/callmedar/callmedar.github.io/actions/workflows/publish.yml/badge.svg)](https://github.com/callmedar/callmedar.github.io/actions/workflows/publish.yml)

![Show this site](https://callmedar.github.io)

### Installation
You can install RustyInk using Cargo:
```bash
cargo install rustyink
```

### Create new project
You can initialise a new project using `new` command.
```bash
rustyink new <folder>
```

You can optionally specify a theme also.
```bash
rustyink new <folder> -t pico
```

### Run project locally
Using `rustyink` command with `<input-dir>` as `docs` in this project:
```bash
rustyink dev --watch <INPUT-DIR>
```
### Modified your Markdown file
```md
---
template: post
title: "This Blog Written in Rust"
author: Syuhendar
author_link: https://github.com/syuhendar729
date_published: 3 Juli, 2023
---
```

### How hosting this site in github pages?
- You can create repostiroy `your-organization.github.io` and push your project.
- Let actions `publish.yml` and `build_test.yml` build it.
- Wait a few minutes and it's done.
- Your website can be show in https://your-organization.github.io

Enjoy create your own site with Rust!!
