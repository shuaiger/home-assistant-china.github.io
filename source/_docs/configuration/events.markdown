---
layout: page
title: "事件"
description: "一切关于HomeAssistant事件的相关描述"
date: 2016-03-12 12:00 -0800
sidebar: true
comments: false
sharing: true
footer: true
redirect_from: /topics/events/
---

事件总线是HomeAssistant的核心，它允许任何组件来触发或监听所有事件。这是一切的核心。例如，任何状态变化都将在事件总线上反映为一个 `state_changed` 事件，其中包括这个实体先前的状态和当前的状态。

HomeAssistant包含一些内置的事件,用以协调不同组件之间的互动。

### {% linkable_title `homeassistant_start` 事件 %}
`homeassistant_start` 事件会在配置文件中的所有组件都初始化后被触发。它被触发的同时将启动 `time_changed` 事件中的计时器，用以计算状态改变后所经历的时间。

### {% linkable_title `homeassistant_stop` 事件 %}
`homeassistant_stop` 在HomeAssistant关闭时被触发。它可被用于关掉相关网络连接和释放相应的资源。

### {% linkable_title `state_changed` 事件 %}
Event `state_changed` is fired when a state changes. Both `old_state` and `new_state` are state objects. [Documentation about state objects.](/topics/state_object/)

Field | Description
----- | -----------
`entity_id` | Entity ID of the changed entity. Example: `light.kitchen`
`old_state` | The previous state of the entity before it changed. This field is ommitted if the entity is new.
`new_state` | The new state of the entity. This field is ommitted if the entity is removed from the state machine.


### {% linkable_title Event `time_changed` %}
Event `time_changed` is fired every second by the timer and contains the current time.

Field | Description
----- | -----------
`now` | A [datetime object](https://docs.python.org/3.4/library/datetime.html#datetime.datetime) containing the current time in UTC.


### {% linkable_title Event `service_registered` %}
Event `service_registered` is fired when a new service has been registered within Home Assistant.

Field | Description
----- | -----------
`domain` | Domain of the service. Example: `light`.
`service` | The service to call. Example: `turn_on`


### {% linkable_title Event `call_service` %}
Event `call_service` is fired to call a service.

Field | Description
----- | -----------
`domain` | Domain of the service. Example: `light`.
`service` | The service to call. Example: `turn_on`
`service_data` | Dictionary with the service call parameters. Example: `{ 'brightness': 120 }`.
`service_call_id` | String with a unique call id. Example: `23123-4`.


### {% linkable_title Event `service_executed` %}
Event `service_executed` is fired by the service handler to indicate the service is done.

Field | Description
----- | -----------
`service_call_id` | String with the unique call id of the service call that was executed. Example: `23123-4`.


### {% linkable_title Event `platform_discovered` %}
Event `platform_discovered` is fired when a new platform has been discovered by the discovery component.

Field | Description
----- | -----------
`service` | The service that is discovered. Example: `zwave`.
`discovered` | Information that is discovered. Can be a dict, tuple etc. Example: `(192.168.1.10, 8889)`.


### {% linkable_title Event `component_loaded` %}
Event `component_loaded` is fired when a new component has been loaded and initialized.

Field | Description
----- | -----------
`component` | Domain of the component that has just been initialized. Example: `light`.
