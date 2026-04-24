# haaInlineEnhancedChatTransparent

A Lightning Web Component (LWC) that embeds an Agentforce Enhanced Chat window inline on an Experience Cloud page, with full control over background transparency and text styling — similar to the help experience seen on help.salesforce.com.

This component is a variant of the [Help Agent Accelerator](https://github.com/salesforce/help-agent-accelerator) `haaInlineEnhancedChat` component, extended with declarative App Builder properties for transparency and color customization.

---

## Features

- **Inline chat experience** — embeds Agentforce Enhanced Chat directly on the page without a floating button or modal
- **Transparent background** — the component container and overlays use a transparent background, allowing page backgrounds, images, or branding to show through
- **Configurable input box opacity** — control exactly how transparent the text input box is via a simple percentage property
- **Declarative color controls** — set welcome message text color, placeholder text color, and input text color directly in Experience Builder without touching CSS or custom labels
- **Welcome message override** — specify the heading text directly on the component, bypassing the `HAA_heading` custom label
- **Placeholder text override** — set the input box hint text directly on the component, bypassing the `HAA_input_placeholder` custom label
- **Full state machine** — inherits the robust FSM from the original accelerator, handling loading, launching, sending, active, error, and retry states
- **Canned prompts** — optional preset question buttons driven by custom labels
- **Debug mode** — optional performance logging and timing overlay for troubleshooting

---

## Prerequisites

- Salesforce Experience Cloud site
- Enhanced Chat v2 (Agentforce Messaging) enabled in the org
- An Embedded Service Deployment configured for the Experience Cloud site
- API version 65.0 (Spring '25) or later

---

## Installation

Deploy directly to your org using the Salesforce CLI:

```bash
sf project deploy start \
  --source-dir force-app/main/default/lwc/haaInlineEnhancedChatTransparent \
  --target-org YOUR_ORG_ALIAS
```

---

## App Builder Properties

Once deployed, drag the component onto any Experience Cloud page in Experience Builder. The following properties are configurable in the panel:

### Connection (required)

| Property | Label | Description |
|---|---|---|
| `orgId` | Org ID | 18-character Salesforce Org ID from the deployment Code Snippet |
| `deploymentApiName` | Deployment API Name | Embedded Service Deployment API Name from the Code Snippet |
| `siteUrl` | Site URL | Experience Cloud site base URL — no trailing slash (e.g. `https://yourdomain.my.site.com/your-site`) |
| `scrt2Url` | SCRT URL | SCRT URL from the Code Snippet (e.g. `https://yourdomain.my.salesforce-scrt.com`). Leave blank if not in your snippet. |
| `bootstrapScriptUrl` | Bootstrap Script URL | Override URL for the bootstrap script. Leave blank to auto-derive from Site URL. |

### Layout

| Property | Label | Default | Description |
|---|---|---|---|
| `chatHeight` | Chat Height | `550px` | CSS height of the chat container (e.g. `550px`, `80vh`). Minimum 400px. |

### Transparency & Color

| Property | Label | Default | Description |
|---|---|---|---|
| `inputBoxOpacity` | Input Box Opacity (%) | `30` | Opacity of the text input box as a percentage. `0` = fully transparent, `100` = fully opaque (solid white). |
| `welcomeMessage` | Welcome Message | *(blank)* | Heading text on the prompt screen. Overrides the `HAA_heading` custom label when set. |
| `welcomeMessageColor` | Welcome Message Text Color | *(blank)* | CSS color for the welcome heading (e.g. `#ffffff`, `white`). Falls back to inherited color when blank. |
| `promptPlaceholder` | Message Box Prompt Text | *(blank)* | Placeholder hint text inside the input box. Overrides the `HAA_input_placeholder` custom label when set. |
| `promptPlaceholderColor` | Message Box Prompt Text Color | *(blank)* | CSS color for the input box placeholder text (e.g. `#cccccc`). Falls back to default when blank. |
| `inputTextColor` | Input Text Color | *(blank)* | CSS color for text typed by the user (e.g. `#000000`). Falls back to default when blank. |

### Other

| Property | Label | Default | Description |
|---|---|---|---|
| `showCannedPrompts` | Show Canned Prompts | `false` | Show preset question buttons below the input. Labels sourced from `HAA_canned_prompt_one`, `HAA_canned_prompt_two`, `HAA_canned_prompt_three`. Set a label to `skip` to hide that button. |
| `enableDebugLogs` | Enable Debug Logs | `false` | Logs lifecycle events and timing to the browser console. |

---

## Color Property Format

All color properties accept any valid CSS color value:

```
#ffffff
white
rgb(255, 255, 255)
rgba(255, 255, 255, 0.9)
```

---

## How It Differs from haaInlineEnhancedChat

| Feature | `haaInlineEnhancedChat` | `haaInlineEnhancedChatTransparent` |
|---|---|---|
| Container background | Solid white (`#fff`) | Transparent |
| Loading overlay background | Solid white (`#fff`) | Transparent |
| Error overlay background | Solid white (`#fff`) | Transparent |
| Input box background | Solid white (`#fff`) | Configurable opacity (default 70% transparent) |
| Welcome message text | Driven by `HAA_heading` custom label | Configurable via property (falls back to label) |
| Placeholder text | Driven by `HAA_input_placeholder` custom label | Configurable via property (falls back to label) |
| Text colors | Hardcoded defaults | Configurable via properties |

---

## Related

- [Help Agent Accelerator (source)](https://github.com/salesforce/help-agent-accelerator) — the original component this is based on
