# Topics

## PubSub Topics

PubSub topics are topics in Fundamentum's event broker. They can be used with the [PubSub Bridge Adapter](./pubsub-bridge.md) to transmit or receive messages. PubSub topics store up to 7 days of messages. Messages older than that are deleted automatically.

PubSub topics have the following fields:

- **Name**: The short name of the topic. It must contain only alphanumeric characters and be between 3 and 256 characters long. The full topic name is automatically generated from the short name (see [Topic Naming](#topic-naming)).
- **Default Type**: Defines the category and direction of the topic from the client's point of view. Possible values are:
  - `telemetry` — subscribing only (also known as *readings*)
  - `states` — subscribing only
  - `custom_actions` — publishing only
- **Is Default**: Whether this is the default topic for its type within the project. There can be at most one default topic per type per project. Setting a new topic as default automatically unsets the previous default of the same type. See [Registry topics](#registry-topics) for use

Three default topics are created for each project:
- `states`
- `readings`
- `custom_actions`

### Dimension Topics

Dimension topics are a special kind of PubSub topic. They are created automatically when a [Fundamentum Topic](#fundamentum-topics) is activated for a project. They cannot be created or modified directly, they have no default topic, and they are subscribe only. See the [Fundamentum Topics](#fundamentum-topics) section for more information.

### Topic Naming

The full name of a PubSub topic is constructed automatically from the short name provided by the user. The format is:

```
regions.{regionId}.projects.{projectId}.topics.{name}
```

For dimension topics, the format is:

```
regions.{regionId}.projects.{projectId}.dimensions.{source}
```

Where:
- `regionId` is the identifier of the region in which the topic exists
- `projectId` is the identifier of the project that owns the topic
- `name` is the short name provided when creating the topic
- `source` is the name of the Fundamentum topic the dimension topic was created from

### Deletion Rules

- A PubSub topic cannot be deleted if it is referenced by registry topics. The references must be removed first.
- Deleting a PubSub topic that is the destination of an active Fundamentum topic link will automatically deactivate that link before deleting the topic.

### Why the region prefix?

Most platforms run separate instances per region, so topics are inherently scoped to a single region. Fundamentum's event broker (Redpanda) spans multiple regions simultaneously for replication purposes. The region prefix disambiguates topics that exist across different regions within the same broker. This prefix is applied automatically — users only need to provide the short topic name.

## Fundamentum Topics

Many events occur within the platform — a device sending a state, an alert being triggered, a change in a registry, and more. These events are published to Fundamentum topics. By activating a Fundamentum topic for your project, you can receive a copy of every relevant message in a dedicated [dimension topic](#dimension-topics).

### Activation

Activating a Fundamentum topic for a project creates a link between the source topic and the project. This automatically creates a PubSub topic of type `dimension` named `projects.{projectId}.dimensions.{source}` (if it does not already exist). From that point on, every message on the Fundamentum topic that concerns the project is copied in real time to the dimension topic.

### Deactivation

Deactivating a Fundamentum topic removes the link between the source topic and the project. The dimension PubSub topic is **not** deleted, so it can be reused if the Fundamentum topic is reactivated later.

Messages that transit on the Fundamentum topic between deactivation and the next activation are **not** forwarded. They are lost permanently and will not be copied retroactively.

## Registry Topics

Registry topics are MQTT topics that link devices to [PubSub topics](#pubsub-topics). They allow devices to publish or subscribe to messages that are forwarded to and from the event broker. Registry topics are created and managed through registries.

Each registry topic has a **type** that matches the [default types](#pubsub-topics) of PubSub topics: `telemetry`, `states`, or `custom_actions`. The type determines the direction of message flow — the same direction rules as PubSub topics apply. The MQTT Topic's direction is always the opposite of the PubSub Topic, e.g. devices publish on `telemetry` MQTT Topic and the associated PubSub Topic can be subscribed to.

### Default Registry Topics

When a registry is created, one registry topic is automatically created for each type (`telemetry`, `states`, `custom_actions`). These default registry topics have no subtype and are linked to the [default PubSub topic](#pubsub-topics) of each type.

### Custom Registry Topics

Users can create additional registry topics by specifying a **subtype name**. Custom registry topics are linked to a PubSub topic of the corresponding type.

### MQTT Topic Naming

Devices interact with registry topics through MQTT topics following this naming pattern:

```
registries/{registry-id}/devices/{serial-number}/{type}/{subtype}
```

Where `{type}` corresponds to the registry topic type:
- `events` for telemetry
- `states` for states
- `custom_actions` for custom actions

For default registry topics (no subtype), `{subtype}` is omitted.

## Managing PubSub Topics

The following procedures explain how to interact with PubSub topics through the Hub and the public API.

### List PubSub Topics

Retrieve all PubSub topics for a project, including their name, default type, default status, number of linked registry topics.

<details>
  <summary>Hub</summary>

  1. Navigate to **PubSub** (https://hub.fundamentum-iot.com/pub-sub-topics)

  The PubSub Topic list will be at the top of the page.

</details>

<details>
  <summary>API</summary>

  https://api.fundamentum-iot.com/v1/huma#/operations/listPubSubTopics

</details>

### Create a PubSub Topic

Create a new PubSub topic for a project. The name must be alphanumeric and between 3 and 256 characters. The type cannot be `dimension` — dimension topics are created automatically through [Fundamentum Topics](#fundamentum-topics).

Only one default topic per type is allowed in a project. Setting `is_default` to true will automatically unset the previous default of the same type. Default topics are used when provisioning [registry topics](#registry-topics) for new registries.

<details>
  <summary>Hub</summary>

  1. Navigate to **PubSub** (https://hub.fundamentum-iot.com/pub-sub-topics)
  2. Click **New Topic**
  3. Fill in the fields
  4. Click **Save**

</details>

<details>
  <summary>API</summary>

  https://api.fundamentum-iot.com/v1/huma#/operations/storePubSubTopic

  - Default type accepted values are: `telemetry`, `states` and `custom_actions`
  - The name is the short name of the topic. See [Topic Naming](#topic-naming)

</details>

### Update a PubSub Topic

Update the name, default type, or default status of an existing PubSub topic. Dimension topics cannot be updated.

Changing `is_default` to true will unset the previous default topic of the same type. See [Create a PubSub Topic](#create-a-pubsub-topic) for details.

<details>
  <summary>Hub</summary>

  1. Navigate to **PubSub** (https://hub.fundamentum-iot.com/pub-sub-topics)
  2. Find the relevant PubSub Topic in the list
  3. Click the **Edit** button of its row
  4. Change relevant fields
  5. Click **Save**

</details>

<details>
  <summary>API</summary>

  https://api.fundamentum-iot.com/v1/huma#/operations/updatePubSubTopic

  - Default type accepted values are: `telemetry`, `states` and `custom_actions`
  - The name is the short name of the topic. See [Topic Naming](#topic-naming)

</details>

### Delete a PubSub Topic

Delete a PubSub topic. See [Deletion Rules](#deletion-rules) for restrictions.

<details>
  <summary>Hub</summary>

  1. Navigate to **PubSub** (https://hub.fundamentum-iot.com/pub-sub-topics)
  2. Find the relevant PubSub Topic in the list
  3. Click the **Delete** button of its row
  4. Confirm the change

</details>

<details>
  <summary>API</summary>

  https://api.fundamentum-iot.com/v1/huma#/operations/deletePubSubTopic

  - PubSub Topics associated to at least one Registry Topic cannot be deleted

</details>

## Managing Fundamentum Topic Links

The following procedures explain how to manage Fundamentum topic forwarding through the Hub and the public API.

### List Fundamentum Topic Links

Retrieve all active Fundamentum topic links for a project. Each link shows the source Fundamentum topic and the destination dimension PubSub topic.

<details>
  <summary>Hub</summary>

  1. Navigate to **PubSub** (https://hub.fundamentum-iot.com/pub-sub-topics)

  The Fundamentum Topic Links list will be at the bottom of the page.

</details>

<details>
  <summary>API</summary>

  https://api.fundamentum-iot.com/v1/huma#/operations/listPubSubTopics

  PubSub topics that are linked will have the `scoped_from` field containing the Fundamentum Topic. Note that this is the same endpoint as listing PubSub topics.

</details>

### Activate a Fundamentum Topic

Activate forwarding of a Fundamentum topic to a project. A dimension PubSub topic is automatically created if it does not already exist. This operation is idempotent — activating an already-active link returns the existing link.

<details>
  <summary>Hub</summary>

  1. Navigate to **PubSub** (https://hub.fundamentum-iot.com/pub-sub-topics)
  2. Find the relevant Fundamentum Topic
  3. Click the "Activate" button on the same row

</details>

<details>
  <summary>API</summary>

  https://api.fundamentum-iot.com/v1/huma#/operations/scopePubSubTopic

  The list of Fundamentum Topics can be found here https://api.fundamentum-iot.com/v1/huma#/operations/listScopeableTopics

</details>

### Deactivate a Fundamentum Topic

Stop forwarding messages from a Fundamentum topic to a project. The dimension PubSub topic is preserved and can be reused if the link is reactivated later. Messages that occur during the inactive period are lost permanently.

<details>
  <summary>Hub</summary>

  1. Navigate to **PubSub** (https://hub.fundamentum-iot.com/pub-sub-topics)
  2. Find the relevant Fundamentum Topic
  3. Click the "Deactivate" button on the same row

</details>

<details>
  <summary>API</summary>

  https://api.fundamentum-iot.com/v1/huma#/operations/unscopePubSubTopic

</details>

## Managing Registry Topics

The following procedures explain how to manage registry topics through the Hub and the public API.

### List Registry Topics

Retrieve all registry topics for a given registry, including their type, subtype, and linked PubSub topic.

<details>
  <summary>Hub</summary>

  1. Navigate to **Registry** (https://hub.fundamentum-iot.com/registries)
  2. Select your registry
  3. Select the "PubSub Topics" tab

</details>

<details>
  <summary>API</summary>

  https://api.fundamentum-iot.com/v1/huma#/operations/getRegistry

  Registry topics will be in the `topics` field

</details>

### Create a Registry Topic

Create a new registry topic for a registry. A subtype name and a PubSub topic of the corresponding type must be specified.

<details>
  <summary>Hub</summary>

  1. Navigate to **Registry** (https://hub.fundamentum-iot.com/registries)
  2. Select your registry
  3. Select the "PubSub Topics" tab
  4. Click **New Connection**
  5. Fill in the fields
  6. Click **Confirm**

</details>

<details>
  <summary>API</summary>

  https://api.fundamentum-iot.com/v1/huma#/operations/storeRegistryTopic

  - Type accepted values are: `telemetry`, `states` and `custom_actions`

</details>

### Update a Registry Topic

Update a registry topic's type or linked PubSub topic.

<details>
  <summary>Hub</summary>

  1. Navigate to **Registry** (https://hub.fundamentum-iot.com/registries)
  2. Select your registry
  3. Select the "PubSub Topics" tab
  4. Find the Registry Topic in the list
  5. Click the **Edit** button
  6. Change relevant fields
  7. Click **Confirm**

</details>

<details>
  <summary>API</summary>

  https://api.fundamentum-iot.com/v1/huma#/operations/updateRegistryTopic

  - Type accepted values are: `telemetry`, `states` and `custom_actions`

</details>

### Delete a Registry Topic

Delete a registry topic. This removes the link between the MQTT topic and the PubSub topic. Default registry topics cannot be deleted.

<details>
  <summary>Hub</summary>

  1. Navigate to **Registry** (https://hub.fundamentum-iot.com/registries)
  2. Select your registry
  3. Select the "PubSub Topics" tab
  4. Find the Registry Topic in the list
  5. Click the **Delete** button
  6. Confirm the change

</details>

### Reset Registry topics

Deletes **all** registry topics and re-creates the default registry topics.

<details>
  <summary>Hub</summary>

  1. Navigate to **Registry** (https://hub.fundamentum-iot.com/registries)
  2. Select your registry
  3. Select the "PubSub Topics" tab
  4. Click **Restore Defaults**
  5. Confirm the change

</details>

<details>
  <summary>API</summary>

  https://api.fundamentum-iot.com/v1/huma#/operations/resetRegistryTopics

</details>
