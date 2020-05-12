# Argonaut Subscription Projects

This is a general overview page for the software hosted at [subscriptions.argo.run](http://subscriptions.argo.run), which can be used to test R5 Subscriptions.

If you have any comments or questions, feel free to ping me on [Zulip](https://chat.fhir.org/#narrow/pm-with/222054-gino.canessa).

# Overview

There are three main projects which together implement the entire Subscriptions workflow:
* A C# [FHIR Server Proxy](#server)
* A React/TypeScript [Client](#client)
* A C# [Endpoint Hosting Server](#endpoint-host)

Additionally, there are two basic client projects to serve as examples:
* A [C# Client](#devdays-cs)
* A [Node/JS Client](#devdays-js)

# Links

Projects are currently running the [May 2020 R5](http://hl7.org/fhir/2020May/) milestone.
* [SubscriptionTopic](http://hl7.org/fhir/2020May/subscriptiontopic.html)
* [Subscription](http://hl7.org/fhir/2020May/subscription.html)
* [SubscriptionStatus](http://hl7.org/fhir/2020May/subscriptionstatus.html)
* subscription-notification [Bundle](http://hl7.org/fhir/2020May/bundle.html#subscription-notification)

These projects additionally use a few artifacts from the Argonaut 2019 Subscriptions Project:
* Draft [Encounters IG](https://github.com/argonautproject/subscriptions/blob/master/encounters-ig.md)
  * Canonical SubscriptionTopic: [encounter-start](https://raw.githubusercontent.com/argonautproject/subscriptions/master/canonical/subscriptiontopic-encounter-start.json)
* Draft [Backport to R4](https://github.com/argonautproject/subscriptions/blob/master/backport-to-r4.md) Guide

# [FHIR Server Proxy](#server)
* [GitHub Repo](https://github.com/microsoft-healthcare-madison/argonaut-subscription-server-proxy)
* Azure Hosted URL: [server.subscriptions.argo.run](http://server.subscriptions.argo.run) (FHIR R4 Endpoint)

The Server Proxy is a thin server layer (pointing to [hapi.fhir.org](hapi.fhir.org)) which intercepts resources needed to support subscriptions:
* Subscription
* SubscriptionTopic
* Basic
* Encounter

# [Client](#client)
* [GitHub Repo](https://github.com/microsoft-healthcare-madison/argonaut-subscription-client-ui)
* Azure Hosted URL: [subscriptions.argo.run](http://subscriptions.argo.run) (Web Page)

The Client has been written to be as self-contained as possible. The major issue with running the client a web-browser is that it cannot host REST endpoints. Instead, the client connects to the [Endpoint Host](#endpoint-host) via Websockets and receives notifications from there.

Since the client is in the browser and the `Endpoint Host` is public, you can use the client to test against locally hosted servers.

## Client Tab: Config
* Settings (e.g., URLs, light/dark look, etc.)
  * FHIR Server URL can be set to your test URL
  * Again, since everything runs in the browser, it can point to localhost, etc.
  * The "Use Backport to R4" setting turns on/off wrapping `Subscription` and `SubscriptionTopic` in `Basic` resources
    * Note that notifications are still sent using R5 models - I have an idea I'm working on for this
  * Connecting gets the Capabilities Statement and checks for needed capabilities based on the operations in the UI
  * If you are having trouble connecting to your server, turn on the 'Skip FHIR Server Capabilities Check' toggle
* Useful links (e.g., to the current and previous Connectathons, to the GitHub repos of this software, etc.)
* Connect/Disconnect button: connect to the server and client host (required for all other operations)

## Client Tab: Patient + REST
* Walks through a single-patient encounter notification and REST notifications
* "On Rails" guided version, only options available are valid for the scenario

## Client Tab: Group + REST
* Same as above, but uses the `Group` resource for filtering events instead of `Patient` directly

## Client Tab: Playground
* Named appropriately  :-)
* Allows for testing of things like Websockets, Email, etc.

## Client Tab: DevDays
* The most BASIC self-contained client tutorials I could come up with.
* More info can be found on my last [DevDays slides](https://aka.ms/devdays-gino)


# [Endpoint Hosting Server](#endpoint-host)
* [GitHub Repo](https://github.com/microsoft-healthcare-madison/argonaut-subscription-client)
* Azure Hosted URL: [client.subscriptions.argo.run](http://client.subscriptions.argo.run) (Web API)

The Endpoint Hosting Server is a host that interacts with a [Client](#client) via Websockets to host public-accessible HTTP/S endpoints. It is only useful in the context of the Client, so may generally be ignored.

# [DevDays C# Client](#devdays-cs)
* [GitHub Repo](https://github.com/microsoft-healthcare-madison/devdays-2019-subscription-cs)

This is a simple, self-contained Subscriptions client in C#.  Directions for use can be found in the DevDays tab of the client ([here](https://subscriptions.argo.run)).


# [DevDays Node/JS Client](#devdays-js)
* [GitHub Repo](https://github.com/microsoft-healthcare-madison/devdays-2019-subscription-node)

This is a simple, self-contained Subscriptions client in JavaScript, using Node.  Directions for use can be found in the DevDays tab of the client ([here](https://subscriptions.argo.run)).

## Contributing
This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

There are many other ways to contribute:
* [Submit bugs](https://github.com/argonaut-subscription-info/issues) and help us verify fixes as they are checked in.
* Review the [source code changes](https://github.com/argonaut-subscription-info/pulls).
* Engage with users and developers on [Official FHIR Zulip](https://chat.fhir.org/)
* [Contribute bug fixes](CONTRIBUTING.md).

See [Contributing](CONTRIBUTING.md) for more information.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

FHIR&reg; is the registered trademark of HL7 and is used with the permission of HL7. 