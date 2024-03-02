---
title: "{{ replace .Name "-" " " | title }}"
slug: "{{ .Name }}"
tags:
  - test
date: "{{ time.Format "2006-01-02" .Date }}"
update: "{{ time.Format "2006-01-02" .Date }}"
draft: true
---
