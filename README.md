# Optimal Beam for Gemini CLI

Connect Gemini CLI to [Optimal Beam](https://optimalbeam.com) for linear elastic
beam calculations and steel section catalog lookups. The connector returns
numerical results, units, assumptions and warnings in the conversation, with
optional links to continue working on the model or catalog in Optimal Beam.

## Connection

The plugin uses the public Streamable HTTP MCP endpoint:

`https://mcp.optimalbeam.com/gemini/mcp`

No Optimal Beam account, API key, OAuth login or environment variable is required.
This package contains only connector configuration, metadata and documentation.
It has no local commands, hooks, dependencies, installation scripts or telemetry.

Install with [Gemini CLI](https://geminicli.com/docs/get-started/installation/):

```sh
gemini extensions install https://github.com/tamerhijjawi/optimal-beam-gemini
```

Review and accept the extension's connection details when prompted. Start a new
Gemini CLI session, or reload extensions, then use `/mcp` to inspect the tools.
Normal tool approval prompts remain enabled. Gemini CLI itself requires a
supported Google login or API configuration; Optimal Beam needs no separate key.

This extension targets Gemini CLI. It does not install a connector in the regular
Gemini chat app. Gallery indexing is separate from direct installation and follows
Google's [extension release process](https://geminicli.com/docs/extensions/releasing/).

## Tools

| Tool | Purpose |
| --- | --- |
| `analyze_beam` | Calculate reactions, shear, bending moment, slope, deflection and available stresses. |
| `search_steel_sections` | Search supported steel section catalogs. |
| `get_steel_section` | Retrieve a section's dimensions and geometric properties. |
| `find_steel_alternatives` | Find nearby catalog alternatives. |
| `compare_steel_sections` | Compare a specified shortlist's properties or elastic beam responses. |
| `show_steel_sections` | Return catalog details and an optional website continuation link. |
| `show_beam_results` | Return a temporary calculation/comparison snapshot and optional model links. |

All seven tools are read-only calculations and catalog lookups. They do not read
or modify saved Optimal Beam account models, payment information or account
settings. Calculations can create temporary result references in server memory.

## Example

Ask Gemini CLI:

> Use Optimal Beam to analyze a 6 m simply supported beam, pinned at 0 m and on
> a roller at 6 m, with a 10 kN downward point load at midspan. Exclude self-weight.
> Use E = 200000 MPa, I = 200000000 mm^4, A = 5000 mm^2 and top/bottom extreme
> fiber distances of 100 mm. Report reactions, maximum moment and deflection.

Expected magnitudes: 5 kN upward reaction at each support, 15 kN m maximum
bending moment and 1.125 mm maximum downward deflection. Report directions and
the tool's sign convention alongside values.

## Scope and data handling

The service performs linear elastic, small-displacement analysis. Member
capacity, buckling, connections, certification and design-code compliance are
outside its scope. Material properties, section properties and self-weight
assumptions must be stated. Alternatives are not code-approved recommendations.

Network access from this plugin is limited to
`https://mcp.optimalbeam.com/gemini/mcp` for tool discovery and requested tool calls.
The hosted backend uses Optimal Beam's website/catalog services and Azure
numerical solver to fulfill those requests. Optional website links point to
`https://optimalbeam.com` and open only when the user follows them.

User-supplied beam dimensions, supports, loads, material/section properties,
catalog queries and any short labels are sent to the service. Do not include
personal or confidential information in labels. The plugin has no local file,
shell, credential or full-conversation access of its own.

Calculation/comparison snapshots are held in process memory for up to 30 minutes.
Result IDs are bearer references and should not be shared with unintended
recipients. Hosting operational logs and Gemini conversation retention are separate
from that cache expiry. See the
[privacy policy](https://optimalbeam.com/privacy.php#chatgpt-plugin) for details.

## Publisher and support

Published by **Optimal Beam Inc.** Questions and deletion requests:
**contact@optimalbeam.com**.

- Website: https://optimalbeam.com
- Setup and support: https://optimalbeam.com/plugin-support.html
- Privacy: https://optimalbeam.com/privacy.php#chatgpt-plugin

## License

The configuration and documentation in this extension repository are licensed under
MIT; see [LICENSE](LICENSE). This license does not cover the hosted Optimal Beam
service, its solver, catalogs, trademarks or other website content. The service's
published terms and privacy policy continue to apply.
