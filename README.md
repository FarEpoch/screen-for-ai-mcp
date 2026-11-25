# Screen for AI MCP

[Screen for AI](https://screenforai.app/) is an MCP server and Android app for putting custom HTML interfaces on physical screens. A compatible AI agent can send a page to a named phone or tablet, leave it running there and later read the choices, measurements or scores that people saved.

## What runs on the screen

The app renders HTML, CSS and JavaScript locally in Android’s Chromium-based WebView. A page can lay out touch controls for the available screen size, animate a change or draw a chart with SVG or canvas. You can deliver a self-contained tool without hosting a website or building an Android app for it. Browser APIs and media formats depend on the installed WebView and the page’s security mode.

For example, a workbench page can keep a checklist beside a drawing. A game-night scoreboard can update after each tap, save the running totals and record individual points. Later the AI can read those values and send back a chart. [See the scoreboard walkthrough.](https://screenforai.app/game-night-scorekeeper)

The device keeps delivered pages and the state and events they explicitly save through the page runtime. A kept page can be reopened or updated. Its local controls can work after the chat closes or the internet drops. Online data sources still need a connection. Reading saved input normally takes a new request from the AI.

## How the connection works

```text
Hosted     AI app ⇄ hosted MCP server ⇄ Android screen
Local      AI tool and connector on your computer ⇄ Android screen
```

Over the internet, the AI app uses the Model Context Protocol (MCP) over Streamable HTTP with OAuth. The phone connects out to the service. After approval, the AI can list its authorized screens, deliver HTML and request saved input from the device. Both links are encrypted in transit. The service processes the page and the requested answers in readable form.

On the same Wi-Fi, a compatible local connector can connect directly over encrypted transport with approval on the phone. This path needs no Screen for AI account or hosted service. Cloud-based AI apps use the hosted path even when you open their chat on your home Wi-Fi. [Check direct connection requirements.](https://screenforai.app/setup#same-wifi)

For an agent, the basic tool sequence is `devices_list` to find an approved screen, `display_render_html` to deliver the page and `view_get_state` or `view_get_events` to retrieve what the page saved. Check the capabilities reported for the selected screen before requesting an operation.

## Connect

1. Install [Screen for AI on Google Play](https://play.google.com/store/apps/details?id=app.screenforai). Open the app and follow the steps to connect the screen **Over the internet**.
2. In Claude, open the [Screen for AI connector](https://claude.ai/directory/screen-for-ai) and choose **Connect to Claude**. For other AI apps, check the [setup guide](https://screenforai.app/setup) for compatibility. The service uses `https://app.screenforai.app/mcp` over Streamable HTTP with OAuth.
3. Sign in with the same Screen for AI account you used on the Android screen.

## Try it

> Use Screen for AI to show a Yes or No question on my Kitchen screen. Ask whether I want coffee.

After you tap an answer, ask your AI what you chose. Replace *Kitchen* with the name you gave your screen.

## Registry and support

The [Official MCP Registry entry](https://registry.modelcontextprotocol.io/?q=app.screenforai%2Fscreen-for-ai) is `app.screenforai/screen-for-ai`. The [server manifest](server.json) describes the hosted connector.

Published by [Far Epoch](https://screenforai.app/publisher/). For help connecting, see [Screen for AI support](https://screenforai.app/support).
