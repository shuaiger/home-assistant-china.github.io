---
layout: page
title: "为HomeAssistant添加设备"
description: "添加设备到HomeAssistant的步骤"
date: 2015-09-19 09:40
sidebar: true
comments: false
sharing: true
footer: true
redirect_from: /getting-started/devices/
---

HomeAssistant会自动识别你局域网中多种可用设备和服务，前提是你打开了 [发现](/components/discovery/) 功能（默认开启）。

访问 [组件概览页面](/components/) 来查看设备和服务安装指引。如果你没有找到对于你喜爱设备的支持，可以考虑自己 [开发新的平台](/developers/add_new_platform/) 来支持它。

通常地，每一个实体（设备）都需要在 `configuration.yaml` 文件中有一个定义，可以通过以下两种方式来添加多个实体：

#### {% linkable_title 方式一：将所有实体都放在一个“父标签”下 %}

```yaml
sensor:
  - platform: mqtt
    state_topic: "home/bedroom/temperature"
    name: "MQTT Sensor 1"
  - platform: mqtt
    state_topic: "home/kitchen/temperature"
    name: "MQTT Sensor 2"
  - platform: rest
    resource: http://IP_ADDRESS/ENDPOINT

switch:
  - platform: vera
```

#### {% linkable_title 方式二：单独列出所有实体 %}

你需要在类别后面添加数字或字符串以区分不同实体，添加的数字或字符串必须保证唯一。

```yaml
media_player livingroom:
  platform: mpd
  server: IP_ADDRESS

media_player kitchen:
  platform: plex

camera 1:
  platform: generic

camera 2:
  platform: mjpeg
```

### {% linkable_title 设备分组 %}

一旦你添加了多个设备到HomeAssistant，这时你将需要将他们分组显示和管理。每个分组包含一个组名称和一系列实体ID。实体ID可以从Web界面-管理工具-Set State部分(<img src='/images/screenshots/developer-tool-states-icon.png' alt='service developer tool icon' class="no-shadow" height="38" />)来获取。

```yaml
# configuration.yaml配置示例展示了两种实体ID的给定方式
group:
  living_room: light.table_lamp, switch.ac
  bedroom:
    - light.bedroom
    - media_player.nexus_player
```

更多细节请参考 [分组](/components/group/) 页面。

By [Jones](https://bbs.hassbian.com/home.php?mod=space&username=Jones)
